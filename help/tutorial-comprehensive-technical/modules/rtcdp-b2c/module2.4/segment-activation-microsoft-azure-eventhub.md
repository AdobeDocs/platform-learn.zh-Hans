---
title: 区段激活到Microsoft Azure事件中心
description: 区段激活到Microsoft Azure事件中心
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 2.4 Real-Time CDP：将区段激活激活到Microsoft Azure事件中心

**作者：[Marc Meewis](https://www.linkedin.com/in/marcmeewis/)，[Wouter Van Galuwe](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将设置Microsoft Azure EventHub目标作为Adobe Experience Platform Real-time CDP的实时目标。 您还将设置和部署一个Azure函数，每当Adobe Experience Platform将区段有效负载交付到Azure EventHub目标时，该函数都将实时触发。 您将触发的Azure函数将显示Adobe Experience Platform Real-time CDP激活功能的机制。

在本模块中，您还将了解什么会触发Real-time CDP将有效负载实际传送到指定目标。 我们还将讨论区段鉴定的状态以及它与激活的关系。

Adobe Experience Platform Real-time CDP支持将数据激活到流式云存储目标，允许您以JSON格式将受众数据和事件实时导出到这些目标。 然后，您可以基于目标中的这些事件描述业务逻辑

Microsoft Azure事件中心是一项完全托管的实时数据摄取服务，它简单、可靠且可扩展。 每秒从任何来源流式传输数百万个事件以构建动态数据管道并立即响应业务挑战。

## 学习目标

- 熟悉Microsoft Azure事件中心
- 设置Microsoft Azure事件中心的RTCDP目标
- 了解Real-time CDP何时激活以及激活有效负载的外观
- 设置Visual Studio代码以开发、测试和部署您的Azure项目
- 创建和部署使用RTCDP实时提供的区段资格的Azure函数

## 先决条件

- 访问[Adobe Experience Platform](https://experience.adobe.com/platform)
- 熟悉AEP演示网站环境
- 了解如何在Adobe Experience Platform中定义、使用和激活流区段

>[!NOTE]
>
>请按照[0.1 — 为Experience League文档](../../gettingstarted/gettingstarted/ex1.md)安装ChromeChrome扩展

## 练习

[2.4.0配置环境](./ex0.md)

在本练习中，您将设置您的Microsoft Azure环境。

[2.4.1配置Microsoft Azure EventHub环境](./ex1.md)

在本练习中，您将设置Microsoft Azure EventHub环境。

[2.4.2在Adobe Experience Platform中配置Azure事件中心目标](./ex2.md)

在本练习中，您将设置您的Real-time CDP目标连接，以便实时将区段交付到您在上一个练习中配置的EventHub。

[2.4.3创建区段](./ex3.md)

在本练习中，您将在Adobe Experience Platform中创建一个流区段

[2.4.4激活区段](./ex4.md)

在本练习中，您将向Real-time CDP EventHub目标激活流区段。

[2.4.5创建您的Microsoft Azure项目](./ex5.md)

在本练习中，您将创建一个Azure函数，该函数将在AdobeExperience Platform将区段资格激活到相应的Azure事件中心目标时实时触发。

[2.4.6端到端方案](./ex6.md)

此时，一切都已设置。 您现在可以在AEP演示网站上进行浏览，并将区段资格交付到Microsoft Azure EventHub Trigger函数。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](../../../overview.md)
