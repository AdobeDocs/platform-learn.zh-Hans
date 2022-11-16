---
title: 使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据
description: 使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# 12.使用BigQuery Source Connector在Adobe Experience Platform中摄取并分析Google Analytics数据

**作者： [维克托·德·拉·伊格莱西亚](https://www.linkedin.com/in/victordelaiglesia/), [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将设置自己的Google云平台实例，在Google云平台中加载示例数据，然后使用BigQuery源连接器将该数据从Google云平台摄取到Adobe Experience Platform。 最后，您将使用Customer Journey Analytics来可视化该数据。

Adobe Experience Platform中的源连接器使将数据导入Adobe Experience Platform的过程变得简单。 Google BigQuery是已有的连接器之一。 借助Adobe Experience Platform和BigQuery Source Connector，我们现在可以将Google Analytics数据导入Analysis Workspace的Customer Journey Analytics。

此外，我们还可以通过将Google Analytics数据与其他数据源(如Customer Journey Analytics内的CRM、呼叫中心或忠诚度数据)联合来扩充这些数据。

## 学习目标

- 熟悉Google云平台和BigQuery用户界面
- 将 Google Analytics 数据摄取到 Adobe Experience Platform
- 使用Customer Journey Analytics对Google Analytics数据进行分析
- 使用离线数据扩充Google Analytics数据

## 先决条件

- 需要熟悉一些Customer Journey Analytics，但不是必需的
- 访问Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问 Customer Journey Analytics
- 访问Google云平台和Google BigQuery
- **下载这些资产**:
   - [JSON — 示例数据：忠诚度数据](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem16.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--aepSandboxId--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[12.1创建您的Google Cloud Platform帐户](./ex1.md)

创建您的Google Cloud Platform帐户。

[12.2在BigQuery中创建第一个查询](./ex2.md)

了解如何使用BigQuery准备数据以加载到平台中。

[12.3将GCP和BigQuery连接到Adobe Experience Platform](./ex3.md)

了解如何在Adobe Experience Platform中设置源连接器。

[12.4将数据从BigQuery加载到Adobe Experience Platform](./ex4.md)

了解如何在Adobe Experience Platform中配置BigQuery源连接器以摄取Google Analytics数据。

[12.5使用Google Analytics分析Customer Journey Analytics数据](./ex5.md)

了解如何分析Customer Journey Analytics中的Google Analytics数据，并将其与忠诚度数据结合。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
