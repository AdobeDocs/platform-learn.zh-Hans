---
title: 面向数据架构师和数据工程师的Adobe Experience Platform入门
description: 面向数据架构师和数据工程师的Adobe Experience Platform快速入门。
breadcrumb-title: 概述
role: Data Architect, Data Engineer
jira: KT-4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# 面向数据架构师和数据工程师的Adobe Experience Platform入门

<!--5min-->

_面向数据架构师和数据工程师的Adobe Experience Platform入门_ 是动手实施Experience Platform的最佳起点。


<!--How do we address ETL-->

## 学习目标

数据架构师和数据工程师必须紧密协作，以成功部署Experience Platform。 本实践教程向您讲授由以下人员执行的关键任务 _两个角色_ 这样您就知道如何开始为自己的业务实施Platform。 您将学习一些练习，这些练习将向您介绍Experience Platform的关键术语、功能、界面和API。 Adobe Experience Cloud应用程序(如Real-time Customer Data Platform、Customer Journey Analytics和Journey Optimizer)的客户也会发现此内容非常有用，因为Platform服务是这些应用程序的重要基础。

![Adobe Experience Cloud营销结构，重点介绍本教程中涵盖的Platform服务 — 身份、个人资料、分段、摄取、查询和治理](assets/marketecture.png)

主题包括：

* 配置用户权限
* 创建沙盒
* 设置开发人员控制台项目并使用平台API
* 数据管理 — 包括创建架构、数据集、身份、合并策略和数据治理
* 使用批处理模式和流模式摄取数据
* 使用Adobe Experience Platform Web SDK捕获Web数据
* 构建实时客户档案
* 使用查询服务验证数据和提取数据
* 生成区段

## 业务方案

Adobe Experience Platform是一个技术平台，旨在帮助您实现营销目标。 业务用例应推动您设计和实施技术的方式。 本教程重点介绍一个名为Luma的虚构零售品牌。 Luma在多个国家经营实体店，还通过网站和移动应用程序在线开展业务。 他们投资于Adobe Experience Platform，旨在将忠诚度、CRM、Web和离线购买数据整合到实时客户配置文件中，并激活这些配置文件以将其营销提升到新的水平。 Luma的业务目标可能与贵公司的目标一致，也可能不一致，但您应该能够将此教程中的实际操作步骤与您自己的业务目标关联起来。

## 先决条件

* 您已完成 [Adobe Experience Platform课程简介](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) Experience League并熟悉Platform功能
* 您可以访问通过Adobe Experience Platform(或Real-Time CDP或Journey Optimizer等基于平台的应用程序)和数据收集（以前称为Launch）配置的帐户。
* 您是该帐户的系统管理员，或者可以拥有一个 [配置用户权限](configure-permissions.md) 为了你。

## 使用本教程

本教程结合了数据工程师和数据架构师的任务。 由于这是入门级教程，您应该能够完成这两个角色的任务。 由于许多课程都是基于以前课程中所实施的，因此您应按顺序浏览这些课程。 我会指出哪些课程可以跳过。

在本教程中创建各种Platform元素时，请尽量使用我推荐的名称。 但是，如果您的组织中有多个人员同时参加本教程，您可能需要自定义一些高级元素名称。 例如，您可能希望将Platform沙盒命名为“Luma Tutorial Platform - Ignatius J Reilly”，而不是仅命名为“Luma Tutorial Platform”。

如果您卡住了，请先尝试重新阅读说明，然后使用 ![记录问题](https://experienceleague.adobe.com/assets/img/feedback.svg) 每个页面侧边栏上的链接以联系我。

## 技术说明

### 沙盒环境

在本教程中，您将创建一个沙盒环境并使用它完成练习。 沙盒环境使您能够安全地完成练习和实验，而不用担心影响生产数据。

### API

平台是API优先构建的。 虽然界面工作流适用于所有主要的Platform工作流，并且主要使用，但本教程包含一些面向API的练习。 我将指导您完成Adobe Developer控制台中的基本项目设置，并为您提供 [!DNL Postman] 环境和收藏集，以开始使用Platform API。 完成本教程后，您可能会发现熟悉平台API并将其用于自己的部署很有价值。

### 第三方技术

虽然在本教程中您将使用多种技术，但您几乎完全停留在Adobe生态系统内。 在您自己的Platform实施中，您可能会将Platform与特定的第三方技术集成。 为了使本教程适用于所有客户，我们将使用更通用的实施。

现在，让我们转到第一课……[配置权限](configure-permissions.md).
