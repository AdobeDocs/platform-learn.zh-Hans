---
title: 如何使用Adobe客户端数据层
description: 如何使用Adobe客户端数据层
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# 如何使用Adobe客户端数据层

In [什么是数据层？](whats-a-data-layer.md)之后，您已了解在讨论数据层时要考虑的两个部分：容器和内容。 Adobe客户端数据层是容器。 不管你怎么 [构建数据](../structuring-your-data.md) 或者您选择在数据中放入哪些信息。 数据可结构化为 [XDM](../structuring-your-data.md#xdm)，如以下示例所示，或者您可以完全构建自己的结构。

理想情况下，贵公司的工程团队负责通过页面上的代码将任何必要的数据推送到数据层中。 然后，营销团队最好使用Adobe Experience Platform Tags从数据层检索数据。

## 将数据推送到数据层

Adobe客户端数据层是一个JavaScript阵列。 创建Adobe客户端数据层时，它最初是空的：

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

要将数据放入数据层，请调用 `push` 数据层阵列上的方法：

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

您可以随时通过调用将其他数据推入数据层 `push` 再来一次。

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

如果您实施了前两个 `push` 调用时，数据层阵列中最终将有两个条目。 数据层在这种状态下并不是特别有用。 通常，您希望访问数据层的合并状态，换句话说，就是单个对象，它是您推送到Data Layer的所有数据的合并结果。 我们将在本教程的后面部分了解如何访问此合并状态。 目前，我们只要了解数据层的计算状态就足够了 `push` 调用如下：

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

有时，您必须从数据层中删除数据段。 当用户从一个视图导航到下一个视图时，这在单页应用程序中尤其常见。 例如，如果用户从产品视图导航到联系人视图，则清除Data Layer上的任何产品数据可能很有意义，因为它不再与活动视图相关。

您可以通过推送值 `undefined` ，用于您要删除的键。 基于我们之前的示例，如果您想删除 `status` 在数据层中，您的代码如下所示：

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

数据层的计算状态将不再包括 `status`：

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

Adobe客户端数据层不仅用于存储数据，还用于通信页面上发生的事件。 实际上，您通常会将数据推送到数据层 _因此_ 页面上发生的事件的ID。 这些事件包括(1)交互事件，如打开聊天机器人或在搜索栏中输入搜索词，或(2)非交互事件，如广告的展示或网页性能计算的完成。

要传达页面上发生了事件，请包含 `event` 键（推送到Data Layer的对象）。 例如，您可能希望告知用户已在搜索字段中输入搜索查询。

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

稍后，您将了解在特定事件推送到数据层时，如何在Adobe Experience Platform Tags中触发规则。 另请注意 `event` 键是 _非_ 包含在计算状态中。 它受到数据层的特殊处理。

## 将事件和数据推送到数据层

通知侦听器用户已输入搜索查询很有帮助，但如果您想提供有关事件的其他信息，该怎么办？ 例如，您可能希望包含用户的搜索查询。 您可以通过以下两种方式之一提供此数据：

1. 提供数据，以便 **被保留** 作为数据层计算状态的一部分的数据层中。
2. 提供数据，以便 **未保留** 作为数据层计算状态的一部分的数据层中。

是否要将数据保留在数据层通常取决于您是否计划在用户在页面上停留的整个过程中引用该数据。 否则，将数据保留在数据层内可能只会导致数据层混乱。

以下是一个使用额外数据推送事件的示例， **被保留** 在数据层中：

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

在此之后 `push` 发生， `siteKnowledge` 将始终显示在数据层的计算状态中，直到页面卸载为止（除非您有意删除或覆盖） `siteKnowledge`)。

相反，以下是一个使用额外数据推送事件的示例， **未保留** 在数据层中：

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

请注意本示例中的 `siteKnowledge` 包在里面 `eventInfo`. 此 `eventInfo` 密钥由数据层进行特殊处理。 它告知数据层，此数据 _应该_ 包含在发送给侦听器的事件中，但 _不应该_ 保留在数据层内。 在监听器(如Adobe Experience Platform Tags)收到有关该事件的通知后，此数据基本上会被遗忘。 此 `siteKnowledge` 键永远不会显示在数据层的计算状态中。

每次调用 `push`，Adobe客户端数据层会通知任何侦听器。 稍后，我们将了解如何从Adobe Experience Platform Tags侦听这些通知并相应地触发规则。
