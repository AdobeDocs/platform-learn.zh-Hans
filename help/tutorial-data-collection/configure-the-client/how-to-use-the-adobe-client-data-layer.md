---
title: 如何使用Adobe客户端数据层
description: 如何使用Adobe客户端数据层
exl-id: b5af9e72-aa6c-4cd7-80dd-b2de762a7523
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# 如何使用Adobe客户端数据层

在 [什么是数据层？](whats-a-data-layer.md)，您了解到讨论数据层时需要考虑两个部分：容器和内容。 的 [Adobe客户端数据层](https://github.com/adobe/adobe-client-data-layer) 是容器。 不管你怎么 [构建数据](../structuring-your-data.md) 或选择将哪些信息放入数据中。 数据可以按 [XDM](../structuring-your-data.md#xdm)，如以下示例所示，或者您可以完全构建自己的结构。

理想情况下，贵公司的工程团队负责通过页面代码将任何必要的数据推送到数据层。 然后，营销团队从数据层检索数据，最好使用Adobe Experience Platform（以前称为Launch）的“标记”功能。

## 将数据推送到数据层

Adobe客户端数据层是一个JavaScript数组。 在创建Adobe客户端数据层时，该数据层开始为空：

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

要将数据放入数据层，请调用 `push` 数据层数组上的方法：

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

您可以随时通过调用 `push` 再次。

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## 理解推送数据

如果您实施了前两个 `push` 调用，则最终会在数据层数组中包含两个条目。 数据层在此状态下没有用处。 通常，您会希望访问数据层的合并状态，或者，换句话说，您希望访问一个对象，该对象是您推送到数据层的所有数据的合并结果。 您将在本教程的后面部分了解如何访问此合并状态。 目前，只需了解下面两个数据层之后数据层的计算状态即可 `push` 调用如下所示：

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## 删除数据

有时，您必须从数据层中删除数据段。 当用户从一个视图导航到下一个视图时，单页应用程序中通常会出现这种情况。 例如，如果用户从产品视图导航到联系视图，则可能适合清除数据层上的任何产品数据，因为它不再与活动视图相关。

您可以通过推送 `undefined` 要删除的密钥。 根据我们前面的示例，如果要删除 `status` 在数据层中，您的代码如下所示：

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

数据层的计算状态将不再包括 `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## 将事件推送到数据层

Adobe客户端数据层不仅用于存储数据，还用于通信页面上发生的事件。 事实上，您通常会将数据推送到数据层 _结果_ 页面中发生的事件。 这些事件包括(1)交互事件，例如打开聊天机器人或在搜索栏中键入搜索词或(2)非交互事件，例如广告的展示或网页性能计算的完成。

要告知页面上已发生事件，请包括 `event` 键值。 例如，您可能希望告知用户已在搜索字段中输入了搜索查询。

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

<!--Later, you'll learn how to trigger rules within Adobe Experience Platform Tags when a particular event is pushed to the data layer.--> Also note that the `event` key is not included in the computed state. It receives special treatment by the data layer.


## 将事件和数据推送到数据层

通知侦听器用户已输入搜索查询很有帮助，但是如果您希望提供有关该事件的其他信息，该怎么办？ 例如，您可能希望包含用户的搜索查询。 您可以通过以下两种方式之一提供此数据：

1. 提供数据以便 **保留** 在数据层中作为数据层计算状态的一部分。
1. 提供数据以便 **未保留** 在数据层中作为数据层计算状态的一部分。

是否要在数据层中保留数据通常取决于您是否计划在用户在页面上的整个访问期间引用该数据。 如果没有，则在数据层内保留数据会导致数据层混乱。

以下是推送事件的示例，该事件包含 **保留** 在数据层中：

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

之后 `push` 发生， `siteKnowledge` 将始终以数据层的计算状态显示，直到页面卸载为止（除非您有意删除或覆盖） `siteKnowledge`)。

相反，以下是使用附加数据推送事件的示例，该示例 **未保留** 在数据层中：

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

请注意，在此示例中， `siteKnowledge` 包裹在内 `eventInfo`. 的 `eventInfo` 密钥由数据层接收特殊处理。 它告知数据层此数据 _show_ 包含在发送到侦听器的事件中，但 _不应_ 保留在数据层内。 当收到有关该事件的通知监听器（如标签管理器）后，会忘记此数据。 的 `siteKnowledge` 键值永远不会显示在数据层的计算状态中。

每次您调用 `push`,Adobe客户端数据层会通知任何侦听器。 稍后，您将学习如何监听这些通知 <!--from Adobe Experience Platform Tags--> 并相应地触发规则。

[下一个： ](implement-product-page-data-layer.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
