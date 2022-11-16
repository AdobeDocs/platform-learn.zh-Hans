---
title: Adobe Journey Optimizer — 外部天气API、短信操作等
description: Adobe Journey Optimizer — 外部天气API、短信操作等
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# 8.Adobe Journey Optimizer:外部数据源和自定义操作

**作者： [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，您将使用Adobe Journey Optimizer来监听客户行为（在线和离线），并以智能、情境和实时方式对其做出响应。 您在第6模块中已经初步体验过Adobe Journey Optimizer。 在本练习中，您将会更深入地了解并探索更高级的用例，以便在历程中使用外部数据源。

## 学习目标

- 了解如何在Adobe Journey Optimizer中创建事件、外部数据源和历程
- 了解如何使用开放天气API中的天气信息
- 了解如何使用Twilio等自定义操作目标和Adobe Journey Optimizer中的Slack

## 先决条件

- 访问 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Journey Optimizer
- 访问开放天气API

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem12.png)

## 业务上下文

作为一个品牌，您在个性化在线体验方面投入了大量资金。 现在，您希望与离线体验一样具有情境性和相关性。
在本模块中，您将使用客户在离线商店的展示，通过在店内屏幕上向该客户展示相关内容来在商店内提供个性化体验，同时，我们希望向同一客户实时提供个性化的推送或短信消息。
作为品牌，您还了解上下文会极大地影响客户的兴趣，因此您希望引入客户位置的当前天气信息，以决定要显示的内容或促销。

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--aepSandboxId--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[8.1定义事件](./ex1.md)

了解如何使用Adobe Journey Optimizer定义自定义事件。

[8.2定义外部数据源](./ex2.md)

了解如何使用Adobe Journey Optimizer配置外部数据源。

[8.3定义自定义操作](./ex3.md)

了解如何使用Adobe Journey Optimizer定义外部操作。

[8.4创建历程和消息](./ex4.md)

将事件、数据源和操作组合到智能的情境历程中。

[8.5触发您的历程](./ex5.md)

触发您的特定历程。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
