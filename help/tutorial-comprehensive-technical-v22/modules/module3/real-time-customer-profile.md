---
title: 基础 — 实时客户资料
description: 基础 — 实时客户资料
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 050e5d99-544d-4a86-a7f6-9f103381dca5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 3.基础 — 实时客户资料

**作者： [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，我们将深入研究Adobe Experience Platform的实时客户资料和身份功能。 您将了解如何定义受众、身份服务和Experience CloudID的角色，以及如何定义区段生成器查询以定义您自己的区段。

## 学习目标

- 了解如何通过Adobe Experience Platform的UI显示客户的实时客户资料
- 了解如何使用Adobe Experience Platform的区段生成器创建区段
- 了解如何使用Adobe Experience Platform API创建区段并将区段结果存储在数据集中
- 了解在离线环境中访问完整客户配置文件（包括实时行为）的影响

## 先决条件

- 访问 [Adobe Experience Platform](https://experience.adobe.com/platform)
- 访问 [https://public.aepdemo.net](https://public.aepdemo.net)
- **下载这些资产**:
   - [Postman收藏集](./../../assets/postman/postman_profile.zip)

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem3.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--aepSandboxId--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[3.1访问网站](./ex1.md)

在本练习中，您将按照脚本浏览网站。

[3.2可视化您自己的实时客户用户档案 — UI](./ex2.md)

在本练习中，您将登录Adobe Experience Platform，并在UI中查看您自己的实时客户资料。

[3.3可视化您自己的实时客户资料 — API](./ex3.md)

在本练习中，您将使用Postman和Adobe I/O，通过使用Adobe Experience Platform的API，查看您自己的实时客户资料。

[3.4创建区段 — UI](./ex4.md)

在本练习中，您将通过使用Adobe Experience Platform的区段生成器来创建一个区段。

[3.5创建区段 — API](./ex5.md)

在本练习中，您将使用Postman和Adobe I/O通过使用Adobe Experience Platform的API，创建一个区段，并将该区段的结果存储为数据集。

[3.6在呼叫中心查看您的实时客户资料](./ex6.md)

在本练习中，您将模拟收到客户呼叫的呼叫中心员工。 为了真正影响此客户的体验，您将需要实时访问所有可用的信息。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
