---
title: 区段激活到Microsoft Azure事件中心
description: 区段激活到Microsoft Azure事件中心
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 十三、Real-Time CDP:区段激活到Microsoft Azure事件中心

**作者： [马克·米维斯](https://www.linkedin.com/in/marcmeewis/), [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将设置一个Microsoft Azure EventHub目标，作为Adobe Experience Platform实时CDP的实时目标。 您还将设置和部署Azure函数，当Adobe Experience Platform将区段有效负载发送到您的Azure EventHub目标时，该函数将实时触发。 您将触发的Azure函数将显示Adobe Experience Platform实时CDP激活功能的机制。

在本模块中，您还将了解哪些触发了实时CDP来将有效负载实际交付到指定目标。 我们还将讨论区段资格的状态以及它与激活的关系。

Adobe Experience Platform Real-time CDP支持对云存储目标进行数据激活，从而允许您以JSON格式将受众数据和事件实时导出到这些目标。 然后，您可以在目标中针对这些事件描述业务逻辑

Microsoft Azure事件中心是一项完全托管的实时数据摄取服务，其简单、可信且可扩展。 每秒从任何来源传输数百万个事件，以构建动态数据管道并立即应对业务挑战。

## 学习目标

- 熟悉Microsoft Azure事件中心
- 将RTCDP目标设置到您的Microsoft Azure事件中心
- 了解Real-time CDP何时激活以及激活有效负载的外观
- 设置Visual Studio代码以开发、测试和部署您的Azure项目
- 创建和部署Azure函数，该函数使用RTCDP实时提供的区段资格条件

## 先决条件

- 访问 [Adobe Experience Platform](https://experience.adobe.com/platform)
- 熟悉AEP演示网站环境
- 了解如何在Adobe Experience Platform中定义、使用和激活流区段

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem18.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--module18sandbox--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[13.0配置环境](./ex0.md)

在本练习中，您将设置Microsoft Azure环境。

[13.1配置Microsoft Azure EventHub环境](./ex1.md)

在本练习中，您将设置Microsoft Azure事件中心环境。

[13.2在Adobe Experience Platform中配置Azure事件中心目标](./ex2.md)

在本练习中，您将设置您的实时CDP目标连接，该连接会将区段实时传送到您在上一个练习中配置的EventHub。

[13.3创建区段](./ex3.md)

在本练习中，您将在Adobe Experience Platform中创建一个流区段

[13.4激活区段](./ex4.md)

在本练习中，您将激活流区段以访问您的实时CDP EventHub目标。

[13.5创建Microsoft Azure项目](./ex5.md)

在本练习中，您将创建一个Azure函数，该函数将在Adobe Experience Platform激活相应Azure事件中心目标的区段资格条件时实时触发。

[13.6端到端方案](./ex6.md)

这时一切都已设置完毕。 您现在可以在AEP演示网站上浏览一些内容，并将区段资格交付到Microsoft Azure事件中心触发器功能。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
