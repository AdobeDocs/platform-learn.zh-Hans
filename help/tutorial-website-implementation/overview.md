---
title: 在网站中使用标记实施 Experience Cloud
description: 对于希望了解如何在网站中实施Adobe Experience Cloud解决方案的前端开发人员或技术营销人员而言，“使用标签在网站中实施Experience Cloud”是他们的最佳起点。
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 37%

---

# 概述

_在网站中使用标记实施Experience Cloud_ 对于希望了解如何在其网站上实施Adobe Experience Cloud解决方案的前端开发人员或技术营销人员来说，这是一个完美的起点。

每个课程均包含操作练习和基础信息，可帮助您实施 Experience Cloud 并了解其价值。我们为您提供了演示网站来完成教程，这样您就可以在安全的环境中学习基础技术。完成本教程后，您应该可以通过自己网站上的标记开始实施所有营销解决方案。

>[!INFO]
>
>本教程使用特定于应用程序的扩展和库(适用于Adobe Analytics的AppMeasurement.js，适用于Adobe Target的at.js)。 如果您打算实施Adobe Experience Platform Web SDK，请参阅 [利用Web SDK实施Adobe Experience Cloud](/help/tutorial-web-sdk/overview.md) 教程。


完成本教程后，您将能够：

* 创建标记属性

* 在网站上安装标记属性

* 添加以下 Adobe Experience Cloud 解决方案：
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* 创建规则和数据元素以将数据发送到 Adobe 解决方案

* 使用 Adobe Experience Cloud Debugger 验证实施

* 通过开发、暂存和生产环境发布更改

>[!NOTE]
>
>Adobe Experience Platform Launch正在作为一套数据收集技术集成到Adobe Experience Platform中。 在使用此内容时，您应该了解的界面中推出了几项术语更改：
>
> * platform launch（客户端）现在为 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch服务器端现在为 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge配置现在为 **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

>[!NOTE]
>
>类似的多解决方案教程也可用于 [Web SDK](../tutorial-web-sdk/overview.md) 和 [移动SDK](../tutorial-mobile-sdk/overview.md).

## 先决条件

在这些课程中，我们假定您拥有 Adobe ID 和完成练习所需的权限。如果没有，您可能需要联系 Experience Cloud 管理员以请求获取访问权限。

* 对于标记，您必须拥有“开发”、“批准”、“发布”、“管理扩展”和“管理环境”权限。 有关标记用户权限的更多信息，请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* 对于 Adobe Analytics，您必须知晓跟踪服务器以及用于完成本教程的报表包
* 对于Audience Manager，您必须知晓Audience Manager子域（也称为“合作伙伴名称”、“合作伙伴ID”或“合作伙伴子域”）

此外，我们还假定您熟悉 HTML 和 JavaScript 等前端开发语言。您无需精通这些语言也可完成课程，但如果您能够轻松阅读和理解代码，将可从这些课程中学到更多知识。

## 关于标记

Adobe Experience Platform的标记功能是Adobe推出的新一代网站标记和移动SDK管理功能。 标记为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告解决方案。 标记无需额外付费。 它可供任何 Adobe Experience Cloud 客户使用。

网站的标记允许您集中管理与桌面和移动设备网站上使用的分析、营销和广告解决方案相关的所有JavaScript。 例如，如果您部署Adobe Analytics，则标记将管理AppMeasurementJavaScript库、填充变量和触发请求。

您的容器的内容将被缩小，包括您的自定义代码。一切都是模块化的。如果您不需要某个项目，它不会包含在您的库中。这样，实施就会变得快速而紧凑。

标记也是一个平台，它允许第三方供应商创建扩展，以便轻松地通过标记部署其解决方案。 扩展是一种代码包(JavaScript、HTML和CSS)，用于扩展标记界面和客户端功能。 您可以将标记视为一个操作系统，而扩展则是您用来完成任务的应用程序。

## 关于课程

在这些课程中，您将在名为 Luma 的虚拟零售网站中实施 Adobe Experience Cloud。[Luma 网站](https://luma.enablementadobe.com/content/luma/us/en.html)具有丰富的数据层和功能，可让您构建实际可行的实施。您将在自己的Experience Cloud组织中构建自己的标记资产，并使用Experience Cloud Debugger将其映射到我们托管的Luma网站。

[![Luma 网站](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## 获取工具

1. 由于您将使用某些特定于浏览器的扩展，因此我们建议您使用 [Chrome Web 浏览器](https://www.google.com/chrome/)来完成教程
1. 添加 [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Chrome浏览器的扩展
1. 复制示例html页面代码

   +++示例HTML页面代码

   ```html
   <!doctype html>
   <html lang="en">
   <head>
       <title>Tags: Sample HTML Page</title>
       <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
       <link rel="preconnect" href="//dpm.demdex.net">
       <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//cm.everesttech.net">
       <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
       <link rel="dns-prefetch" href="//dpm.demdex.net">
       <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//cm.everesttech.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
       <!--/Preconnect and DNS-Prefetch-->
       <!--Data Layer to enable rich data collection and targeting-->
       <script>
       var digitalData = {
           "page": {
               "pageInfo" : {
                   "pageName": "Home"
                   }
               }
       };
       </script>
       <!--/Data Layer-->
       <!--jQuery or other helper libraries-->
       <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
       <!--/jQuery-->
       <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
       <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
       <!--/Tags Header Embed Code-->
   </head>
   <body>
       <h1>Tags: Sample HTML Page</h1>
       <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
       <p>See <a href="https://docs.adobe.com/content/help/en/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
   </body>
   </html>
   ```

+++

1. 获取一个文本编辑器，您可以在其中更改示例 HTML 页面。（如果您没有文本编辑器，我们建议您尝试使用 [Brackets](https://brackets.io/)）
1. 将 [Luma 网站](https://luma.enablementadobe.com/content/luma/us/en.html)加入书签

>[!NOTE]
>
>在阅读本教程并在其他浏览器中完成数据收集界面步骤时，您可能会发现在Chrome中打开Luma网站来完成本教程更容易。

让我们开始吧！

[下一课程“创建标记属性”>](create-a-property.md)
