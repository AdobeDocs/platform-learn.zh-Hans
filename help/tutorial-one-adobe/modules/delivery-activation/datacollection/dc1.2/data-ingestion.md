---
title: 基础 — 数据摄取
description: 基础 — 数据摄取
kt: 5342
doc-type: tutorial
exl-id: 0fa38179-637b-4dda-a4e4-754a4cdd61a8
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# 1.2数据摄取

在本模块中，目标是全面了解数据摄取。 您将了解流和批处理中的数据摄取。 您将使用Launch实施流式数据摄取，以便将实验操作网站上的客户行为实时流式传输到Adobe Experience Platform。 您将了解如何使用Adobe Experience Platform工作流批量摄取数据，以便获取CSV文件，将其映射到XDM架构，然后将其摄取到Adobe Experience Platform。

## 学习目标

- 了解如何在Adobe Experience Platform中创建XDM架构
- 了解如何在Adobe Experience Platform中创建数据集
- 了解如何在Launch中创建流端点并配置Adobe Experience Platform扩展
- 了解如何在Launch中创建规则以将数据流式传输到Adobe Experience Platform
- 了解如何将Adobe Experience Platform Launch集成到网页上
- 了解如何使用Adobe Experience Platform工作流将CSV文件摄取到Adobe Experience Platform

## 先决条件

- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform Launch： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 对Postman的访问权限

>[!NOTE]
>
>请按照[为Chrome文档安装Chrome扩展](../../../getting-started/gettingstarted/ex1.md)中所述，安装、配置并使用Experience League扩展

## 练习

[1.2.1浏览网站](./ex1.md)

在本练习中，您将浏览要用作此支持一部分的网站。

[1.2.2配置架构并设置标识符](./ex2.md)

在本练习中，您将配置所需的XDM架构以捕获用户档案信息和客户行为。 在每个XDM模式中，您还必须配置一个主标识符以将所有信息链接到。

[1.2.3配置数据集](./ex3.md)

在本练习中，您将检索所需的数据集，以捕获和存储用户档案信息和客户行为。

[1.2.4从离线来源摄取数据](./ex4.md)

在本练习中，您将转到网站和移动设备应用程序，并像客户一样将数据流式传输到Platform。

[1.2.5数据登陆区](./ex5.md)

使用Azure Blob Storage设置数据登陆区Source连接器。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

![技术内部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./../../../../overview.md)
