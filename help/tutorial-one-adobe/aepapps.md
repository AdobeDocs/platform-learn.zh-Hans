---
title: AEP与应用程序技术实验室
description: AEP与应用程序技术实验室
doc-type: multipage-overview
source-git-commit: 245bb4738d72ee52ef7e99fcb099953153b7b781
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 1%

---

# 概述 — AEP与应用程序技术实验室

## 概述

## AEP与应用程序架构概述

在本视频中，您将了解本教程的Adobe Experience Platform和应用程序部分背后的架构。

>[!VIDEO](https://video.tv.adobe.com/v/3481415?quality=12&learn=on)

下载架构概述图像：

![技术内部人士](./assets/images/architecture_data.jpeg)

### 开始使用

[快速入门](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

在本基本模块中，您将准备所有内容，以便能够访问和使用演示环境。

### 交付和激活

#### 数据收集

[1.1基础 — Adobe Experience Platform数据收集和Web SDK的设置](./modules/delivery-activation/datacollection/dc1.1/data-ingestion-launch-web-sdk.md)

在此基础模块中，您将了解Adobe Experience Platform数据收集和新的Web SDK扩展。

[1.2 Foundation — 数据摄取](./modules/delivery-activation/datacollection/dc1.2/data-ingestion.md)

在此基础模块中，您将把来自各种来源的数据摄取到Adobe Experience Platform中

[1.3联合受众构成](./modules/delivery-activation/datacollection/dc1.3/fac.md)

在本模块中，您将学习如何使用联合数据设置联合受众模型并生成受众。

#### Real-Time CDP B2C

[2.1 Foundation — 实时客户资料](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/real-time-customer-profile.md)

在此基础模块中，您将利用UI和API来探索Adobe Experience Platform中的Real-time Customer Profile。

[2.2智能服务](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-2/intelligent-services.md)

在本模块中，您将学习如何设置、配置和使用Adobe Experience Platform智能服务。

[2.3 Real-Time CDP — 构建受众并采取行动](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/real-time-cdp-build-a-segment-take-action.md)

在本模块中，您将配置受众并将受众激活到多个目标，包括Google DV360、Adobe Target和AWS S3。

[2.4 Real-Time CDP：Audience Activation到Microsoft Azure活动中心](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

在本模块中，您将设置Microsoft Azure EventHub目标作为Adobe Experience Platform Real-time CDP的实时目标。

[2.5 Real-Time CDP连接：事件转发](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

在本模块中，您会将数据服务器端转发到多个端点，例如Google Cloud Platform Pub/Sub和AWS Kinesis。

[2.6将数据从Apache Kafka流式传输到Real-Time CDP](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

在本模块中，您将学习如何设置自己的Apache Kafka集群并将数据流式传输到Adobe Experience Platform。

### Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer：编排](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

在本模块中，您将使用Adobe Journey Optimizer构建基于触发器的历程。

[3.2 Adobe Journey Optimizer：外部数据源和自定义操作](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

在本模块中，您将使用Adobe Journey Optimizer在线和离线倾听客户行为，并通过各种渠道以智能、情境式和实时的方式对其进行响应。

[3.3 Adobe Journey Optimizer：推送和应用程序内消息](./modules/delivery-activation/ajo-b2c/ajob2c-3/ajopushinapp.md)

在本模块中，您将使用Adobe Journey Optimizer配置推送通知和应用程序内消息。

[3.4 Adobe Journey Optimizer：基于事件的历程](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

在本模块中，您将学习关于Journey Optimizer的所有须知内容，这有助于企业为其客户设计和提供互联、情境式和个性化的体验。

[3.5 Adobe Journey Optimizer：翻译服务](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

在本模块中，您将学习如何设置并使用Adobe Journey Optimizer中的翻译服务将消息本地化给客户。

[3.6 Adobe Journey Optimizer：内容管理](./modules/delivery-activation/ajo-b2c/ajob2c-6/ajocontent.md)

在本模块中，您将学习如何在Adobe Journey Optimizer中设置和使用内容卡和登陆页面，并将深入探讨Adobe Journey Optimizer与GenStudio for Performance Marketing之间的集成。

[3.7 Adobe Journey Optimizer： Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-7/ajo-decisioning.md)

在本模块中，您将学习如何在Adobe Journey Optimizer中设置和使用决策体验和基于代码的体验。

[3.8 Adobe Journey Optimizer：营销活动](./modules/delivery-activation/ajo-b2c/ajob2c-8/ajocampaigns.md)

在本模块中，您将学习如何在Adobe Journey Optimizer中设置和使用营销活动。

### 报表和分析

#### Adobe Customer Journey Analytics

[1.1 Customer Journey Analytics：使用Analysis Workspace在Adobe Experience Platform之上构建功能板](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

在本模块中，您将通过配置包含全渠道数据的功能板获得在线到离线洞察。

[1.2 Customer Journey Analytics：使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

在本模块中，您将设置自己的Google Cloud Platform实例，在Google Cloud Platform中加载演示数据，然后您将使用BigQuery Source Connector将该数据从Google Cloud Platform摄取到Adobe Experience Platform中。

#### 数据蒸馏器

[2.1查询服务](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

在本模块中，您将学习如何使用Adobe Experience Platform查询服务。

#### Content Analytics

[3.1Content Analytics](./modules/reporting-insights/content/module3.1/contentanalytics.md)

在本模块中，您将学习如何实施和使用Adobe Content Analytics。

![技术内部人士](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。