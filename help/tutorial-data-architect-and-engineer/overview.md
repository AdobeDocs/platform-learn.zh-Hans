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
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# 面向数据架构师和数据工程师的Adobe Experience Platform入门

<!--5min-->

_面向数据架构师和数据工程师的Adobe Experience Platform快速入门_&#x200B;是动手进行Experience Platform的最佳起点。


<!--How do we address ETL-->

## 学习目标

数据架构师和数据工程师必须紧密协作，以成功部署Experience Platform。 本实践教程将指导您由&#x200B;_两个角色_&#x200B;执行的关键任务，以便您了解如何开始为自己的业务实施Platform。 您将学习各种练习，从中了解Experience Platform的关键术语、功能、界面和API。 Adobe Experience Cloud应用程序(如Real-time Customer Data Platform、Customer Journey Analytics和Journey Optimizer)的客户也会发现此内容非常有用，因为Platform服务是这些应用程序的重要基础。

![Adobe Experience Cloud营销结构重点介绍了本教程中涵盖的Platform服务 — 身份、个人资料、分段、摄取、查询和治理](assets/marketecture.png)

主题包括：

* 配置用户权限
* 创建沙盒
* 设置Developer Console项目并使用Platform API
* 数据管理 — 包括创建架构、数据集、身份、合并策略和数据治理
* 使用批处理模式和流模式摄取数据
* 使用Adobe Experience Platform Web SDK捕获Web数据
* 构建实时客户档案
* 使用查询服务验证数据并提取数据
* 生成区段

## 业务方案

Adobe Experience Platform是一个技术平台，旨在帮助您实现营销目标。 业务用例应推动您设计和实施技术的方式。 本教程重点介绍一个名为Luma的虚构零售品牌。 Luma在多个国家经营实体店，还通过网站和移动应用程序在线开展业务。 他们投资于Adobe Experience Platform，以将忠诚度、CRM、Web和离线购买数据整合到实时客户配置文件中，并激活这些配置文件以将其营销提升到新的水平。 Luma的业务目标可能与贵公司的目标一致，也可能不一致，但您应该能够将此教程中的实际操作步骤与您自己的业务目标关联起来。

## 先决条件

* 您已观看Experience League上的[Adobe Experience Platform播放列表简介](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction)，并且熟悉Platform功能
* 您可以访问由Adobe Experience Platform(或基于Platform的应用程序，如Real-Time CDP或Journey Optimizer)和数据收集（以前称为Launch）配置的帐户。
* 您是该帐户的系统管理员，或者可以为您配置一个[用户权限](configure-permissions.md)。

## 使用本教程

本教程将面向数据工程师和数据架构师的任务组合在一起。 由于这是入门级教程，您应该能够完成这两个角色的任务。 由于许多课程都是基于以前的课程中所实施的，因此您应该按顺序浏览这些课程。 我会指出哪些课程可以跳过。

在本教程中创建各种Platform元素时，请尽量使用我推荐的名称。 但是，如果您的组织中有多个人员同时参加本教程，则可能需要自定义一些高级别元素名称。 例如，您可能希望将Platform沙盒命名为“Luma Tutorial Platform - Ignatius J Reilly”，而不是仅命名为“Luma Tutorial Platform”。

如果卡住，请尝试先重新阅读说明，然后使用每个页面侧边栏上的![记录问题](https://experienceleague.adobe.com/assets/img/feedback.svg)链接与我联系。

## 技术说明

### 沙盒环境

在本教程中，您将创建一个沙盒环境并使用它来完成练习。 沙盒环境使您能够安全地完成练习和实验，而不用担心会破坏您的生产数据。

### API

平台是以API优先构建的。 虽然界面工作流适用于所有主要平台工作流，并且主要使用，但本教程包含一些面向API的练习。 我将指导您完成Adobe Developer Console中的基本项目设置，并为您提供[!DNL Postman]环境和收藏集以开始使用平台API。 完成本教程后，您可能会发现熟悉平台API并将其用于自己的部署很有价值。

### 第三方技术

虽然在本教程中您将使用多种技术，但您几乎完全停留在Adobe生态系统内。 在您自己的Platform实施中，您可能会将Platform与特定的第三方技术集成。 为了使本教程适用于所有客户，我们将使用更通用的实施。

## 教程更新

* 2023年6月：更新以包含新的权限工作流和使用OAuth服务器到服务器API凭据


现在，我们继续学习第一课 — [配置权限](configure-permissions.md)。
