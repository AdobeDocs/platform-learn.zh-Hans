---
title: 创建架构
description: 创建架构
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# 创建架构

如 [构建数据结构](../structuring-your-data.md)，则发送到Adobe Experience Platform的数据必须位于XDM中。 更具体地说，您的数据必须与 _模式_. 模式基本上是数据外观的描述。 它描述字段的名称以及这些字段在数据中的位置。 它还描述每个字段应具有的值类型（例如，布尔值、长度为12个字符的字符串、数字数组）。

Adobe Experience Platform提供了一些称为字段组的现成构建基块，这些字段组在行业中很常见。 例如，对于金融服务业，有用于余额转移和贷款申请的现场组。 旅游和酒店业设有航班和住宿预订的现场小组。

我们建议您在创建架构时尽可能使用内置字段组。 我们还了解您可能需要特定于您自己公司的字段。 因此，您可以创建自己的自定义字段组，以便在创建的架构中使用。

让我们逐步了解如何为典型的电子商务网站创建模式。

首先，导航到 [!UICONTROL 模式] 查看Adobe Experience Platform。

![架构视图](../../../assets/implementation-strategy/schemas-view.png)

选择 [!UICONTROL 创建架构] 中。 随即会显示菜单。 选择 [!UICONTROL XDM ExperienceEvent].

此时，应会显示一个对话框，询问您要将哪些字段组添加到架构中。 您应选择的第一个字段组是名为 [!UICONTROL AEP Web SDK ExperienceEvent]. 此字段组会添加一组字段，其中包含由Adobe Experience Platform Web SDK自动收集的数据。

![AEP Web SDK mixin](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

由于本教程的网站是电子商务网站，因此您还应当选择 [!UICONTROL 商务详细信息] 字段组。 此群组允许您发送典型的商务数据，如查看、添加到购物车和购买的产品。

![商务详细信息混合](../../../assets/implementation-strategy/commerce-details-mixin.png)

单击 [!UICONTROL 添加字段组] 按钮。 此时，您应会看到架构的结构。

![包含混合的架构](../../../assets/implementation-strategy/schema-with-mixins.png)

您添加的字段组列在左侧。 选择字段组会突出显示该字段组提供的右侧字段。 花些时间探索可用的领域。

最后，选择 [!UICONTROL 无标题架构] 在屏幕左侧，提供屏幕右侧的名称和描述，然后单击 [!UICONTROL 保存].

![具有名称和描述的架构](../../../assets/implementation-strategy/schema-name-description.png)

您的架构已创建。 接下来，让我们了解如何创建数据集以保存您的数据。

有关创建模式的更多信息，请参阅 [创建架构(UI)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=zh-Hans).
