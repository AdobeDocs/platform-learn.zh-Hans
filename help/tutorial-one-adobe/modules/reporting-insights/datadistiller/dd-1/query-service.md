---
title: 查询服务
description: 查询服务
kt: 5342
doc-type: tutorial
exl-id: 881dcff5-3637-4b67-9e61-88690babe83b
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# 2.1查询服务

在本模块中，您将获得Adobe Experience Platform查询服务的实际操作预览。 通过查询服务，您可以跨所有Adobe Experience Cloud应用程序数据执行全渠道查询，并可跨Adobe Campaign、Analytics、Audience Manager、Target和Advertising Cloud联结和分析数据，以及加载/插入Adobe Experience Platform的其他客户数据。

查询服务是一种无服务器工具。 它通过与PostgreSQL的兼容性支持来自多个客户端应用程序的SQL查询和连接。
我们将结合使用Web交互数据、呼叫中心交互和上传到平台中的客户忠诚度数据来使用已插入到平台中的数据。

## 学习目标

- 熟悉Adobe Experience Platform UI
- 连接到查询服务并运行SQL查询
- 浏览Adobe Experience Platform中的数据集
- 将Tableau或Power BI连接到Adobe Experience Platform查询服务以创建可视化图表和报表

## 先决条件

- 最好对SQL有一定的了解，但不是必需的
- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 数据集（实验室期间使用的数据集，为您预加载）
- PostgreSQL
- Tableau或Microsoft Power BI桌面

>[!NOTE]
>
>请按照[为Chrome文档安装Chrome扩展](../../../getting-started/gettingstarted/ex1.md)中所述，安装、配置并使用Experience League扩展

## 练习

[2.1.1先决条件](./ex1.md)

您需要安装PSQL才能执行此启用练习中的查询。 根据您的操作系统，您必须安装Microsoft Power BI或Tableau。 Windows用户可以选择Power BI或Tableau。 Mac用户应该安装Tableau。

[2.1.2快速入门](./ex2.md)

在本练习中，您将探索Adobe Experience Platform查询服务用户界面，了解数据集，找到您的查询，并最终设置来自PSQL的连接。

[2.1.3使用查询服务](./ex3.md)

在本练习中，您将了解基本查询服务语法，并可以在查询中识别XDM架构的属性。

[2.1.4查询、查询、查询……和流失分析](./ex4.md)

在本练习中，您将进行查询，并在进行流失分析时了解Adobe定义的函数。 最后，您将编写一个查询来准备数据集，以供在Microsoft Power BI中使用。

[2.1.5从查询生成数据集](./ex5.md)

在本练习中，您将通过在之前执行的查询来生成数据集，并在下一个练习中使用此数据集。

[2.1.6查询服务和Power BI](./ex6.md)

在本练习中，您会将Power BI连接到Adobe Experience Platform和查询服务以执行Callcenter交互分析。

[2.1.7查询服务和Tableau](./ex7.md)

在本练习中，您会将Tableau连接到Adobe Experience Platform和查询服务以执行Callcenter交互分析。

[2.1.8查询服务API](./ex8.md)

在本练习中，您将使用查询服务API来管理查询模板和查询计划。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

![技术内部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./../../../../overview.md)
