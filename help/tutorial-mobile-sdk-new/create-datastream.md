---
title: 配置数据流
description: 了解如何在Experience Platform中创建数据流。
feature: Mobile SDK,Datastreams
hide: true
hidefromtoc: true
source-git-commit: 45481ca81f2ee4119bc900a0dd2652818269df6b
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 6%

---

# 创建数据流

了解如何在Experience Platform中创建数据流。

数据流是Platform边缘网络上的服务器端配置。 数据流确保将传入到Platform边缘网络的数据正确路由到Adobe Experience Cloud应用程序和服务。 欲了解更多信息，请参见 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 或此 [视频](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=zh-Hans).

## 先决条件

要创建数据流，必须在数据收集界面（以前称为）中为您的组织配置此功能 [!UICONTROL Launch])并且您必须拥有的用户权限 [!UICONTROL Experience Platform] > [!UICONTROL 数据收集] > **[!UICONTROL 管理数据流]** 和 **[!UICONTROL 查看数据流]**.

## 学习目标

在本课程中，您将执行以下操作：

* 了解何时使用数据流。
* 创建数据流。
* 配置数据流.

## 创建数据流

可以在以下位置创建数据流： [!UICONTROL 数据收集] 界面使用 [!UICONTROL 数据流] 配置工具。 要创建数据流，请执行以下操作：

1. 由于数据流是在沙盒级别定义的，因此请确保您处于正确的Experience Platform沙盒中。
1. 选择 **[!UICONTROL 数据流]** 在左边栏中。
1. 选择&#x200B;**[!UICONTROL 新数据流]**。

   ![数据流主页](assets/datastream-new.png)

1. 提供 **[!UICONTROL 名称]**&#x200B;例如 `Luma Mobile App` 和 **[!UICONTROL 描述]**&#x200B;例如 `Datastream for Luma Mobile App`.
1. 从中选择您在上一课中创建的架构 **事件架构**&#x200B;列表。
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![新数据流](assets/datastream-name.png)


## 添加服务

接下来，将Experience Cloud服务连接到数据流。 当Platform Mobile SDK向Edge Network发送数据时，数据流将数据发送到这些服务：

1. 选择 **[!UICONTROL 添加服务]**。

1. 添加 **[!UICONTROL Adobe Analytics]** 从 [!UICONTROL 服务] 列表，

1. 输入要在其中使用的报表站点的名称 **[!UICONTROL 报表包ID]**.

1. 通过切换启用服务 **[!UICONTROL 已启用]** 打开。

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![将Adobe Analytics添加为数据流服务](assets/datastream-service-aa.png)

您可能还希望启用Adobe Experience Platform服务。

>[!IMPORTANT]
>
>您只能在创建事件数据集后启用Adobe Experience Platform服务。 如果尚未创建事件数据集，请按照相关说明操作 [此处](platform.md).

1. 单击 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加服务]** 以添加其他服务。

1. 从 [!UICONTROL 服务] 列表中选择 **[!UICONTROL Adobe Experience Platform]**。

1. 通过切换启用服务 **[!UICONTROL 已启用]** 打开。

1. 选择 **[!UICONTROL 事件数据集]** 您在 [创建数据集](platform.md#create-a-dataset) 指令，例如 **Luma移动应用程序事件数据集**

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![将Adobe Experience Platform添加为数据流服务](assets/datastream-service-aep.png)
1. 最终配置应如下所示。

   ![数据流设置](assets/datastream-settings.png)


>[!NOTE]
>
>启用您的组织使用的每项服务，可确保随时随地使用在移动应用程序中收集的数据。 有关数据流设置的更多信息，请参阅文档 [此处](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

在您自己的网站上实施Platform Mobile SDK时，您应该创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您将Platform Mobile SDK与基于Platform的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)一起使用，则应确保在适当的Platform沙盒中创建这些数据流。

>[!SUCCESS]
>
>您现在有了一个数据流用于本教程的其余部分。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[配置标记](configure-tags.md)**
