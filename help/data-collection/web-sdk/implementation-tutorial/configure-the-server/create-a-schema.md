---
title: 创建架构
description: 创建架构
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# 创建架构

如中所述 [构建数据](../structuring-your-data.md)，发送到Adobe Experience Platform的数据必须为XDM格式。 更具体地说，您的数据必须匹配 _架构_. 架构基本上是对数据外观的描述。 它描述了字段的名称以及它们在数据中的位置。 它还描述了每个字段应具有的值类型（例如，布尔值、长度为12个字符的字符串、数字数组）。

Adobe Experience Platform提供了一些业内常见的现成构建基块，称为字段组。 例如，对于金融服务行业，有用于余额转账和贷款申请的现场小组。 对于旅游和酒店业，有航班和住宿预订的现场小组。

在创建架构时，我们建议您尽可能使用内置字段组。 我们还了解您可能需要特定于您自己公司的字段。 因此，您可以创建自己的自定义字段组，以便在创建的架构中使用。

让我们逐步了解如何为典型的电子商务网站创建架构。

首先，导航到 [!UICONTROL 架构] 在Adobe Experience Platform中查看。

![架构视图](../../../assets/implementation-strategy/schemas-view.png)

选择 [!UICONTROL 创建架构] 在右上角。 此时将显示一个菜单。 选择 [!UICONTROL XDM ExperienceEvent].

此时，将显示一个对话框，询问您要将哪些字段组添加到架构中。 应选择的第一个字段组是名为的字段组 [!UICONTROL AEP Web SDK ExperienceEvent]. 此字段组添加了一组字段，这些字段包含由Adobe Experience Platform Web SDK自动收集的数据。

![AEP Web SDK mixin](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

由于本教程的网站是一个电子商务网站，因此您还应选择 [!UICONTROL 商业详细信息] 字段组。 此组允许您发送典型的商业数据，如正在查看、添加到购物车和购买的产品。

![商业详细信息mixin](../../../assets/implementation-strategy/commerce-details-mixin.png)

单击 [!UICONTROL 添加字段组] 按钮进行调试。 此时，您应该会看到架构的结构。

![带有Mixin的架构](../../../assets/implementation-strategy/schema-with-mixins.png)

左侧列出了您添加的字段组。 选择字段组会突出显示由该字段组提供的右侧字段。 请花些时间探索可用的字段。

最后，选择 [!UICONTROL 无标题架构] 在屏幕左侧，在屏幕右侧提供名称和描述，然后单击 [!UICONTROL 保存].

![具有名称和说明的架构](../../../assets/implementation-strategy/schema-name-description.png)

已创建您的架构。 接下来，让我们了解如何创建数据集以保存您的数据。

有关创建架构的详细信息，请参见 [创建架构(UI)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=zh-Hans).
