---
title: Foundation — 实时客户档案
description: Foundation — 实时客户档案
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
exl-id: 79ae9722-bf38-47f7-acbc-aa5bd1289411
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# 2.1 Foundation — 实时客户资料

**作者：[Wouter Van Galuwe](https://www.linkedin.com/in/woutervangeluwe/)**

在本模块中，我们将深入探讨Adobe Experience Platform的实时客户配置文件和身份功能。 您将了解如何定义受众、Identity Service和Experience CloudID的角色，以及如何定义区段生成器查询来定义您自己的区段。

## 学习目标

- 了解如何通过Adobe Experience Platform UI可视化客户的实时客户个人资料
- 了解如何使用Adobe Experience Platform的区段生成器创建区段
- 了解如何使用Adobe Experience Platform API创建区段并将区段结果存储在数据集中
- 了解在离线环境中访问完整客户个人资料的影响，包括实时行为

## 先决条件

- 访问[Adobe Experience Platform](https://experience.adobe.com/platform)
- 访问[https://public.aepdemo.net](https://public.aepdemo.net)
- **下载这些资源**：
   - [Postman收藏集](./../../../assets/postman/postman_profile.zip)

>[!NOTE]
>
>请按照[为Experience League文档安装Chrome扩展](../../gettingstarted/gettingstarted/ex1.md)中所述，安装、配置并使用Chrome扩展

## 练习

[2.1.1访问网站](./ex1.md)

在本练习中，您将按照脚本浏览网站。

[2.1.2可视化您自己的实时客户个人资料 — UI](./ex2.md)

在本练习中，您将登录到Adobe Experience Platform，并在UI中查看您自己的Real-time Customer Profile 。

[2.1.3可视化您自己的实时客户个人资料 — API](./ex3.md)

在本练习中，您将使用Postman和Adobe I/O，通过利用Adobe Experience Platform的API来查看您自己的实时客户个人资料。

[2.1.4创建区段 — UI](./ex4.md)

在本练习中，您将使用Adobe Experience Platform的区段生成器创建一个区段。

[2.1.5创建区段 — API](./ex5.md)

在本练习中，您将使用Postman和Adobe I/O创建区段，并将该区段的结果存储为数据集，具体方法是使用Adobe Experience Platform的API。

[2.1.6在呼叫中心查看您的实时客户资料](./ex6.md)

在本练习中，您将模拟一个接到客户呼叫的呼叫中心员工。 为了真正影响客户的体验，您需要实时访问所有可用的信息。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](../../../overview.md)
