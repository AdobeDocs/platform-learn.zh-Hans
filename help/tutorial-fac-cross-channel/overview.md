---
title: 通过联合受众组合解锁跨渠道见解
description: 联合受众构成是一项强大的功能，它使数据架构师和数据工程师能够直接从第三方数据仓库构建和丰富受众。
breadcrumb-title: 概述
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 概述

联合受众组合是一项强大的功能，可用于Adobe Real-Time Customer Data Platform (Real-Time CDP)和Adobe Journey Optimizer环境。 它使数据架构师和数据工程师能够直接从[受支持的](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}第三方数据仓库构建和扩充受众，而无需将数据复制到Adobe Experience Platform。 本教程为技术用户提供了实践指导，帮助他们连接企业数据仓库、创建和丰富受众以及激活受众以提供个性化的营销体验。

## 可视化指南

本可视化指南向您展示为支持业务方案的各个方面而执行的每项活动的步骤。 目标是为您提供可在环境中利用的活动，包括：

- 将Adobe Experience Platform连接到企业数据仓库。
- 使用联合受众组合创建和管理受众。
- 将联合受众映射到外部目标，如Amazon S3。
- 使用联合数据丰富现有受众。
- 创建受众以推动“即时”个性化。
- 使用联合受众数据构建客户历程。

本指南专为使用Real-Time CDP或Journey Optimizer的数据架构师和数据工程师而设计。 它假定您熟悉Adobe Experience Platform和基本的Data Warehouse概念。

## 业务上下文

SecurFinancial是一家领先的金融服务公司。 它跨完全不同的来源利用丰富的客户数据来对大量区段提供个性化的优惠和营销活动。 他们计划使用Adobe的Real-Time CDP联合受众构成功能，此功能允许企业使用其现有数据仓库，同时使用Adobe Experience Platform的应用程序提供个性化的客户体验。 主要优势包括：

- **对仓库数据的访问**：从支持的数据仓库中的数据集创建高价值受众，而无需数据复制。
- **最小化数据移动**：直接在仓库中查询数据，减少重复并维护数据管理。
- **统一体验工作流**：在Adobe Experience Platform中针对跨渠道用例策划和激活受众。
- **增强型个性化**：通过仓库属性丰富用户档案和受众，从而提供实时、触发的体验。

## 业务方案

SecurFinancial希望发起电子邮件营销活动，重新定位那些根据良好的信用获得预贷款资格，且SecurFinancial资产组合中没有有效贷款的客户。 虽然他们实时摄取在线行为数据，但在确定客户资格预审方面面临挑战，因为他们无法将信用信息摄取到AEP。 为了在不移动受限数据的情况下确定预认证客户的资格，他们将使用联合受众构成丰富其AEP行为受众。

## 先决条件

要在环境中执行类似活动，请确保您具有：

- 访问配置了Real-Time CDP或Journey Optimizer的Adobe Experience Platform帐户。
- 系统管理员权限或配置权限的功能。
- 熟悉Adobe Experience Platform概念，例如架构、数据集和受众(推荐：完成Experience League上的[Adobe Experience Platform播放列表简介](https://experienceleague.adobe.com/zh-hans/playlists/experience-platform-introduction?lang=en){target="_blank"})。
- 访问支持的企业数据仓库(例如，Amazon Redshift、Azure Synapse Analytics、Snowflake或Google BigQuery)。
- 用于查询数据仓库的SQL的基本知识。
- **沙盒环境**：在您组织的Real-Time CDP实例中创建一个沙盒，以便在不影响生产数据的情况下安全地试验。
- **Data Warehouse连接**：本教程使用Snowflake连接，但您可以使用任何[支持的云仓库](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/access-prerequisites)。

让我们从[Data Warehouse连接](data-warehouse-connection.md)开始。
