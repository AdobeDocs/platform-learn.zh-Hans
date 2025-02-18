---
title: 使用BigQuery Google Analytics Connector在Adobe Experience Platform中摄取和分析Source数据
description: 使用BigQuery Google Analytics Connector在Adobe Experience Platform中摄取和分析Source数据
kt: 5342
doc-type: tutorial
exl-id: 19266ac3-7c93-4cdb-8b65-75ce5c38649c
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 1.2使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据

在本模块中，您将设置自己的Google Cloud Platform实例，在Google Cloud Platform中加载示例数据，然后使用BigQuery Source Connector将该数据从Google Cloud Platform摄取到Adobe Experience Platform中。 最后，您将使用Customer Journey Analytics可视化这些数据。

Adobe Experience Platform中的Source连接器可简化将数据导入Adobe Experience Platform的过程。 Google BigQuery是已经可用的连接器之一。 借助Adobe Experience Platform和BigQuery Source Connector，我们现在可以将Google Analytics数据引入Customer Journey Analytics中的Analysis Workspace。

此外，我们可以通过将Google Analytics数据与Customer Journey Analytics中的其他数据源（如CRM、呼叫中心或忠诚度数据）联接来扩充该数据。

## 学习目标

- 熟悉Google云平台和BigQuery用户界面
- 将Google Analytics数据摄取到Adobe Experience Platform
- 使用Customer Journey Analytics分析Google Analytics数据
- 使用离线数据扩充Google Analytics数据

## 先决条件

- 最好最好还是有一定的了解Customer Journey Analytics的知识，但并不一定需要
- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 对Customer Journey Analytics的访问权限
- 访问Google Cloud Platform和Google BigQuery
- **下载这些资源**：
   - [JSON — 示例数据：忠诚度数据](./../../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>请按照[为Chrome文档安装Chrome扩展](../../../getting-started/gettingstarted/ex1.md)中所述，安装、配置并使用Experience League扩展

## 练习

[1.2.1开始使用Google Cloud平台](./ex1.md)

开始使用Google Cloud Platform环境。

[1.2.2在BigQuery中创建第一个查询](./ex2.md)

了解如何使用BigQuery准备数据以加载到Platform中。

[1.2.3将GCP和BigQuery连接到Adobe Experience Platform](./ex3.md)

了解如何在Adobe Experience Platform中设置源连接器。

[1.2.4将数据从BigQuery加载到Adobe Experience Platform中](./ex4.md)

了解如何在Adobe Experience Platform中配置BigQuery源连接器以摄取您的Google Analytics数据。

[1.2.5使用Customer Journey Analytics分析Google Analytics数据](./ex5.md)

了解如何在Customer Journey Analytics中分析Google Analytics数据并将其与忠诚度数据相结合。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

![技术内部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./../../../../overview.md)
