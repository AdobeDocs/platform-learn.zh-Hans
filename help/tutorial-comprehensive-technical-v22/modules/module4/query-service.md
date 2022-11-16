---
title: 查询服务
description: 查询服务
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 74943e52-8a7e-4db7-9407-7deeab008fa7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---

# 4.查询服务

**作者： [马克·米维斯](https://www.linkedin.com/in/marcmeewis/), [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将获得Adobe Experience Platform查询服务的实际操作预览。 通过查询服务，您可以跨所有Adobe Experience Cloud应用程序数据执行全方位查询，从而跨Adobe Campaign、Analytics、Audience Manager、Target和Advertising Cloud以及加载/插入到Adobe Experience Platform中的其他客户数据加入并分析数据。

查询服务是一种无服务器工具。 它通过其PostgreSQL兼容性支持来自多个客户端应用程序的SQL查询和连接。
我们将使用已通过Web交互数据、呼叫中心交互以及上传到平台的客户忠诚度数据注入到平台中的数据。

## 学习目标

- 熟悉Adobe Experience Platform UI
- 连接到查询服务并运行SQL查询
- 浏览Adobe Experience Platform中的数据集
- 将表格或Power BI连接到Adobe Experience Platform查询服务以创建可视化和报表

## 先决条件

- 首选熟悉SQL，但不是必需的
- 访问Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 数据集（实验室期间使用的数据集，为您预加载）
- PostgreSQL
- 表格或MicrosoftPower BI桌面
- **下载这些资产**:
   - [JSON — 示例数据：网站交互](./../../assets/json/ee.json)
   - [JSON — 示例数据：呼叫中心交互](./../../assets/json/callcenter.json)
   - [JSON — 示例数据：忠诚度](./../../assets/json/loyalty.json)

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem7.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--module7sandbox--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[4.0先决条件](./ex0.md)

您需要安装PSQL才能执行此启用练习中的查询。 根据您的操作系统，您必须安装MicrosoftPower BI或表格。 Windows用户可以在Power BI或表格之间进行选择。 Mac用户应安装Tableau。

[4.1快速入门](./ex1.md)

在本练习中，您将浏览Adobe Experience Platform查询服务用户界面，了解数据集，查找查询，最后从PSQL设置连接。

[4.2使用查询服务](./ex2.md)

在本练习中，您将了解基本的查询服务语法，并可以在查询中标识XDM架构的属性。

[4.3查询、查询、查询……和流失分析](./ex3.md)

在本练习中，您将执行查询，在进行一些流失分析时，将了解Adobe定义的函数。 在此操作结束时，您将编写一个查询来准备数据集以在MicrosoftPower BI中使用。

[4.4从查询生成数据集](./ex4.md)

在本练习中，您将根据上一个练习中执行的查询生成一个数据集，并且您将在下一个练习中使用该数据集。

[4.5查询服务和Power BI](./ex5.md)

在本练习中，您将Power BI连接到Adobe Experience Platform和查询服务以执行呼叫中心交互分析。

[4.6查询服务和表格](./ex6.md)

在本练习中，您将Tableau连接到Adobe Experience Platform和查询服务以执行Callcenter交互分析。

[4.7查询服务API](./ex7.md)

在本练习中，您将使用查询服务API来管理查询模板和查询计划。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
