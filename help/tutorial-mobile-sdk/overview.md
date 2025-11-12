---
title: 在移动应用程序中实施Adobe Experience Cloud教程
description: 了解如何实施Adobe Experience Cloud移动应用程序。 本教程将指导您在一个Swift或Android示例应用程序中实施Experience Cloud应用程序。
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 342bb7efbe868622c4bc08e02568bce948fed61c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 1%

---

# 在移动应用程序中实施Adobe Experience Cloud教程

了解如何使用Adobe Experience Platform Mobile SDK在移动应用程序中实施Adobe Experience Cloud应用程序。

Experience Platform Mobile SDK是客户端SDK，它允许Adobe Experience Cloud的客户通过Adobe Edge Network与Adobe Experience Platform应用程序和第三方服务进行交互。 有关更多详细信息，请参阅[Adobe Experience Platform Mobile SDK文档](https://developer.adobe.com/client-sdks/home/)。

![架构](assets/architecture.png){zoomable="yes"}


本教程将指导您在名为Luma的示例应用程序中完成Platform Mobile SDK的实施。 Luma应用程序具有的功能可让您构建现实的实施。 完成本教程后，您应该可以在自己的移动应用程序中开始通过Experience Platform Mobile SDK实施所有营销解决方案。

这些课程专门针对：

* iOS，使用Swift编程语言和SwiftUI框架。
* Android，使用Kotlin和Java编程语言以及JetPack Compose框架。

完成本教程后，您将能够：

* 使用标准和自定义字段组创建架构。
* 设置数据流。
* 配置移动标记属性。
* 设置Experience Platform数据集（可选）。
* 在应用程序中安装并实施标记扩展。
* 将Experience Cloud参数正确传递给[webview](web-views.md)。
* 使用[Adobe Experience Platform Assurance](assurance.md)验证实施。
* 添加以下Adobe Experience Cloud应用程序或扩展：
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [生命周期数据收集](lifecycle-data.md)
   * [同意](consent.md)
   * [身份标识](identity.md)
   * [轮廓](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [使用Journey Optimizer推送消息](journey-optimizer-push.md)
   * [Journey Optimizer的应用程序内消息传递](journey-optimizer-inapp.md)
   * [Journey Optimizer的决策管理](journey-optimizer-offers.md)
   * [目标](target.md)


>[!NOTE]
>
>[Web SDK](../tutorial-web-sdk/overview.md)也提供了类似的多解决方案教程。

## 权限

在这些课程中，我们假定您拥有Adobe ID以及完成练习所需的用户级别权限。 如果没有，您应该联系Adobe管理员以请求获取访问权限。

* 在数据收集中，您必须具有：
   * **[!UICONTROL 平台]** — 权限项&#x200B;**[!UICONTROL 移动设备]**
   * **[!UICONTROL 属性权限]** — 用于&#x200B;**[!UICONTROL 开发]**、**[!UICONTROL 批准]**、**[!UICONTROL 发布]**、**[!UICONTROL 管理扩展]**&#x200B;和&#x200B;**[!UICONTROL 管理环境]**&#x200B;的权限项。
   * **[!UICONTROL 公司权限]** — 用于&#x200B;**[!UICONTROL 管理属性]**&#x200B;的权限项

     有关标记权限的详细信息，请参阅产品文档中的标记[用户权限](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/admin/user-permissions){target="_blank"}。
* 在Experience Platform中，您必须具有：
   * **[!UICONTROL 数据建模]** — 用于管理和查看架构的权限项。
   * **[!UICONTROL Identity Management]** — 管理和查看身份命名空间的权限项。
   * **[!UICONTROL 数据收集]** — 用于管理和查看数据流的权限项。

   * 如果您是基于Platform的应用程序(如Real-Time CDP、Journey Optimizer或Customer Journey Analytics)的客户，并计划参加相关课程，您还应参加：
      * **[!UICONTROL 数据管理]** — 用于管理和查看数据集的权限项。
      * 可用于本教程的开发&#x200B;**沙盒**。

   * 对于Journey Optimizer课程，您需要权限来配置&#x200B;**推送通知服务**&#x200B;并创建&#x200B;**应用程序表面**、**历程**、**消息**&#x200B;和&#x200B;**消息预设**。 此外，对于决策管理，您需要具有适当的权限来&#x200B;**管理优惠**&#x200B;和&#x200B;**决策**，如[权限级别](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/access-control/high-low-permissions)中所述。

* 对于Adobe Analytics，您必须知道可以使用哪些&#x200B;**报表包**&#x200B;来完成本教程。

* 对于Adobe Target，您必须具有创建和激活活动的权限。


>[!NOTE]
>
>在本教程中，您可以创建架构、数据集、身份等。 如果多个用户在一个沙盒中学习本教程，请考虑在创建这些对象时附加或附加标识作为命名约定的一部分。 例如，将` - <your name or initials>`添加到指示您创建的对象的名称。

## 版本历史记录

* 2025年9月9日：
   * 应用程序的Android版本及随附说明。
   * 更新了Journey Optimizer中应用程序表面和促销活动功能的变更。
* 2023年11月29日：通过新的示例应用程序以及应用程序内消息传送、决策管理和Adobe Target的新课程进行重大修改。
* 2022年3月9日：首次发布

## 下载Luma应用程序

>[!BEGINTABS]

>[!TAB iOS]

示例应用程序有两个版本可供下载。 两个版本均可从[GitHub](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App)下载/克隆。 您找到两个文件夹：

1. [开始](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}：对于您完成本教程中的动手练习所需使用的大多数Experience Platform Mobile SDK代码，项目没有代码或带有占位符代码。
1. [完成](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}：具有完整实现的版本以供参考。

您将iOS用作平台，[!DNL Swift]用作编程语言，[!DNL SwiftUI]用作用户界面框架，[!DNL Xcode]用作集成开发环境(IDE)。 但是，解释的许多实施概念与其他开发平台类似。 许多公司已经成功完成了本教程，之前的iOS和Swift(UI)开发经验很少甚至没有。 您无需成为专家即可完成课程，但如果您能够轻松阅读和理解代码，将可从课程中学到更多知识。

您可以从App Store下载应用程序的最终产品化版本。

[![下载](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)

>[!TAB Android]

示例应用程序有两个版本可供下载。 这两个版本均可从[GitHub](https://github.com/adobe/Luma-Android)下载或克隆。 您找到两个文件夹：

1. [开始](https://github.com/adobe/Luma-Android){target="_blank"}：对于您完成本教程中的动手练习所需使用的大多数Experience Platform Mobile SDK代码，项目没有代码或带有占位符代码。
1. [完成](https://github.com/adobe/Luma-Android){target="_blank"}：具有完整实现的版本以供参考。

您将Android用作平台，[!DNL Kotlin]+[!DNL Java]用作编程语言，[!DNL JetPack Compose]用作用户界面框架，[!DNL Android Studio]用作集成开发环境(IDE)。 但是，解释的许多实施概念与其他开发平台类似。 许多人已经成功完成了本教程，之前的Android / Kotlin+Java / JetPack撰写体验很少，甚至没有。 您无需成为专家即可完成课程，但如果您能够轻松阅读和理解代码，将可从课程中学到更多知识。

如果您愿意，可以[加入Google Play中应用程序的产品化版本](https://play.google.com/apps/internaltest/4700642199234438150)的测试。


>[!ENDTABS]

让我们开始吧！

>[!SUCCESS]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有任何疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享这些内容。

下一步： **[创建XDM架构](create-schema.md)**
