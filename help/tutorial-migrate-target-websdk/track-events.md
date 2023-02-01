---
title: 跟踪事件 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Experience PlatformWeb SDK跟踪Adobe Target转化事件。
source-git-commit: 43740912bc5a941aa21c5f38ed2c1aac74abffbc
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# 使用Platform Web SDK跟踪Target转化事件

可以使用与at.js类似的平台Web SDK跟踪Target的转化事件。 转化事件通常分为以下类别：

* 自动跟踪不需要任何配置的事件
* 购买应根据最佳实践Platform Web SDK实施进行调整的转化事件
* 需要更新代码的非购买转化事件

>[!WARNING]
>
> 2022年10月1日之后开始的平台Web SDK实施可能需要使用 [prefetch解决方法](prefetch-workaround.md) 以便成功跟踪此页面中描述的某些事件。

## 目标跟踪比较

下表比较了at.js和Platform Web SDK如何跟踪转化事件

| 活动目标 | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 转化>查看页面 | 自动跟踪。 根据 `context.address.url` 在at.js请求有效负载中。 | 自动跟踪。 根据 `xdm.web.webPageDetails.URL` 在 `sendEvent` 负载 |
| 转化>已查看mbox | 通过请求展示型mbox位置或通知来跟踪，使用 `trackEvent()` 或 `sendNotifications()` 带有 `type` 值 `display`. | 使用平台Web SDK跟踪 `sendEvent` 调用 `eventType` of `decisioning.propositionDisplay`. |
| “转化”>“已单击元素” | 自动跟踪基于VEC的活动。 显示为at.js网络调用，其中 `notifications` 请求有效负载中的对象和 `type` 值 `click`. | 自动跟踪基于VEC的活动。 显示为平台Web SDK `sendEvent` 调用 `eventType` of `decisioning.propositionInteract`. |
| 参与度>页面查看次数 | 自动跟踪 | 自动跟踪 |
| 参与度>网站逗留时间 | 自动跟踪 | 自动跟踪 |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## 自动跟踪的事件

以下转化目标不需要对您的实施进行任何具体调整：

* 转化>查看页面
* “转化”>“已单击元素”
* 参与度>页面查看次数
* 参与度>网站逗留时间

>[!NOTE]
>
>平台Web SDK允许更好地控制请求有效负载中传递的值。 要确保Target功能（如QA URL和“已查看页面”转化目标）正常工作，请检查 `xdm.web.webPageDetails.URL` 值包含具有正确字符大小写的完整页面URL。

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## 自定义跟踪事件

Target实施通常使用自定义转化事件来跟踪基于表单的活动的点击次数，表示流中的转化，或传递参数而无需请求新内容。

下表概述了at.js方法和Platform Web SDK等效于一些常见的转化跟踪用例。

| 用例 | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 跟踪mbox位置（范围）的点击转化事件 | 执行 `trackEvent()` 或 `sendNotifications()` 带有 `type` 值 `click` 特定mbox位置 | 执行 `sendEvent` 事件类型为 `decisioning.propositionInteract` |
| 跟踪自定义转化事件，该事件可能还包含其他数据，如Target配置文件参数 | 执行 `trackEvent()` 或 `sendNotifications()` 带有 `type` 值 `display` 特定mbox位置 | 执行 `sendEvent` 事件类型为 `decisioning.propositionDisplay` |

>[!NOTE]
>
>尽管 `decisioning.propositionDisplay` 最常用于增加特定范围的展示次数，也应用作at.js的直接替换 `trackEvent()` 通常。 的 `trackEvent()` 函数默认为 `display` 如果未指定，则。 检查您的实施，以确保为可能已定义的任何自定义转化使用正确的事件类型。

有关如何使用的更多信息，请参阅专用的at.js文档 [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) 和 [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) ，以跟踪Target事件。

at.js示例使用 `trackEvent()` 要跟踪mbox位置上的点击，请执行以下操作：

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

通过平台Web SDK实施，您可以通过调用 `sendEvent` 命令，填充 `_experience.decisioning.propositions` XDM字段组，并设置 `eventType` 值之一：

* `decisioning.propositionDisplay`:表示Target活动的呈现。
* `decisioning.propositionInteract`:表示用户与活动的交互，如鼠标单击。

的 `_experience.decisioning.propositions` XDM字段组是一个对象数组。 每个对象的属性均从 `result.propositions` 在 `sendEvent` 命令： `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

接下来，了解如何 [启用跨域ID共享](cross-domain.md) 以保持访客配置文件的一致性。

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).