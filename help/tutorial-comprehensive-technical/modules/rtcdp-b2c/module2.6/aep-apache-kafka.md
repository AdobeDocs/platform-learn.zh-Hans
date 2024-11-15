---
title: 将数据从Apache Kafka流式传输到Adobe Experience Platform中
description: 在本模块中，您将学习如何设置自己的Apache Kafka集群，定义主题、制作者和消费者，并使用适用于Kafka Connect的Adobe Experience Platform Sink Connector将数据流式传输到Adobe Experience Platform。
kt: 5342
doc-type: tutorial
exl-id: 2b7010f3-ab31-4099-aecd-fd4e73b7e96e
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 2.6将数据从Apache Kafka流式传输到Adobe Experience Platform

**作者：[Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/)，[Nipun Nair](https://www.linkedin.com/in/nipunnair/)，[Wouter Van Galuwe](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将学习如何设置自己的Apache Kafka聚类，定义主题、制作者和消费者，并通过Kafka Connect使用Adobe Experience Platform Sink Connector将数据流式传输到Adobe Experience Platform。

## 学习目标

- 执行本地Kafka群集的基本设置
- 创建Kafka主题，使用Kafka制作者和Kafka消费者
- 配置Kafka连接和Adobe Experience Platform接收器连接器
- 手动生成事件并查看这些事件在Adobe Experience Platform中被摄取
- 使用Kafka Connect中的现有Twitter生成器库将Twitter数据流式传输到Adobe Experience Platform

## 先决条件

- 您的计算机上需要安装Java JDK11或更高版本，您可以在此处下载该JDK： [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- 对Adobe Experience Platform的访问权限

>[!NOTE]
>
>请按照[为Experience League文档安装Chrome扩展](../../gettingstarted/gettingstarted/ex1.md)中所述，安装、配置并使用Chrome扩展

## 练习

[2.6.1 Apache Kafka简介](./ex1.md)

在本练习中，您将了解Apache Kafka的基础知识

[2.6.2安装和配置Kafka群集](./ex2.md)

在本练习中，您将下载、安装和配置基本的Apache Kafka集群。

[2.6.3在Adobe Experience Platform中配置HTTP API流端点](./ex3.md)

在本练习中，您将配置Adobe Experience Platform中的HTTP API Source连接器。

[2.6.4安装和配置Kafka Connect和Adobe Experience Platform接收器连接器](./ex4.md)

在本练习中，您将使用Kafka Connect来安装和使用Adobe Experience Platform接收器连接器，并将手动将事件发送到Adobe Experience Platform。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](../../../overview.md)
