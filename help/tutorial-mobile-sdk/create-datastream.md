---
title: 配置数据流
description: 了解如何在Experience Platform中创建数据流。
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 4%

---

# 创建数据流

了解如何在Experience Platform中创建数据流。

>[!INFO]
>
> 2023年11月下旬，本教程将替换为使用新示例移动应用程序的新教程

数据流是Platform边缘网络上的服务器端配置。  数据流确保将传入到Platform边缘网络的数据正确路由到Adobe Experience Cloud应用程序和服务。 欲了解更多信息，请参见 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 或此 [视频](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=zh-Hans).

## 先决条件

要创建数据流，必须在数据收集界面（以前称为）中为您的组织配置此功能 [!UICONTROL Launch])并且您必须拥有的用户权限 [!UICONTROL Experience Platform] > [!UICONTROL 数据收集] > **[!UICONTROL 管理数据流]** 和 **[!UICONTROL 查看数据流]**.

## 学习目标

在本课程中，您将执行以下操作：

* 了解何时使用数据流。
* 创建数据流。
* 配置数据流.

## 创建数据流

可以在以下位置创建数据流： [!UICONTROL 数据收集] 界面使用 [!UICONTROL 数据流] 配置工具。 要创建数据流，请执行以下操作：

1. 确保您在正确的Platform沙盒中。
1. 选择&#x200B;**[!UICONTROL 新数据流]**。

   ![数据流主页](assets/mobile-datastream-new.png)

1. 提供名称，例如 `Luma App`.
1. 选择您在上一课中创建的架构。
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![新数据流](assets/mobile-datastream-name.png)


## 添加服务

接下来，您可以将Experience Cloud服务连接到数据流。 当Platform Mobile SDK将数据发送到Edge Network时，数据流会将数据发送到这些服务：

1. 添加 **[!UICONTROL Adobe Analytics]** 并提供报表包。

1. 启用 **[!UICONTROL Adobe Audience Manager]** （可选）。

1. 启用 **[!UICONTROL Adobe Experience Platform]** 并提供 **[!UICONTROL 数据集]** （可选）。
   * 如果您尚未创建数据集，请按照相关说明操作 [此处](platform.md).

1. 最终配置应如下所示。
   ![数据流设置](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>启用您的组织使用的每项服务，可确保随时随地使用在移动应用程序中收集的数据。 查找有关数据流设置的更多信息，请查看文档 [此处](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

在您自己的网站上实施Platform Mobile SDK时，您应该创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您将Platform Mobile SDK与基于Platform的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)一起使用，则应确保在适当的Platform沙盒中创建这些数据流。

下一步： **[配置标记](configure-tags.md)**

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
