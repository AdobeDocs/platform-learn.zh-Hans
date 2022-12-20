---
title: “利用 Web SDK 实施 Adobe Experience Cloud”教程
description: 了解如何使用 Adobe Experience Platform Web SDK 实施 Experience Cloud 应用程序。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 25%

---

# “利用 Web SDK 实施 Adobe Experience Cloud”教程

了解如何使用 Adobe Experience Platform Web SDK 实施 Experience Cloud 应用程序。

Experience PlatformWeb SDK是客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience Platform边缘网络与Adobe应用程序和第三方服务进行交互。 请参阅 [Adobe Experience Platform Web SDK概述](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) 以了解更多详细信息。

本教程将指导您在名为Luma的示例零售网站上完成Platform Web SDK的实施。 [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma 站点具有丰富的数据层和功能，可让您构建现实的实施。完成本教程后，您应该可以在自己的网站上开始通过Platform Web SDK实施所有营销解决方案。

[![Luma 网站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## 学习目标

完成教程后，您将能够：

* 配置数据流

* 创建XDM模式

* 添加以下Adobe Experience Cloud应用程序：
   * **[Adobe Experience Platform](setup-experience-platform.md)** (以及基于平台构建的应用程序，如Adobe Real-time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* 创建标记规则和XDM对象数据元素，以将数据发送到Adobe应用程序

* 使用Adobe Experience Platform Debugger验证实施

* 捕获用户同意

* 通过事件转发将数据转发给第三方

>[!NOTE]
>
>提供了类似的多解决方案教程 [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## 先决条件

所有Experience Cloud客户都可以使用Platform Web SDK。 无需为基于平台的应用程序(如Real-time Customer Data Platform或Journey Optimizer)授予许可证，即可使用Web SDK。

在这些课程中，我们假定您拥有Adobe帐户，并且 [所需权限](configure-permissions.md) 完成课程。 如果没有，您必须联系Experience Cloud管理员以请求获取访问权限。

此外，我们还假定您熟悉 HTML 和 JavaScript 等前端开发语言。您无需成为这些语言的专家，但如果您能够阅读和理解代码，则可从本教程中学到更多知识。

让我们开始吧！

[下一个： ](configure-permissions.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
