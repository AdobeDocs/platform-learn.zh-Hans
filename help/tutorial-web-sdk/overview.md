---
title: “利用 Web SDK 实施 Adobe Experience Cloud”教程
description: 了解如何使用Adobe Experience Platform Web SDK实施Experience Cloud应用程序。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 11%

---

# “利用 Web SDK 实施 Adobe Experience Cloud”教程

>[!CAUTION]
>
>我们预计将于2024年4月23日星期二发布对本教程的主要更改。 之后，许多练习都将发生更改，您可能需要从头开始重新启动教程才能完成所有课程。


了解如何使用Adobe Experience Platform Web SDK实施Experience Cloud应用程序。

Experience PlatformWeb SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户通过Adobe Experience PlatformEdge Network与Adobe应用程序和第三方服务进行交互。 请参阅 [Adobe Experience Platform Web SDK概述](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hans) 以了解更多详细信息。

本教程将指导您在名为Luma的示例零售网站上实施Platform Web SDK。 此 [Luma网站](https://luma.enablementadobe.com/content/luma/us/en.html) 具有丰富的数据层和功能，可让您构建现实的实施。 完成本教程后，您应该可以在自己的网站上开始通过Platform Web SDK实施所有营销解决方案。

[![Luma网站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## 学习目标

完成本教程后，您将能够：

* 配置数据流

* 创建XDM架构

* 添加以下Adobe Experience Cloud应用程序：
   * **[Adobe Experience Platform](setup-experience-platform.md)** (以及基于Platform构建的应用程序，例如Adobe Real-time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* 创建标记规则和XDM对象数据元素以将数据发送到Adobe应用程序

* 使用Adobe Experience Platform Debugger验证实施

* 捕获用户同意

* 通过事件转发将数据转发给第三方

>[!NOTE]
>
>类似的多解决方案教程可用于 [移动SDK](../tutorial-mobile-sdk/overview.md).

## 先决条件

所有Experience Cloud客户都可以使用Platform Web SDK。 无需授权基于Platform的应用程序(如Real-time Customer Data Platform或Journey Optimizer)即可使用Web SDK。

在这些课程中，我们假定您拥有Adobe账户和 [所需权限](configure-permissions.md) 以完成课程。 如果没有，则必须联系Experience Cloud管理员以请求获取访问权限。

此外，我们还假定您熟悉 HTML 和 JavaScript 等前端开发语言。您无需成为这些语言的专家，但如果您能够阅读和理解代码，则可充分利用本教程。

让我们开始吧！

[下一步： ](configure-permissions.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
