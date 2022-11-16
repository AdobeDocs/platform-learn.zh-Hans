---
title: 创建数据集
description: 创建数据集
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 创建数据集

除了描述您发送到Adobe Experience Platform的数据之外，您还需要一个位置来保留数据。 在Adobe Experience Platform中，您可以放置数据的存储段称为数据集。

>[!NOTE]
>
>如果您仅使用Platform Web SDK将数据发送到Adobe Analytics、Adobe Target和Adobe Audience Manager，或使用事件转发，则不需要数据集。 如果您仅出于这些目的使用Web SDK，则可以跳过本教程页。

1. 选择 **[!UICONTROL 数据集]** 在 [!UICONTROL 数据管理] 的左侧菜单中。
1. 接下来，选择 **[!UICONTROL 创建数据集]** 中，单击Advertising Cloud。
   ![数据集视图](../assets/datasets-view.png)

## 从架构创建数据集

1. 从 [!UICONTROL 工作流] 界面，选择第一个图块， **[!UICONTROL 从架构创建数据集]**.
1. 搜索 [您之前创建的架构](create-a-schema.md) 并选择它。
   ![模式选择](../assets/schema-selection.png)
1. 选择 **[!UICONTROL 下一个]** 和提供名称和描述。
   ![数据集名称和描述](../assets/dataset-name-description.png)
1. 选择 **[!UICONTROL 完成]**. 您的数据集已创建，可接收数据。

在您开始将数据发送到数据集时，Adobe Experience Platform会验证您尝试放入数据集的数据是否符合应用的架构。 如果数据与架构不一致，则数据将被拒绝，并且不会放入数据集中。 通过此验证步骤，数据集的消费者(Adobe产品、第三方或您自己的公司)可以对数据集数据的结构和整洁程度有一定程度的确定性。

有关创建数据集的更多信息，请参阅 [创建数据集并摄取数据](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[下一个： ](create-a-datastream.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

