---
title: 构建数据
description: 构建数据
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 构建数据

企业有自己的语言来沟通自己的领域。 汽车经销商负责制造厂商、车型和汽缸。 航空公司负责航班号、服务等级和座位安排。 其中一些术语是特定公司所独有的，一些术语在垂直行业中共享，一些术语在几乎所有企业中共享。 对于在垂直行业甚至更广泛的行业中共享的术语，当您以通用方式命名和构建这些术语时，可以开始使用您的数据执行强大的操作。

例如，许多企业处理订单。 如果这些企业共同决定以类似的方式为订单建模，那该怎么办？ 例如，如果数据模型包含一个对象，且该对象具有 `priceTotal` 产指订单之总价。 如果该对象还具有命名的属性，该怎么办 `currencyCode` 和 `purchaseOrderNumber`. order对象可能包含名为的属性 `payments` 那将是一系列付款对象。 每个对象将代表订单的付款。 例如，客户可能使用礼品卡支付部分订单，而使用信用卡支付剩余部分。 您可以开始构建类似于下面的模型：

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

如果所有处理订单的企业都决定以一致的方式根据行业中常见的术语对订单数据进行建模，那么神奇的事情可能会开始发生。 信息可以在您的组织内外更流畅地交换，而不是不断地解释和翻译数据（ prop和evar ，任何人都能？ ）。 机器学习可以更轻松地了解您的数据 _方法_ 并提供可操作洞察。 用于呈现相关数据的用户界面可以变得更加直观。 您的数据可以与遵循相同建模的合作伙伴和供应商无缝集成。

## XDM

这是Adobe的目标 [体验数据模型](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM为行业中常见的数据提供规范性建模，同时允许您扩展模型以满足特定需求。 Adobe Experience Platform是围绕XDM构建的，因此，发送到Experience Platform的数据需要采用XDM格式。 您无需考虑在将数据发送到Experience Platform之前在何处以及如何将当前数据模型转换为XDM，而是考虑更普遍地在公司内部采用XDM，以便很少需要进行翻译。
