---
title: 1.设置Adobe Experience Platform数据收集和Web SDK扩展
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 1. Foundation — 设置Adobe Experience Platform数据收集和Web SDK扩展

**作者： [马修·伍利](https://www.linkedin.com/in/matthewjwoolley/), [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

本基础模块向您介绍了Adobe的数据收集设想，并说明如何通过Adobe Experience Platform数据收集、Adobe Experience Platform SDK和Adobe Experience Platform Edge Network将数据从网站和移动应用程序导入Adobe Experience Platform和其他应用程序。 本模块介绍了一些概念和技术，这些概念和技术的影响超出了Adobe Experience Platform技术教程的范围。 应该清楚，这些练习的哪些部分是完整教程其余部分的基础，该教程将向您进一步讲授Experience Edge及其功能，以及要获取更多信息和教程的位置。

## 学习目标

- 了解品牌如何使用Adobe Experience Platform数据收集作为其Tag Management系统(TMS)。
- 了解品牌用于将数据摄取到其Adobe产品的数据流。
- 了解如何通过Adobe Experience Platform边缘网络将数据发送到Adobe Experience Platform和其他产品。
- 了解如何创建数据元素和规则以从Web和移动设备中收集数据。
- 了解Web SDK跟踪事件以及如何调试其内容。
- 了解数据层是什么以及实施数据层时的Adobe建议。
- 了解从头开始实施Web SDK的步骤。
- 了解Web实施与移动实施之间的区别。

## 先决条件

- 访问 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform数据收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 访问演示网站

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem1.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--aepSandboxId--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[1.1了解Adobe Experience Platform数据收集](./ex1.md)

在本练习中，探索Adobe Experience Platform数据收集UI并了解其功能。

[1.2边缘网络、数据流和服务器端数据收集](./ex2.md)

在本练习中，您将学习如何在Adobe Experience Platform数据收集界面中将数据转发到Adobe产品，并调查演示网站使用的数据流。

[1.3Adobe Experience Platform数据收集简介](./ex3.md)

在本练习中，您将学习如何设置扩展、构建数据元素和规则，并将它们发布到Web。

[1.4客户端Web数据收集](./ex4.md)

在本练习中，调试已安装的Web SDK，以了解其工作方式以及将在将来的练习中使用哪些数据。

[1.5实施Adobe Analytics和Adobe Audience Manager](./ex5.md)

在本练习中，请参阅并使用Adobe Analytics和Adobe Audience Manager中通过Web SDK收集的Web数据。

[1.6实施Adobe Target](./ex6.md)

在本练习中，在Adobe Target中设置通过Web SDK实施的活动。

[1.7 Adobe Experience Platform中的XDM架构要求](./ex7.md)

为确保Web SDK和alloy.js能够将数据摄取到Adobe Experience Platform中，需要将特定XDM Mixin加入Adobe Experience Platform的XDM架构中。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
