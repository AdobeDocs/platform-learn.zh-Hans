---
title: 智能服务
description: 智能服务
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---

# 5.智能服务

**作者： [迪普蒂曼·巴达耶纳](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将学习如何设置、配置和使用Adobe Experience Platform Intelligent Services。

## 学习目标

- 熟悉Adobe Experience Platform
- 配置架构/数据集以与Intelligent Services一起使用
- 创建新的Customer AI实例
- 评分仪表板和分段

## 先决条件

- 访问 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem5.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--module10sandbox--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[5.1客户AI — 数据准备（摄取）](./ex1.md)

通过Adobe Experience Platform上的体验数据模型(XDM)，可摄取和转换客户数据。 具体而言，Intelligent Services中使用的所有数据集都必须符合消费者体验事件(CEE)XDM架构。

[5.2 Customer AI — 创建新实例（配置）](./ex2.md)

营销分析师通过指定业务规则和识别相关数据来配置所需的预测。 配置模型后，计划执行和查看得分。

[5.3客户AI — 评分仪表板和分段（预测并采取行动）](./ex3.md)

模型完成培训和评分后，分数会写回Platform。 您可以决定要对预测执行哪些操作，例如定义区段、构建自定义功能板等。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
