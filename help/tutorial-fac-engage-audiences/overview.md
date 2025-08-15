---
title: 使用联合受众构成吸引来自Data Warehouse的受众
description: 联合受众构成是一项强大的功能，它使数据架构师和数据工程师能够直接从第三方数据仓库构建和丰富受众。
breadcrumb-title: 概述
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 使用联合受众构成吸引来自Data Warehouse的受众

联合受众合成(FAC)是一项可用于Adobe Real-Time Customer Data Platform (Real-Time CDP)和Adobe Journey Optimizer环境的强大功能。 它使数据架构师和数据工程师能够直接从[受支持的企业数据仓库](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}策划和激活高价值受众，而无需将客户数据复制或移动到Adobe Experience Platform (AEP)。 这种可组合的CDP方法（一种为客户量身定制的解决方案）符合行业趋势，使企业能够利用其数据基础架构实现个性化的数字体验，同时维护数据治理。

## 业务上下文

SecurFinancial是一家领先的金融服务公司。 它跨完全不同的来源利用丰富的客户数据来对大量区段提供个性化的优惠和营销活动。 他们计划使用Adobe Real-Time CDP联合受众构成功能从他们的数据仓库中组织受众，同时将受众激活到Adobe Experience Platform的目标，并使用Adobe Journey Optimizer提供量身定制的解决方案以提供个性化的客户体验。

## 业务方案

SecurFinancial希望发起电子邮件营销活动，重新定位那些根据良好的信用获得预贷款资格，且SecurFinancial资产组合中没有有效贷款的客户。 虽然他们实时摄取在线行为数据，但在确定客户资格预审方面面临挑战，因为他们无法将信用信息摄取到AEP。 为了在不移动受限数据的情况下鉴别预认证客户，他们将使用联合受众构成丰富其AEP行为受众。

## 指南

本指南将演示我们如何支持SecureFinancial业务领域。 具体来说，它涵盖了我们如何让受众接触到需要这些受众的系统，包括S3存储帐户、在Journey Optimizer中开展电子邮件促销活动的历程，以及对获得预批准贷款的客户进行现场重新定位。

这些步骤包括：

1. 将Adobe Experience Platform连接到企业数据仓库。
2. 使用联合受众组合创建受众。
3. 将联合受众映射到外部Amazon S3目标。
4. 使用联合受众数据构建客户历程。
5. 使用联合数据丰富受众。
6. 在Edge上推动“即时”个性化。

## 先决条件

要在环境中执行类似活动，请确保您具有：

- 访问配置了Real-Time CDP或Journey Optimizer的Adobe Experience Platform帐户。
- 系统管理员权限或配置权限的功能。
- 熟悉Adobe Experience Platform概念，例如架构、数据集和受众(推荐：完成Experience League上的[Adobe Experience Platform播放列表简介](https://experienceleague.adobe.com/zh-hans/playlists/experience-platform-introduction?lang=en){target="_blank"})。
- 访问支持的[企业数据仓库](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}。
- 用于查询数据仓库的SQL的基本知识。
- **沙盒环境**：在您组织的实例中创建一个沙盒，以便在不影响生产数据的情况下安全地试验。
- **Data Warehouse连接**：本教程使用Snowflake连接，但您可以使用任何[受支持的Data Warehouse](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/access-prerequisites)。

首先，我们来回顾[联合受众组合的高级架构和流程](fac-architecture-and-flow.md)。
