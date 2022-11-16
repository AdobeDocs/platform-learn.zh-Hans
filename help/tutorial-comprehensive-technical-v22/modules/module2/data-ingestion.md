---
title: 基础 — 数据摄取
description: 基础 — 数据摄取
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 2.基础 — 数据获取

**作者： [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在此模块中，目标是了解有关数据摄取的所有信息。 您将了解流式处理和批量处理中的数据摄取。 您将使用Launch实施流数据摄取，以便实时将实验操作网站上的客户行为流式传输到Adobe Experience Platform。 您将了解批量数据摄取，方法是使用Adobe Experience Platform工作流获取CSV文件，将其映射到XDM架构，然后将其摄取到Adobe Experience Platform中。

## 学习目标

- 了解如何在Adobe Experience Platform中创建XDM模式
- 了解如何在Adobe Experience Platform中创建数据集
- 了解如何在Launch中创建流端点并配置Adobe Experience Platform扩展
- 了解如何在Launch中创建规则以将数据流式传输到Adobe Experience Platform
- 了解如何将Adobe Experience Platform Launch集成到网页上
- 了解如何使用Adobe Experience Platform工作流将CSV文件摄取到Adobe Experience Platform

## 先决条件

- 访问 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 访问 [https://public.aepdemo.net](https://public.aepdemo.net)
- 访问Postman

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem2.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--module2sandbox--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[2.1浏览网站](./ex1.md)

在本练习中，您将浏览将用作此启用部分的网站。

[2.2配置架构和设置标识符](./ex2.md)

在本练习中，您将配置所需的XDM架构，以捕获用户档案信息和客户行为。 在每个XDM架构中，您还必须配置一个主标识符，以将所有信息链接到。

[2.3配置数据集](./ex3.md)

在本练习中，您将检索所需的数据集，以捕获和存储用户档案信息和客户行为。

[2.4从离线源摄取数据](./ex4.md)

在本练习中，您将访问网站和移动设备应用程序，并像客户一样行为，将数据流式传输到Platform。

[2.5数据登陆区](./ex5.md)

使用Azure Blob Storage设置数据登陆区源连接器。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
