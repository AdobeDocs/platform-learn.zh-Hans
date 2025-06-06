---
title: Adobe Experience Platform数据收集和实时服务器端转发
description: 在本模块中，您将使用之前配置的数据集、架构和Adobe Experience Platform数据收集服务器属性来收集数据，然后将该数据服务器端转发到所选的端点。
kt: 5342
doc-type: tutorial
exl-id: dbf5e995-9c2e-4f72-b336-e942cb22cde5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 2.5 Real-Time CDP连接：事件转发

在本模块中，您将使用之前配置的数据集、架构和Adobe Experience Platform数据收集客户端属性来收集数据，然后将该数据服务器端转发到所选的端点。

在本模块中，您将执行以下操作：

- 创建Adobe Experience Platform数据收集服务器资产
- 在Adobe Experience Platform数据收集中安装和使用Adobe Cloud Connector扩展
- 创建Google函数端点并向其流式传输数据
- 创建AWS端点并向其流式传输数据

## 学习目标

- 熟悉Adobe Experience Platform数据收集服务器属性和新的Adobe Cloud Connector扩展
- 了解如何在Google和AWS等第三方解决方案中重用Adobe Experience Platform Web SDK数据
- 了解Adobe Experience Platform数据收集和服务器端转发的架构。

## 先决条件

- 访问Adobe Experience Platform和Adobe Experience Platform数据收集
- 了解Adobe Experience Platform数据集和XDM

>[!NOTE]
>
>请按照[为Chrome文档安装Chrome扩展](../../../getting-started/gettingstarted/ex1.md)中所述，安装、配置并使用Experience League扩展

## 练习

[2.5.1创建数据收集事件转发属性](./ex1.md)

在本练习中，您将创建Adobe Experience Platform数据收集事件转发属性。

[2.5.2更新您的数据流以使数据收集事件转发属性可以使用数据](./ex2.md)

在本练习中，您将更新现有的数据流，以便通过Adobe Experience Platform数据收集客户端资产收集的数据可用于Adobe Experience Platform数据收集服务器资产。

[2.5.3创建和配置自定义webhook](./ex3.md)

在本练习中，您将创建并配置一个自定义webhook，并开始将Web SDK收集的数据转发到该自定义webhook。

[2.5.4将事件转发到GCP Pub/Sub](./ex4.md)

在本练习中，您将创建和配置Google云功能，并开始将Web SDK收集的数据转发到Google。

[2.5.5将活动转发至AWS Kinesis和AWS S3](./ex5.md)

在本练习中，您将使用AWS IAM、AWS Kinesis、AWS Firehose和AWS S3配置您的AWS环境，之后您将开始转发Web SDK收集的事件数据。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

![技术内部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./../../../../overview.md)
