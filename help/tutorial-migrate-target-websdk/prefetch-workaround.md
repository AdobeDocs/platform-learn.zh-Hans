---
title: 用于预取的解决方法 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何实施使用预取传递参数的解决方法
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 用于预取的解决方法

2022年10月1日之前，所有未使用Target Web SDK生产的Target客户，都会使用“预取”模式从Experience Platform边缘网络向Target提出请求。 预取允许浏览器预载并缓存Target选件，以便在访客达到页面的正确状态时即可应用这些选件。 这在单页应用程序(SPA)中是有利的，因为所需的用户体验可以尽可能快速地呈现，而无需其他网络请求。 但是，这对SPA实施和非SPA实施都有重要影响。

现在，在网络请求中交付选件内容时，访客将被计入活动，而不是将访客计入活动 `propositionDisplay` sendEvent请求由Web SDK发出。 当renderDecisions设置为true以及体验已成功在页面上呈现时，可视化体验编辑器(VEC)活动会自动发出这些请求。 如果使用自定义范围，并且将renderDecisions设置为false，则需要实施者特意启动命题显示请求。 此外， _用于除立即活动资格以外的其他目的的所有参数都必须通过 `propositionDisplay`  事件_.

## 为什么需要解决方法？

在许多Target实施中，有时会发出重要的网络请求，而不预期会交付某个活动。 例如，可以向以下用户发出请求：

* 记录订单转化
* 设置配置文件参数
* 触发配置文件脚本
* 发送实体参数以填充Recommendations目录

遗憾的是，在预取模式下，这些量度的行为未按预期方式运行。 在预取模式下，除非此数据是 `propositionDisplay`.

## 解决方法是什么？

解决方法包括三部分：

1. 将自定义范围定义为 `sendEvent`
1. 在基于表单的活动中使用自定义范围（活动可提供默认内容）
1. 使用响应处理程序进行另一个 `sendEvent` 对于命题展示，包括您需要捕获订单、设置配置文件参数、触发配置文件脚本、发送实体参数等参数。

例如，以下是如何使用此解决方法发送用户档案参数的示例：


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

如果将用户档案设置为命题显示的一部分，则会保存到访客的用户档案，并在后续请求中可用。 同一方法可用于报告订单转化详细信息和实体参数。

在标记中，使用“发送事件结束”事件类型触发包含附加sendEvent的事件。

## 如何知道我的实施是否使用预取模式？

您必须打开客户关怀票证，以确定您的帐户是否使用预取模式。


>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).