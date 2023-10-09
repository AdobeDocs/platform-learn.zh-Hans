---
title: 配置数据流
description: 了解如何在Experience Platform中创建数据流。
feature: Mobile SDK,Datastreams
hide: true
exl-id: d8b9df3d-49ee-4578-92c6-0f920a86fe7e
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# 创建数据流

了解如何在Experience Platform中创建数据流。

数据流是Platform边缘网络上的服务器端配置。 数据流确保将传入到Platform边缘网络的数据正确路由到Adobe Experience Cloud应用程序和服务。 欲了解更多信息，请参见 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 或此 [视频](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=zh-Hans).

![架构](assets/architecture.png)

## 先决条件

要创建数据流，必须在数据收集界面（以前称为）中为您的组织配置此功能 [!UICONTROL Launch])，并且您必须具有管理和查看数据流的用户权限。

## 学习目标

在本课程中，您将执行以下操作：

* 了解何时使用数据流。
* 创建数据流。
* 配置数据流.

## 创建数据流

可以在以下位置创建数据流： [!UICONTROL 数据收集] 界面使用 [!UICONTROL 数据流] 配置工具。 要创建数据流，请执行以下操作：

1. 当数据流在沙盒级别定义时，请确保您处于正确的Experience Platform沙盒中。
1. 选择 **[!UICONTROL 数据流]** 在左边栏中。
1. 选择&#x200B;**[!UICONTROL 新数据流]**。

   ![数据流主页](assets/datastream-new.png)

1. 提供 **[!UICONTROL 名称]**&#x200B;例如 `Luma Mobile App` 和 **[!UICONTROL 描述]**&#x200B;例如 `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >最后提醒：如果您正在阅读本教程，将多人放在一个沙盒上，或者您使用的是共享帐户，请考虑在命名约定中附加或附加标识作为命名约定的一部分。 例如，使用 `Luma Mobile App Event Dataset - Joe Smith`，而不是 `Luma Mobile App Event Dataset`。另请参阅中的注释 [概述](overview.md).

1. 从中选择您在上一课中创建的架构 **事件架构** 列表。
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![新数据流](assets/datastream-name.png)


## 添加服务

当您查看（可选）时 [分析](analytics.md) 和 [Experience Platform](platform.md) 在本教程的课程中，您将向数据流添加服务，以确保当Platform Mobile SDK将数据发送到Edge Network时，数据流会将该数据转发到配置的服务。

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>启用您的组织使用的每项服务，可确保随时随地使用在移动应用程序中收集的数据。 有关数据流设置的更多信息，请参阅文档 [此处](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

在您自己的应用程序中实施Platform Mobile SDK时，您最终应创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您将Platform Mobile SDK与基于Platform的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)结合使用，则应确保在相应的沙盒中创建这些数据流。

>[!SUCCESS]
>
>您现在有了一个数据流用于本教程的其余部分。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[配置标记属性](configure-tags.md)**
