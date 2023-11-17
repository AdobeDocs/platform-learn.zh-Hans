---
title: 在移动应用程序中实施Adobe Experience Cloud教程概述
description: 了解如何实施Adobe Experience Cloud移动应用程序。 本教程将指导您在一个示例Swift应用程序中实施Experience Cloud应用程序。
recommendations: noDisplay,catalog
hide: true
exl-id: 378bdf5d-c3ce-4a4c-b188-ab9e8265627f
source-git-commit: f592fc61ad28d04eba3c1c21a0a66bda6e816a5b
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 9%

---

# 在移动应用程序中实施 Adobe Experience Cloud 指南

了解如何用 Adobe Experience Platform 移动 SDK 在移动应用程序中实施 Adobe Experience Cloud 应用程序。

Experience PlatformMobile SDK是一个客户端SDK，它允许Adobe Experience Cloud的客户通过Adobe Experience Platform Edge Network与Adobe应用程序和第三方服务进行交互。 请参阅 [Adobe Experience Platform移动SDK文档](https://developer.adobe.com/client-sdks/documentation/) 以了解更多详细信息。

![架构](assets/architecture.png)


本教程将指导您在名为Luma的示例零售应用程序中实施Platform Mobile SDK。 此 [Luma应用程序](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 具有的功能可让您构建现实的实施。 完成本教程后，您应该可以在自己的移动应用程序中开始通过Experience PlatformMobile SDK实施所有营销解决方案。

这些课程是为iOS设计的，使用Swift/SwiftUI编写，但许多概念也适用于Android™。

完成本教程后，您将能够：

* 使用标准和自定义字段组创建架构。
* 设置数据流.
* 配置移动标记属性。
* 设置Experience Platform数据集（可选）。
* 在应用程序中安装并实施标记扩展。
* 将Experience Cloud参数正确传递给 [webview](web-views.md).
* 使用验证实施 [Adobe Experience Platform Assurance](assurance.md).
* 添加以下Adobe Experience Cloud应用程序/扩展：
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [生命周期数据收集](lifecycle-data.md)
   * [同意](consent.md)
   * [标识](identity.md)
   * [配置文件](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Adobe Experience Platform](platform.md)
   * [使用Journey Optimizer推送消息](journey-optimizer-push.md)
   * [Journey Optimizer的应用程序内消息传递](journey-optimizer-inapp.md)
   * [Journey Optimizer的优惠](journey-optimizer-offers.md)
   * [使用Target进行A/B测试](target.md)


>[!NOTE]
>
>类似的多解决方案教程可用于 [Web SDK](../tutorial-web-sdk/overview.md).

## 先决条件

在这些课程中，我们假定您拥有 Adobe ID 和完成练习所需的权限。如果没有，您应该联系Adobe管理员以请求获取访问权限。

* 在数据收集中，您必须具有：
   * **[!UICONTROL 平台]** — 权限项 **[!UICONTROL 移动设备]**
   * **[!UICONTROL 资产权限]** — 权限项至 **[!UICONTROL 开发]**， **[!UICONTROL 批准]**， **[!UICONTROL Publish]**， **[!UICONTROL 管理扩展]**、和 **[!UICONTROL 管理环境]**.
   * **[!UICONTROL 公司权限]** — 权限项至 **[!UICONTROL 管理资产]** 此外，如果您已完成可选的推送消息课程， **[!UICONTROL 管理应用程序配置]**

     有关标记权限的更多信息，请参阅 [标记的用户权限](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=zh-Hans){target="_blank"} 在产品文档中。
* 在Experience Platform中，您必须具有：
   * **[!UICONTROL 数据建模]** — 用于管理和查看架构的权限项。
   * **[!UICONTROL Identity Management]** — 用于管理和查看身份命名空间的权限项。
   * **[!UICONTROL 数据收集]** — 用于管理和查看数据流的权限项。

   * 如果您是基于Platform的应用程序(如Real-Time CDP、Journey Optimizer或Customer Journey Analytics)的客户，则还应：
      * **[!UICONTROL 数据管理]** — 用于管理和查看数据集以完成 _可选平台练习_ （需要基于平台的应用程序的许可证）。
      * 开发 **沙盒** 供本教程使用。

* 对于Adobe Analytics，您必须知道是哪个 **报表包** 您可以使用完成本教程。

* 对于Adobe Target，您必须具有正确配置的权限 **角色**， **工作区**、和 **属性** 如所述 [此处](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=zh-Hans).

* 对于Adobe Journey Optimizer，您必须具有足够的权限才能配置 **推送通知服务** 并创建 **应用程序表面**， a **历程**， a **message** 和 **消息预设**. 对于决策管理，您需要拥有 **管理优惠** 和 **决策** 如所述 [此处](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

所有Experience Cloud客户都应有权访问部署Mobile SDK所需的功能。


>[!NOTE]
>
>在本教程中，您将创建架构、数据集、身份等。 如果您正在学习本教程，将多个人员放在一个沙盒上，或者您使用的是共享帐户，请考虑在创建这些对象时附加或附加标识作为命名约定的一部分。 例如，添加 ` - <your name or initials>` 到指示您创建的对象的名称。


## 下载Luma应用程序

示例应用程序有两个版本可供下载。 这两个版本都可以下载/克隆 [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). 您将找到两个文件夹：


1. [开始](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}：对于大多数Experience PlatformMobile SDK代码，您都需要使用此类项目来完成本教程中的动手练习，但该项目没有代码，也没有占位符代码。
1. [完成](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}：具有完整实施的版本以供参考。

>[!NOTE]
>
>您将使用iOS作为平台， [!DNL Swift] 作为编程语言， [!DNL SwiftUI] 作为UI框架和 [!DNL Xcode] 作为集成开发环境(IDE)。 但是，解释的许多实施概念与其他开发平台类似。 而且许多公司已经成功完成了本教程，以前在iOS/Swift(UI)上几乎没有任何体验。 您无需成为专家即可完成课程，但如果您能够轻松阅读和理解代码，将可从课程中学到更多知识。


让我们开始吧！

>[!SUCCESS]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[创建XDM架构](create-schema.md)**
