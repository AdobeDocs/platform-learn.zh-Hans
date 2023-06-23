---
title: 创建数据集
description: 创建数据集
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# 创建数据集

除了描述您将发送到Adobe Experience Platform的数据之外，您还需要一个位置来保留数据。 在Adobe Experience Platform中，您可以放置数据的这些存储段称为数据集。

要创建数据集，请导航到 [!UICONTROL 数据集] 在Adobe Experience Platform中查看。

![数据集视图](../../../assets/implementation-strategy/datasets-view.png)

单击 [!UICONTROL 创建数据集] 在右上角。

在数据集创建过程中，选择 [!UICONTROL 从架构创建数据集] 并选择 [您之前创建的架构](create-a-schema.md).

![架构选择](../../../assets/implementation-strategy/schema-selection.png)

单击 [!UICONTROL 下一个] 并提供名称和描述。

![数据集名称和描述](../../../assets/implementation-strategy/dataset-name-description.png)

单击[!UICONTROL 完成]。您的数据集已创建，可以接收数据。

当您开始将数据发送到数据集时，Adobe Experience Platform将验证您尝试放入数据集的数据是否符合所应用的架构。 如果数据不符合架构，则数据会遭到拒绝，并且不会被放入数据集中。 作为此验证步骤的结果，数据集消费者(Adobe产品、第三方或您自己的公司)对于数据集数据的结构和干净度有一定程度的确定。

有关创建数据集的更多信息，请参阅 [数据集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh-Hans).
