---
title: “利用 Web SDK 实施 Adobe Experience Cloud”教程
description: 了解如何使用Adobe Experience Platform Web SDK实施Experience Cloud应用程序。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 4%

---

# “利用 Web SDK 实施 Adobe Experience Cloud”教程

了解如何使用Adobe Experience Platform Web SDK实施Experience Cloud应用程序。

Experience PlatformWeb SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户通过Adobe Experience PlatformEdge Network与Adobe应用程序和第三方服务进行交互。 请参阅 [Adobe Experience Platform Web SDK概述](https://experienceleague.adobe.com/en/docs/experience-platform/edge/home) 以了解更多详细信息。

![Experience PlatformWeb SDK架构](assets/dc-websdk.png)

本教程将指导您在名为Luma的示例零售网站上实施Platform Web SDK。 此 [Luma网站](https://luma.enablementadobe.com/content/luma/us/en.html) 具有丰富的数据层和功能，可让您构建现实的实施。 在本教程中，您需要：

* 使用适用于Luma网站的Platform Web SDK实施，在您自己的帐户中创建自己的标记资产。
* 为Web SDK实施配置所有数据收集功能，例如数据流、架构和身份命名空间。
* 添加以下Adobe Experience Cloud应用程序：
   * **[Adobe Experience Platform](setup-experience-platform.md)** (以及基于Platform构建的应用程序，例如Adobe Real-time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* 实施事件转发以将Web SDK收集的数据发送到非Adobe目标。
* 使用Experience Platform调试器和Assurance验证您自己的Platform Web SDK实施。

完成本教程后，您应该可以在自己的网站上开始通过Platform Web SDK实施所有营销应用程序！


>[!NOTE]
>
>类似的多解决方案教程可用于 [移动SDK](../tutorial-mobile-sdk/overview.md).

## 先决条件

所有Experience Cloud客户都可以使用Platform Web SDK。 无需授权基于Platform的应用程序(如Real-time Customer Data Platform或Journey Optimizer)即可使用Web SDK。

在这些课程中，我们假定您拥有Adobe帐户和完成课程所需的权限。 如果没有，则必须联系贵公司的Experience Cloud管理员以获取访问权限。

* 对象 **数据收集**，您必须具有：
   * **[!UICONTROL 平台]** — 权限 **[!UICONTROL Web]** 如果获得许可， **[!UICONTROL Edge]**
   * **[!UICONTROL 资产权限]** — 权限 **[!UICONTROL 批准]**， **[!UICONTROL 开发]**， **[!UICONTROL 编辑属性]**， **[!UICONTROL 管理环境]**， **[!UICONTROL 管理扩展]**、和 **[!UICONTROL Publish]**，
   * **[!UICONTROL 公司权限]** — 权限 **[!UICONTROL 管理资产]**

     有关标记权限的更多信息，请参阅 [文档](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions).

* 对象 **Experience Platform**，您必须具有：

   * 访问 **默认生产**， **&quot;Prod&quot;** 沙盒。
   * 访问 **[!UICONTROL 管理架构]** 和 **[!UICONTROL 查看架构]** 下 **[!UICONTROL 数据建模]**.
   * 访问 **[!UICONTROL 管理身份命名空间]** 和 **[!UICONTROL 查看身份命名空间]** 下 **[!UICONTROL Identity Management]**.
   * 访问 **[!UICONTROL 管理数据流]** 和 **[!UICONTROL 查看数据流]** 下 **[!UICONTROL 数据收集]**.
   * 如果您是某个基于平台的应用程序的客户，并且将要完成 [设置Experience Platform](setup-experience-platform.md) 课程中，您还应具有：
      * 访问 **开发** 沙盒。
      * 下的所有权限项 **[!UICONTROL 数据管理]**、和 **[!UICONTROL 用户档案管理]**：

     所需的功能应该可供所有Experience Cloud客户使用，即使您不是基于平台的应用程序(如Real-Time CDP)的客户。

     有关Platform访问控制的更多信息，请参阅 [文档](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home).

* 对于可选 **Adobe Analytics** 课程，你一定有 [管理员对报表包设置、处理规则和Analysis Workspace的访问权限](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-console/home)

* 对于可选 **Adobe Target** 课程，你一定有 [编辑者或审批者](https://experienceleague.adobe.com/en/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80) 访问权限。

* 对于可选 **Audience Manager** 课程中，您必须有权创建、读取和写入特征、区段和目标。 有关更多信息，请参阅以下教程： [Audience Manager基于角色的访问控制](https://experienceleague.adobe.com/en/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>我们假定您熟悉HTML和JavaScript等前端开发语言。 您无需成为这些语言的专家，但如果您能够阅读和理解代码，则可充分利用本教程。

## 更新

* 2024年4月24日：主要更新，包括添加设置变量/更新变量、拆分个性化和Analytics请求、Journey Optimizer课程

## 加载Luma网站

加载 [Luma网站](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} 在单独的浏览器选项卡中将它添加为书签，这样您可以在教程中根据需要轻松加载它。 除了能够加载我们的托管生产站点外，您不需要任何其他访问Luma的权限。

[![Luma网站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

让我们开始吧！

[下一步： ](configure-schemas.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
