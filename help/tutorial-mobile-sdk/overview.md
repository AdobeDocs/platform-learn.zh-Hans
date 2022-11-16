---
title: 在移动设备应用程序中实施Adobe Experience Cloud教程概述
description: 了解如何实施Adobe Experience Cloud移动应用程序。 本教程将指导您在Swift示例应用程序中实施Experience Cloud应用程序。
recommendation: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 10%

---

# 在移动应用程序中实施 Adobe Experience Cloud 指南

了解如何用 Adobe Experience Platform 移动 SDK 在移动应用程序中实施 Adobe Experience Cloud 应用程序。

Experience PlatformMobile SDK是一个客户端SDK，它允许Adobe Experience Cloud客户通过Adobe Experience Platform边缘网络与Adobe应用程序和第三方服务进行交互。 请参阅 [Adobe Experience Platform Mobile SDK文档](https://aep-sdks.gitbook.io/docs/) 以了解更多详细信息。

![构建设置](assets/data-collection-mobile-sdk.png)


本教程将指导您在名为Luma的示例零售应用程序中完成Platform Mobile SDK的实施。 的 [Luma应用程序](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 具有一些功能，可让您构建实际可行的实施。 完成本教程后，您应该可以在自己的移动设备应用程序中开始通过Platform Mobile SDK实施所有营销解决方案。

课程专为iOS设计，并在Swift中编写，但许多概念也适用于Android™。

完成本教程后，您将能够：

* 使用标准和自定义字段组创建架构。
* 设置数据流。
* 配置移动标记属性。
* 设置Experience Platform数据集（可选）。
* 在应用程序中安装和实施标记扩展。
* 添加以下Adobe Experience Cloud应用程序/扩展：
   * [Adobe Experience Platform Edge(XDM)](events.md)
   * [生命周期数据收集](lifecycle-data.md)
   * [Adobe Analytics via XDM](analytics.md)
   * [同意](consent.md)
   * [标识](identity.md)
   * [配置文件](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [使用Journey Optimizer推送消息](journey-optimizer-push.md)
* 正确地将Experience Cloud参数传递到 [Web视图](web-views.md).
* 使用验证实施 [Adobe Experience Platform保障](assurance.md).

>[!NOTE]
>
>提供了类似的多解决方案教程 [Web SDK](../tutorial-web-sdk/overview.md).

## 先决条件

在这些课程中，我们假定您拥有 Adobe ID 和完成练习所需的权限。如果没有，则应联系Adobe管理员以请求获取访问权限。

* 在数据收集中，您必须具有：
   * **[!UICONTROL 平台]** — 权限项 **[!UICONTROL 移动设备]**
   * **[!UICONTROL 资产权限]** — 权限项 **[!UICONTROL 开发]**, **[!UICONTROL 批准]**, **[!UICONTROL 发布]**, **[!UICONTROL 管理扩展]**&#x200B;和 **[!UICONTROL 管理环境]**.
   * **[!UICONTROL 公司权限]** — 权限项 **[!UICONTROL 管理资产]** 和，如果完成了可选的推送消息课程， **[!UICONTROL 管理应用程序配置]**

      有关标记权限的更多信息，请参阅 [标记的用户权限](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=zh-Hans)产品文档中的{target=&quot;_blank&quot;}。
* 在Experience Platform中，您必须具有：
   * **[!UICONTROL 数据建模]** — 用于管理和查看架构的权限项。
   * **[!UICONTROL Identity Management]** — 用于管理和查看身份命名空间的权限项。
   * **[!UICONTROL 数据收集]** — 用于管理和查看数据流的权限项。

   * 如果您是基于平台的应用程序(如Real-time CDP、Journey Optimizer或Customer Journey Analytics)的客户，则还应该：
      * **[!UICONTROL 数据管理]** — 用于管理和查看数据集以完成操作的权限项 _可选平台练习_ （需要基于平台的应用程序的许可证）。
      * 开发 **沙盒** 您可以在本教程中使用它。
* 对于Adobe Analytics，你必须知道 **报表包** 您可以使用来完成本教程。

所有Experience Cloud客户都应有权访问部署Mobile SDK所需的功能。

此外，还假定您熟悉 [!DNL Swift]. 您无需成为专家即可完成课程，但如果您能够轻松阅读和理解代码，将可从这些课程中学到更多知识。

## 下载Luma应用程序

可以下载示例应用程序的两个版本。

1. [空](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} — 版本，不含任何Experience Cloud代码，可在本教程中完成动手操作练习
1. [已完全实施](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} — 具有完整Experience Cloud实施以供引用的版本。

让我们开始吧！


下一个： **[创建XDM架构](create-schema.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)