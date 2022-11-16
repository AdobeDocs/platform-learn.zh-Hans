---
title: 构建数据结构
description: 构建数据结构
exl-id: 8d176389-25a4-4718-afff-efd2f87204ed
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 构建数据结构

企业有自己的语言来交流自己的领域。 汽车经销商与制造商、车型和汽缸打交道。 航空公司负责航班号、服务类别和座位分配。 其中一些术语对于特定公司是独有的，一些术语在垂直行业之间共享，而一些术语则被几乎所有企业共享。 对于在垂直行业甚至更广泛的行业中共享的术语，当您以通用方式命名和构建这些术语时，可以开始使用您的数据做一些功能强大的事情。

例如，许多企业都在处理订单。 如果这些企业共同决定以类似方式对订单进行建模，该怎么办？ 例如，如果数据模型包含一个对象，且 `priceTotal` 代表订单总价的财产？ 如果该对象也具有名为的属性，该怎么办 `currencyCode` 和 `purchaseOrderNumber`? 可能顺序对象包含名为的属性 `payments` 就是一组支付对象。 每个对象都表示订单的付款。 例如，某位客户可能用礼品卡支付了部分订单，而其余客户则使用信用卡支付。 您可以开始构建如下所示的模型：

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

如果所有处理订单的企业都决定以一种一致的方式为订单数据建模，那么神奇的事情可能会开始发生。 您可以在组织内外更顺畅地交换信息，而不是不断地解释和翻译数据（prop和evar，还有任何人？）。 机器学习可以更轻松地了解数据 _手段_ 并提供可操作的洞察。 显示相关数据的用户界面可能变得更加直观。 您的数据可以与遵循相同建模的合作伙伴和供应商无缝集成。

## XDM

这是Adobe的目标 [体验数据模型](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM为行业中常见的数据提供规范性建模，同时允许您根据特定需求扩展模型。 Adobe Experience Platform是基于XDM构建的，因此，发送到Experience Platform的数据需要位于XDM中。 在将数据发送到Experience Platform之前，请考虑如何将当前数据模型转换为XDM，而不是考虑在组织内更普遍地采用XDM，这样便很少需要进行翻译。

[下一个： ](configure-the-server/create-a-schema.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
