---
title: 配置数据流
description: 了解如何启用数据流并配置Experience Cloud解决方案。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Web SDK,Datastreams
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: d81e7df36807778967bc0350735aec008fb1a55e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---

# 配置数据流

了解如何启用数据流并配置Experience Cloud应用程序。

数据流会告知Adobe Experience PlatformEdge Network将通过Platform Web SDK收集的数据发送到何处。 在数据流配置中，您可以启用Experience Cloud应用程序、Experience Platform帐户和事件转发。 请参阅 [配置数据流的基础知识](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=zh-Hans) 以了解更多详细信息。


![Web SDK、数据流和Edge Network图](assets/dc-websdk-datastreams.png)

## 学习目标

在本课程结束后，您将能够：

* 创建数据流
* 数据流覆盖入门

## 先决条件

在配置数据流之前，您必须已完成以下课程：

* [配置架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)

## 创建数据流

现在，您可以创建一个数据流来告知PlatformEdge Network将Web SDK收集的数据发送到何处。

**要创建数据流，请执行以下操作：**

1. 打开 [数据收集界面](https://launch.adobe.com/){target="_blank"}
1. 确保您在正确的沙盒中

   >[!NOTE]
   >
   >如果您是基于Platform的应用程序(如Real-Time CDP或Journey Optimizer)的客户，我们建议您在本教程中使用开发沙盒。 如果不是，请使用 **[!UICONTROL Prod]** 沙盒。

1. 转到 **[!UICONTROL 数据流]** 在左侧导航中
1. 选择 **[!UICONTROL 新建数据流]** 在屏幕的右侧。
1. 输入 `Luma Web SDK: Development Environment` 作为 **[!UICONTROL 名称]**. 当您稍后在标记属性中配置Web SDK扩展时，将会引用此名称。
1. 选择您的 `Luma Web Event Data` 作为 **[!UICONTROL 事件架构]**
1. 选择 **[!UICONTROL 保存]**

   ![创建数据流](assets/datastream-create-new-datastream.png)

在下一个屏幕上，您可以向数据流添加Adobe应用程序等服务，但此时您不会在本教程中添加任何服务。 您将在后面的课程中这样做 [设置Experience Platform](setup-experience-platform.md)， [设置Analytics](setup-analytics.md)， [设置Audience Manager](setup-audience-manager.md)， [设置目标](setup-target.md)，或 [事件转发](setup-event-forwarding.md).

>[!NOTE]
>
>在您自己的网站上实施Platform Web SDK时，您应该创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您将Platform Web SDK与基于Platform的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)一起使用，则应确保在适当的Platform沙盒中创建这些数据流。

## 覆盖数据流

数据流覆盖允许您为数据流定义其他配置，然后在实施的某些条件下覆盖默认配置。


数据流配置覆盖分为两步：

1. 首先，在数据流配置中定义数据流覆盖。 必须为每个要覆盖的Adobe应用程序执行此操作。
1. 然后，您可以通过Web SDK Send Event Action或Web SDK标记扩展中的配置将覆盖发送到Edge Network。

在 [设置Adobe Analytics](setup-analytics.md) 课程可使用Platform Web SDK发送事件操作覆盖页面的报表包。

请参阅 [数据流配置覆盖文档](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overrides.html?lang=en) 以获取有关如何覆盖数据流配置的详细说明。

现在，您可以在标记资产中安装Platform Web SDK扩展了！

[下一步： ](install-web-sdk.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
