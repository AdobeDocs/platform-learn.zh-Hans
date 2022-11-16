---
title: Adobe Experience Platform数据收集和实时服务器端转发
description: 在本模块中，您将使用之前配置的数据集、架构和Adobe Experience Platform数据收集服务器属性来收集数据，然后将该数据服务器端转发到所选的端点。
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 14.Real-Time CDP连接：事件转发

**作者： [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/), [克莱门特·德拉兰德](https://www.linkedin.com/in/clement-delalande/)**

在此模块中，您将使用之前配置的数据集、架构和Adobe Experience Platform数据收集客户端属性来收集数据，然后将该数据服务器端转发到所选的端点。

在本模块中，您将：

- 创建Adobe Experience Platform数据收集服务器属性
- 在Adobe Experience Platform数据收集中安装和使用AdobeCloud Connector扩展
- 创建Google函数端点并向其发送流数据
- 创建AWS端点并向其发送流数据

观看此视频，了解价值、客户历程和配置流程：

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## 学习目标

- 熟悉Adobe Experience Platform数据收集服务器属性和新的AdobeCloud连接器扩展
- 了解如何在Google和AWS等第三方解决方案中重复使用Adobe Experience Platform Web SDK数据
- 了解Adobe Experience Platform数据收集和服务器端转发背后的架构。

## 先决条件

- 访问Adobe Experience Platform和Adobe Experience Platform数据收集
- 了解Adobe Experience Platform数据集和XDM

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem21.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--aepSandboxId--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[14.1创建数据收集事件转发属性](./ex1.md)

在本练习中，您将创建Adobe Experience Platform数据收集事件转发属性。

[14.2更新数据流，以使数据可用于数据收集事件转发属性](./ex2.md)

在本练习中，您将更新现有的数据流，以使由Adobe Experience Platform数据收集客户端属性收集的数据可用于Adobe Experience Platform数据收集服务器属性。

[14.3创建和配置自定义Webhook](./ex3.md)

在本练习中，您将创建并配置一个自定义Webhook，然后开始将Web SDK收集的数据转发到该自定义Webhook。

[14.4创建和配置Google云函数](./ex4.md)

在本练习中，您将创建并配置Google云函数，并开始将Web SDK收集的数据转发到Google。

[14.5向AWS生态系统发展的事件](./ex5.md)

在本练习中，您将使用AWS API网关、AWS Kinesis、AWS Firehose和AWS S3配置AWS环境，之后将开始转发由Web SDK收集的事件数据。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
