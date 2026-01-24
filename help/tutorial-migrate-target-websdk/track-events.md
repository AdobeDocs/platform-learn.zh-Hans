---
title: 跟踪事件 — 将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Experience PlatformWeb SDK跟踪Adobe Target转化事件。
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 使用Platform Web SDK跟踪Target转化事件

与at.js类似，可以使用Platform Web SDK跟踪Target的转化事件。 转化事件通常分为以下类别：

* 自动跟踪不需要任何配置的事件
* 应为最佳实践Platform Web SDK实施调整的购买转化事件
* 需要代码更新的非购买转化事件

## 目标跟踪比较

下表比较了at.js和Platform Web SDK如何跟踪转化事件

| 活动目标 | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 转化>查看页面 | 已自动跟踪。 基于at.js请求有效负载中`context.address.url`的值。 | 已自动跟踪。 基于`sendEvent`有效负载中`xdm.web.webPageDetails.URL`的值 |
| “转化”>“已查看mbox” | 已使用`trackEvent()`或`sendNotifications()`且值为`display`的显示mbox位置或通知请求进行跟踪。`type` | 已使用`decisioning.propositionDisplay`的`eventType`通过Platform Web SDK `sendEvent`调用进行跟踪。 |
| 转化>单击元素 | 自动为基于VEC的活动进行跟踪。 显示为at.js网络调用，在请求有效负载中具有`notifications`对象且`type`值为`click`。 | 自动为基于VEC的活动进行跟踪。 显示为Platform Web SDK `sendEvent`调用，其中包含`decisioning.propositionInteract`的`eventType`。 |
| 参与>页面查看 | 已自动跟踪 | 已自动跟踪 |
| 参与>网站逗留时间 | 已自动跟踪 | 已自动跟踪 |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html?lang=zh-Hans) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## 自动跟踪的事件

以下转化目标不需要对实施进行任何具体调整：

* 转化>查看页面
* 转化>单击元素
* 参与>页面查看
* 参与>网站逗留时间

>[!NOTE]
>
>Platform Web SDK允许更好地控制请求有效负载中传递的值。 要确保Target功能(如QA URL和“查看了某个页面”转化目标正常工作，请检查`xdm.web.webPageDetails.URL`值是否包含具有正确字符大小写的完整页面URL。

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

Target实施通常使用自定义转化事件来跟踪基于表单的活动的点击次数，以指示流量中的转化，或者在不请求新内容的情况下传递参数。

下表概述了几种常见的转化跟踪用例的at.js方法和Platform Web SDK等效项。

| 用例 | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 跟踪mbox位置（范围）的点击转化事件 | 为特定mbox位置执行`trackEvent()`或值为`click`的`type`的`sendNotifications()` | 执行事件类型为`decisioning.propositionInteract`的`sendEvent`命令 |
| 跟踪可能还包含其他数据（如Target配置文件参数）的自定义转化事件 | 为特定mbox位置执行`trackEvent()`或值为`display`的`type`的`sendNotifications()` | 执行事件类型为`decisioning.propositionDisplay`的`sendEvent`命令 |

>[!NOTE]
>
>虽然`decisioning.propositionDisplay`最常用于增加特定范围的展示次数，但通常也应将它用作at.js `trackEvent()`的直接替代项。 如果未指定，`trackEvent()`函数将默认为`display`类型。 检查您的实施，确保对您可能已定义的任何自定义转化使用正确的事件类型。

有关如何使用[`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/)和[`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/)跟踪Target事件的更多信息，请参阅at.js专用文档。

at.js示例使用`trackEvent()`跟踪对mbox位置的点击：

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

通过Platform Web SDK实施，您可以通过调用`sendEvent`命令、填充`_experience.decisioning.propositions` XDM字段组并将`eventType`设置为以下两个值之一来跟踪事件和用户操作：

* `decisioning.propositionDisplay`：表示Target活动的渲染。
* `decisioning.propositionInteract`：表示用户与活动的交互，如鼠标单击。

`_experience.decisioning.propositions` XDM字段组是一个对象数组。 每个对象的属性派生自`sendEvent`命令中返回的`result.propositions`： `{ id, scope, scopeDetails }`

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

接下来，了解如何[为一致的访客配置文件启用跨域ID共享](cross-domain.md)。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=zh-Hans#M463)中发帖让我们知道。
