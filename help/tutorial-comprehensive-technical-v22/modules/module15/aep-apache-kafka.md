---
title: 将数据从Apache Kafka流入Adobe Experience Platform
description: 在本模块中，您将学习如何使用Adobe Experience Platform Sink Connector for Kafka Connect设置您自己的Apache Kafka群集，定义主题、制作者和消费者，并将数据流入Adobe Experience Platform。
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 15.将数据从Apache Kafka流到Adobe Experience Platform

**作者： [维韦克蒂瓦里](https://www.linkedin.com/in/vivek-tiwari-25092656/), [尼普纳尔](https://www.linkedin.com/in/nipunnair/), [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将学习如何设置自己的Apache Kafka群集，定义主题、制作者和消费者，以及使用Adobe Experience Platform Sink Connector通过Kafka Connect将数据流入Adobe Experience Platform。

## 学习目标

- 执行本地Kafka群集的基本设置
- 创建Kafka主题，使用Kafka制作人和Kafka消费者
- 配置Kafka Connect和Adobe Experience Platform Sink连接器
- 手动生成事件，并查看在Adobe Experience Platform中摄取的这些事件
- 使用Kafka Connect中现有的Twitter制作者库将Twitter数据流式传输到Adobe Experience Platform

## 先决条件

- 需要在您的计算机上安装Java JDK11或更高版本，您可以在此处下载该JDK: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- 访问 Adobe Experience Platform

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem24.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--aepSandboxId--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[15.1 Apache Kafka简介](./ex1.md)

在本练习中，您将学习Apache Kafka的基础知识

[15.2安装和配置Kafka群集](./ex2.md)

在本练习中，您将下载、安装和配置基本的Apache Kafka群集。

[15.3在Adobe Experience Platform中配置HTTP API流端点](./ex3.md)

在本练习中，您将在Adobe Experience Platform中配置HTTP API源连接器。

[15.4安装和配置Kafka Connect和Adobe Experience Platform Sink连接器](./ex4.md)

在本练习中，您将使用Kafka Connect来安装和使用Adobe Experience Platform Sink连接器，并且您将手动将事件发送到Adobe Experience Platform。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
