---
title: 配置数据流
description: 了解如何在Experience Platform中创建数据流。
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# 创建数据流

了解如何在Experience Platform中创建数据流。

数据流是平台边缘网络上的服务器端配置。  数据流可确保将传入到平台边缘网络的数据正确路由到Adobe Experience Cloud应用程序和服务。 有关更多信息，请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 或 [视频](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=zh-Hans).

## 先决条件

要创建数据流，您的组织必须在数据收集界面(以前称为 [!UICONTROL Launch])，并且您必须拥有 [!UICONTROL Experience Platform] > [!UICONTROL 数据收集] > **[!UICONTROL 管理数据流]** 和 **[!UICONTROL 查看数据流]**.

## 学习目标

在本课程中，您将：

* 了解何时使用数据流。
* 创建数据流。
* 配置数据流。

## 创建数据流

可以在 [!UICONTROL 数据收集] 界面 [!UICONTROL 数据流] 配置工具。 要创建数据流，请执行以下操作：

1. 确保您位于正确的Platform沙盒中。
1. 选择 **[!UICONTROL 新数据流]**.

   ![数据流主页](assets/mobile-datastream-new.png)

1. 提供名称，例如 `Luma App`.
1. 选择您在上一课程中创建的架构。
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![新数据流](assets/mobile-datastream-name.png)


## 添加服务

接下来，您可以将Experience Cloud服务连接到数据流。 当Platform Mobile SDK将数据发送到边缘网络时，数据流会将数据发送到以下服务：

1. 添加 **[!UICONTROL Adobe Analytics]** 和提供报表包。

1. 启用 **[!UICONTROL Adobe Audience Manager]** （可选）。

1. 启用 **[!UICONTROL Adobe Experience Platform]** 提供 **[!UICONTROL 数据集]** （可选）。
   * 如果您尚未创建数据集，请按照相关说明操作 [此处](platform.md).

1. 最终配置应当如下所示。
   ![数据流设置](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>启用贵组织使用的每项服务，可确保在移动设备应用程序中收集的数据可以随时随地使用。 有关数据流设置的更多信息，请参阅此文档 [此处](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

在您自己的网站上实施Platform Mobile SDK时，应创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您在基于平台的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)中使用Platform Mobile SDK，则应确保在相应的Platform沙箱中创建这些数据流。

下一个： **[配置标记](configure-tags.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
