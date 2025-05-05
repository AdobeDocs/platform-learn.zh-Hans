---
title: 为Platform Mobile SDK实施配置数据流
description: 了解如何在 Experience Platform 中创建数据流。
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 5%

---

# 创建数据流

了解如何在 Experience Platform 中创建数据流。

数据流是平台Edge Network上的服务器端配置。 数据流确保将传入到PlatformEdge Network的数据正确路由到Adobe Experience Cloud应用程序和服务。 有关详细信息，请参阅[文档](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hans)或此[视频](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=zh-Hans)。

![架构](assets/architecture.png)

## 先决条件

要创建数据流，必须在数据收集界面（以前为[!UICONTROL Launch]）中为您的组织配置此功能，并且您必须具有用户权限管理和查看数据流。

## 学习目标

在本课程中，您将执行以下操作：

* 了解何时使用数据流。
* 创建数据流。
* 配置数据流。

## 创建数据流

可以使用[!UICONTROL 数据流]配置工具在[!UICONTROL 数据收集]界面中创建数据流。 要创建数据流，请执行以下操作：

1. 当数据流在沙盒级别定义时，请确保您处于正确的Experience Platform沙盒中。
1. 在左边栏中选择&#x200B;**[!UICONTROL 数据流]**。
1. 选择&#x200B;**[!UICONTROL 新数据流]**。

   ![数据流主页](assets/datastream-new.png)

1. 提供&#x200B;**[!UICONTROL Name]**，例如`Luma Mobile App`和&#x200B;**[!UICONTROL Description]**，例如`Datastream for Luma Mobile App`。

   >[!NOTE]
   >
   >最后提醒：如果您正在阅读本教程，将多人放在一个沙盒上，或者您使用的是共享帐户，请考虑在命名约定中附加或附加标识作为命名约定的一部分。 例如，使用`Luma Mobile App Event Dataset - Joe Smith`而不是`Luma Mobile App Event Dataset`。 另请参阅[概述](overview.md)中的注释。

1. 从&#x200B;**事件架构**&#x200B;列表中选择您在上一课中创建的架构。
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![新数据流](assets/datastream-name.png)


## 添加服务

完成本教程中的（可选） [Analytics](analytics.md)和[Experience Platform](platform.md)课程后，您可将服务添加到数据流，以便将发送到PlatformEdge Network的数据转发到这些应用程序。

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
>启用您的组织使用的每项服务，可确保随时随地使用在移动应用程序中收集的数据。 有关数据流设置的详细信息，请在[此处](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hans)查看文档。

在您自己的应用程序中实施Platform Mobile SDK时，您最终应创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您将Platform Mobile SDK与基于Platform的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)结合使用，则应确保在相应的沙盒中创建这些数据流。

>[!SUCCESS]
>
>您现在有了一个数据流用于本教程的其余部分。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有任何疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享这些内容

下一步： **[配置标记属性](configure-tags.md)**
