---
title: 面向数据架构师和数据工程师的Adobe Experience Platform快速入门
description: 面向数据架构师和数据工程师的Adobe Experience Platform快速入门。
breadcrumb-title: 概述
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# 面向数据架构师和数据工程师的Adobe Experience Platform快速入门

<!--5min-->

_面向数据架构师和数据工程师的Adobe Experience Platform快速入门_ 是实际操作Experience Platform的最佳起点。


<!--How do we address ETL-->

## 学习目标

数据架构师和数据工程师必须密切协作，才能成功部署Experience Platform。 本动手实践教程将教您执行的关键任务 _两个角色_ 这样，您就知道如何开始为自己的业务实施Platform。 将指导您完成一些练习，这些练习将向您介绍关键的术语、功能、界面和Experience PlatformAPI。 Adobe Experience Cloud应用程序(如Real-time Customer Data Platform、Customer Journey Analytics和Journey Optimizer)的客户也会发现此内容非常有用，因为平台服务是这些应用程序的关键基础。

![Adobe Experience Cloud营销架构，重点介绍本教程中涵盖的Platform服务 — 身份、用户档案、分段、摄取、查询和管理](assets/marketecture.png)

主题包括：

* 配置用户权限
* 创建沙箱
* 设置开发人员控制台项目并使用平台API
* 数据管理 — 包括创建模式、数据集、标识、合并策略和数据管理
* 使用批处理和流模式摄取数据
* 使用Adobe Experience Platform Web SDK捕获Web数据
* 构建实时客户用户档案
* 使用查询服务验证数据并提取数据
* 生成区段

## 业务方案

Adobe Experience Platform是一个技术平台，旨在帮助您实现营销目标。 业务用例应有助于您设计和实施技术的方式。 本教程重点介绍一个虚构的零售品牌Luma。 Luma在多个国家/地区经营实体店，还在网上开设了网站和移动应用。 他们正在投资Adobe Experience Platform，以将忠诚度、CRM、Web和离线购买数据合并到实时客户档案中，并激活这些档案以提升营销水平。 Luma的业务目标可能与您公司的目标一致，也可能与公司的目标不一致，但您应该能够将本教程中的实际操作步骤与您自己的业务目标相关联。

## 先决条件

* 您已完成 [Adobe Experience Platform课程简介](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) Experience League，熟悉平台功能
* 您有权访问已通过Adobe Experience Platform(或基于平台的应用程序，如Real-time CDP或Journey Optimizer)和数据收集（以前称为Launch）进行配置的帐户。
* 您是该帐户的系统管理员，或者可以拥有 [配置用户权限](configure-permissions.md) 为你。

## 使用本教程

本教程将面向数据工程师和数据架构师的任务整合在一起。 由于这是一个介绍性级别的教程，因此您应该能够完成两个角色的任务。 由于许多课程都以前课程中的内容为基础，因此您应该按顺序学习这些课程。 我会指出可以跳过哪些课程。

在本教程中创建各种Platform元素时，请尽量遵循我推荐的名称。 但是，如果您的组织中有多个人员同时阅读本教程，则可能需要自定义一些高级元素名称。 例如，您可能希望将平台沙盒命名为“Luma Tutorial Platform - Ignatius J Reilly”，而不是仅命名为“Luma Tutorial Platform”。

如果卡住，请先尝试重新阅读说明，然后使用 ![记录问题](https://experienceleague.adobe.com/assets/img/feedback.svg) 链接到每个页面的侧栏以联系我。

## 技术说明

### 沙盒环境

在教程中，您将创建一个沙盒环境，并使用它完成练习。 沙盒环境使您能够安全地完成练习和实验，而不必担心生产数据受到破坏。

### API

平台是先构建API的。 虽然所有主要Platform工作流都有界面工作流，且主要使用界面工作流，但本教程中包含一些面向API的练习。 我将指导您完成Adobe Developer控制台中的基本项目设置，并为您提供 [!DNL Postman] 要开始使用Platform API的环境和收藏集。 完成本教程后，您可能会发现熟悉平台API并将其用在您自己的部署中非常有价值。

### 第三方技术

尽管在本教程中您将使用多种技术，但您几乎仍将完全处于Adobe生态系统中。 在您自己的平台实施中，您可能会将平台与特定的第三方技术相集成。 为了使本教程与所有客户相关，我们将使用更宽泛的实施。

现在，我们继续学习第一课……[配置权限](configure-permissions.md).
