---
title: 利用 Web SDK 实施 Adobe Experience Cloud 教程
description: 了解如何使用 Adobe Experience Platform Web SDK 实施 Experience Cloud 应用程序。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 7%

---

# 利用 Web SDK 实施 Adobe Experience Cloud 教程

了解如何使用 Adobe Experience Platform Web SDK 实施 Experience Cloud 应用程序。

Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户通过Adobe Edge Network与Adobe Experience Platform应用程序和第三方服务进行交互。 有关更多详细信息，请参阅[Adobe Experience Platform Web SDK概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/edge/home)。

![Experience Platform Web SDK架构](assets/dc-websdk.png)

本教程将指导您在名为Luma的示例零售网站上实施Platform Web SDK。 [Luma网站](https://luma.enablementadobe.com/content/luma/us/en.html)具有丰富的数据层和功能，可让您构建现实的实施。 在本教程中，您需要：

* 使用适用于Luma网站的Platform Web SDK实施，在您自己的帐户中创建自己的标记资产。
* 为Web SDK实施（如数据流、架构和身份命名空间）配置所有数据收集功能。
* 添加以下Adobe Experience Cloud应用程序：
   * **[Adobe Experience Platform](setup-experience-platform.md)**(以及在Adobe Real-Time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics等平台上构建的应用程序)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* 实施事件转发以将Web SDK收集的数据发送到非Adobe目标。
* 使用Experience Platform Debugger和Assurance验证您自己的Platform Web SDK实施。

完成本教程后，您应该可以在自己的网站上开始通过Platform Web SDK实施所有营销应用程序！


>[!NOTE]
>
>[Mobile SDK](../tutorial-mobile-sdk/overview.md)也提供了类似的多解决方案教程。

## 先决条件

所有Experience Cloud客户都可以使用Platform Web SDK。 无需授权基于Platform的应用程序(如Real-Time Customer Data Platform或Journey Optimizer)即可使用Web SDK。

在这些课程中，我们假定您拥有Adobe帐户和完成课程所需的权限。 如果没有，则必须联系贵公司的Experience Cloud管理员以获取访问权限。

* 对于&#x200B;**数据收集**，您必须具有：
   * **[!UICONTROL 平台]** — **[!UICONTROL Web]**&#x200B;的权限，如果获得许可，还有&#x200B;**[!UICONTROL Edge]**
   * **[!UICONTROL 属性权限]** — 权限&#x200B;**[!UICONTROL 批准]**、**[!UICONTROL 开发]**、**[!UICONTROL 编辑属性]**、**[!UICONTROL 管理环境]**、**[!UICONTROL 管理扩展]**&#x200B;和&#x200B;**[!UICONTROL 发布]**，
   * **[!UICONTROL 公司权限]** — 权限&#x200B;**[!UICONTROL 管理资产]**

     有关标记权限的详细信息，请参阅[文档](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/admin/user-permissions)。

* 对于&#x200B;**Experience Platform**，您必须具有：

   * 访问&#x200B;**默认生产**，**“生产”**&#x200B;沙盒。
   * 访问&#x200B;**[!UICONTROL 数据建模]**&#x200B;下的&#x200B;**[!UICONTROL 管理架构]**&#x200B;和&#x200B;**[!UICONTROL 查看架构]**。
   * 访问&#x200B;**[!UICONTROL Identity Management]**&#x200B;下的&#x200B;**[!UICONTROL 管理身份命名空间]**&#x200B;和&#x200B;**[!UICONTROL 查看身份命名空间]**。
   * 访问&#x200B;**[!UICONTROL 数据收集]**&#x200B;下的&#x200B;**[!UICONTROL 管理数据流]**&#x200B;和&#x200B;**[!UICONTROL 查看数据流]**。
   * 如果您是某个基于平台的应用程序的客户，并且即将完成[设置Experience Platform](setup-experience-platform.md)课程，则您还应该拥有：
      * 访问&#x200B;**开发**&#x200B;沙盒。
      * **[!UICONTROL 数据管理]**&#x200B;和&#x200B;**[!UICONTROL 配置文件管理]**&#x200B;下的所有权限项：

     所需的功能应该可供所有Experience Cloud客户使用，即使您不是基于平台的应用程序(如Real-Time CDP)的客户。

     有关Platform访问控制的详细信息，请参阅[文档](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/home)。

* 对于可选&#x200B;**Adobe Analytics**&#x200B;课程，您必须拥有[对报表包设置、处理规则和Analysis Workspace的管理员访问权限](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-console/home)

* 对于可选&#x200B;**Adobe Target**&#x200B;课程，您必须具有[编辑者或审批者](https://experienceleague.adobe.com/zh-hans/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80)访问权限。

* 对于可选&#x200B;**Audience Manager**&#x200B;课程，您必须有权创建、读取和写入特征、区段和目标。 有关详细信息，请参阅有关[Audience Manager基于角色的访问控制](https://experienceleague.adobe.com/zh-hans/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control)的教程。


>[!NOTE]
>
>我们假定您熟悉HTML和JavaScript等前端开发语言。 您无需成为这些语言的专家，但如果您能够阅读和理解代码，则可充分利用本教程。

## 更新

* 2024年4月24日：主要更新，包括添加设置变量/更新变量、拆分个性化和Analytics请求、Journey Optimizer课程

## 加载Luma网站


>[!WARNING]
>
> 本教程中使用的Luma网站预计将在2026年2月16日这一周内被替换。 作为本教程的一部分完成的工作可能不适用于新网站。

在单独的浏览器选项卡中加载[Luma网站](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}，并将其加入书签，这样您就可以在教程中根据需要轻松加载该网站。 除了能够加载我们的托管生产站点外，您不需要任何其他访问Luma的权限。

[![Luma网站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

让我们开始吧！

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=zh-Hans)上分享这些内容
