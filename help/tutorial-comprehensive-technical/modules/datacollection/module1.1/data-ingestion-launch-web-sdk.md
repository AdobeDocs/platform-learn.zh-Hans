---
title: 1.1设置Adobe Experience Platform数据收集和Web SDK扩展
description: 基础 — Adobe Experience Platform数据收集和Web SDK扩展的设置
kt: 5342
doc-type: tutorial
exl-id: b69ebe41-ff28-4dde-b639-198201120742
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 1.1基础 — 设置Adobe Experience Platform数据收集和Web SDK标记扩展

此基础模块向您介绍Adobe的数据收集愿景，并介绍如何通过Adobe Experience Platform数据收集、Adobe Experience Platform SDK和Adobe Experience PlatformEdge Network将数据从网站和移动应用程序获取到Adobe Experience Platform和其他应用程序中。

本模块介绍的一些概念和技术所产生的影响超出Adobe Experience Platform技术教程的范围。 应该清楚的是，这些练习的哪些部分是全面教程其余部分的基础，这些部分将向您提供更多有关Edge Network及其功能的知识，以及可在何处获取更多信息和教程。

## 学习目标

- 了解品牌如何使用Adobe Experience Platform数据收集作为其Tag Management System (TMS)。
- 了解品牌用于将数据摄取到其Adobe产品的数据流。
- 了解如何通过Adobe Experience PlatformEdge Network将数据发送到Adobe Experience Platform和其他产品。
- 了解如何创建从Web和移动设备收集数据的数据元素和规则。
- 了解[Web SDK](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/home)跟踪事件以及如何调试其内容。
- 了解什么是数据层以及实施数据层时Adobe的建议。
- 了解从头开始实施[Web SDK](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/home)的步骤是什么。
- 了解Web实施与移动实施之间的区别。

## 先决条件

- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform数据收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 访问演示网站

>[!NOTE]
>
>请按照[为Experience League文档安装Chrome扩展](../../gettingstarted/gettingstarted/ex1.md)中所述，安装、配置并使用Chrome扩展

## 练习

[1.1.1了解Adobe Experience Platform数据收集](./ex1.md)

在本练习中，我们将浏览Adobe Experience Platform数据收集UI并了解其功能。

[1.1.2Edge Network、数据流和服务器端数据收集](./ex2.md)

在本练习中，您将了解如何在Adobe Experience Platform数据收集界面中将数据转发到Adobe产品，并调查Demo网站使用的数据流。

[1.1.3 Adobe Experience Platform数据收集简介](./ex3.md)

在本练习中，您将学习如何设置扩展、构建数据元素和规则并将它们发布到Web。

[1.1.4客户端Web数据采集](./ex4.md)

在本练习中，请调试已安装的Web SDK，以了解其工作方式以及在未来练习中将使用哪些数据。

[1.1.5实施Adobe Analytics和Adobe Audience Manager](./ex5.md)

在本练习中，可查看和使用在Adobe Analytics和Adobe Audience Manager中通过Web SDK收集的Web数据。

[1.1.6实施Adobe Target](./ex6.md)

在本练习中，我们将在Adobe Target中设置一个活动，该活动可通过Web SDK实施。

[1.1.7 Adobe Experience Platform中的XDM架构要求](./ex7.md)

为了确保Web SDK能够将数据摄取到Adobe Experience Platform，需要特定的XDM mixin才能成为Adobe Experience Platform中XDM架构的一部分。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

![技术内部人士](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](../../../overview.md)
