---
title: 概述
description: 面向数据工程师、数据分析师、数据架构师、数据科学家、编排工程师和营销人员的起点，全面了解Adobe Experience Platform及其所有应用程序服务的业务价值。
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: b46c753a8d854b5a448d10d30c7a5701900a35b8
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 2%

---

# Adobe Experience Platform 综合技术教程

## 概述

本教程是数据工程师、数据分析师、数据架构师、数据科学家、编排工程师和营销人员全面了解Adobe Experience Platform及其所有应用程序服务的业务价值的完美起点。 每个课程都关注当今复杂的个性化生态系统下企业面临的真正挑战，并细分Experience Platform如何在各种实践练习中解决该挑战。

本教程的内容非常多样，提供了对以下应用程序的清晰洞察：

- Adobe Experience Platform
- Adobe Experience Platform 数据收集
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

本教程不仅侧重于Adobe应用，还考虑了品牌运营的更广泛生态系统。 为此，在一些课程中，重点介绍了&#x200B;_非Adobe_&#x200B;应用程序如何与Adobe Experience Platform集成。 这样，您就可以深入了解以下应用程序如何与Adobe Experience Platform配合使用：

- Amazon：AWS Lambda、AWS S3、AWS Kinesis
- Google： Google Cloud Platform、Google BigQuery、Google Display&amp;Video 360、Google AdWords
- Microsoft：Power BI、Azure EventHub、Azure Blob Storage
- Salesforce： Tableau
- Apache Kafka
- Postman
- ...

完成本教程中的练习后，您将能够：

- 配置架构、字段组、数据集和标识
- 配置Adobe Experience Platform数据收集属性，并在Adobe Experience Platform数据收集中设置新的Web SDK扩展
- 使用Adobe Experience Platform数据收集将数据实时流式传输到Adobe Experience Platform
- 使用工作流或使用提取、转换、加载(ETL)应用程序将数据批量摄取到Adobe Experience Platform中
- 在Adobe Experience Platform中可视化并使用实时客户个人资料
- 创建区段
- 使用多个Adobe Experience Platform API
- 使用SQL在Adobe Experience Platform中查询数据
- 配置和运行基于触发器的实时历程
- 使用Real-time CDP激活到各种目的地的区段以采取行动
- 使用Customer Journey Analytics报告来自各种来源(包括Google BigQuery)的全渠道客户数据

## 先决条件

- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform数据收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 访问演示系统： [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

## 视频

您可在我们的[Experience Makers Community YouTube频道](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw)上从我们的技术学院活动、Bootcamp及其他视频中找到许多有趣的视频。

## 内容

[0.快速入门](./modules/gettingstarted/gettingstarted/getting-started.md)

- **受众：** Adobe Experience Platform综合技术教程的所有参与者
- **先决条件：**&#x200B;下一步访问演示系统、Adobe Experience Platform和Adobe Experience Platform数据收集。
- **描述：**&#x200B;在此基础模块中，您将设置所有内容，以便访问和使用演示环境。
- **时间投资：** 30分钟

### 1.数据收集

[1.1基础 — Adobe Experience Platform数据收集和Web SDK的设置](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **受众：**&#x200B;数据工程师、数据架构师
- **先决条件：**&#x200B;对Adobe Experience Platform和Adobe Experience Platform数据收集的访问权限。
- **描述：**&#x200B;在本基础模块中，您将了解Adobe Experience Platform数据收集和新的Web SDK扩展。
- **时间投资：** 30分钟

[1.2 Foundation — 数据摄取](./modules/datacollection/module1.2/data-ingestion.md)

- **受众：**&#x200B;数据工程师、数据架构师
- **先决条件：**&#x200B;对Adobe Experience Platform和Adobe Experience Platform数据收集的访问权限。
- **描述：**&#x200B;在此基础模块中，您将从网站中摄取数据到Platform
- **时间投资：** 120分钟

[1.3联合受众构成](./modules/datacollection/module1.3/fac.md)

- **受众：**&#x200B;数据分析师、数据工程师、数据架构师
- **先决条件：**&#x200B;访问Adobe Experience Platform
- **描述：**&#x200B;在本模块中，您将学习如何设置自己的Apache Kafka群集，定义主题、制作者和使用者，并使用Adobe Experience Platform Sink Connector for Kafka Connect将数据流式传输到Adobe Experience Platform。
- **时间投资：** 90分钟

### 2.Real-Time CDPB2C

[2.1 Foundation — 实时客户资料](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **受众：**&#x200B;数据工程师、数据架构师、营销人员
- **先决条件：**&#x200B;访问Adobe Experience Platform和Postman
- **描述：**&#x200B;在本基础模块中，您将使用UI和API来探索Adobe Experience Platform中的Real-time Customer Profile。
- **时间投资：** 90分钟
- **下载这些资源**：
   - [Postman收藏集](./assets/postman/postman_profile.zip)

[2.2智能服务](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **受众：**&#x200B;数据工程师、数据架构师、数据科学家
- **先决条件：**&#x200B;访问Adobe Experience Platform、智能服务
- **描述：**&#x200B;在本模块中，您将学习如何设置、配置和使用Adobe Experience Platform Intelligent Services。
- **时间投资：** 60分钟

[2.3 Real-Time CDP — 构建区段并采取行动](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **受众：**&#x200B;数据架构师、编排工程师、营销人员
- **先决条件：**&#x200B;访问Adobe Experience Platform、Real-time CDP、Adobe Audience Manager、Adobe Target、AWS S3
- **描述：**&#x200B;在本模块中，您将配置区段，启用该区段进行流式分段，并将区段激活到多个目标，包括Google DV360、Google AdWords、Adobe Audience Manager、Adobe Target和SalesforceMarketing Cloud等S3目标。
- **时间投资：** 90分钟

[2.4 Real-Time CDP：将区段激活激活到Microsoft Azure事件中心](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **受众：**&#x200B;数据工程师、数据架构师、数据分析师
- **先决条件：**&#x200B;访问Adobe Experience Platform、Real-time CDP和Microsoft Azure
- **描述：**在本模块中，您将设置Microsoft Azure EventHub目标作为Adobe Experience Platform Real-time CDP的实时目标。 您还将设置和部署一个Azure函数，每当Adobe Experience Platform将区段有效负载交付到Azure EventHub目标时，该函数都将实时触发。 您将触发的Azure函数将显示Adobe Experience Platform Real-time CDP激活功能的机制。
在本模块中，您还将了解什么会触发Real-time CDP将有效负载实际传送到指定目标。 我们还将讨论区段鉴定的状态以及它与激活的关系。
- **时间投资：** 90分钟

[2.5 Real-Time CDP连接：事件转发](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **受众：**&#x200B;数据工程师、数据架构师、数据分析师
- **先决条件：**&#x200B;对Real-Time CDP连接、标记和事件转发属性的访问权限
- **描述：**&#x200B;在本模块中，您将使用以前配置的数据集、架构和Adobe Experience Platform数据收集属性来收集数据，然后将该数据服务器端转发到所选的端点。
- **时间投资：** 90分钟

[2.6将数据从Apache Kafka流式传输到Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **受众：**&#x200B;数据分析师、数据工程师、数据架构师
- **先决条件：**&#x200B;访问Adobe Experience Platform
- **描述：**&#x200B;在本模块中，您将学习如何设置自己的Apache Kafka群集，定义主题、制作者和使用者，并使用Adobe Experience Platform Sink Connector for Kafka Connect将数据流式传输到Adobe Experience Platform。
- **时间投资：** 90分钟

### 3.Adobe Journey OptimizerB2C

[3.1 Adobe Journey Optimizer：编排](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **受众：**&#x200B;数据工程师、数据架构师、编排工程师
- **先决条件：**&#x200B;访问Adobe Experience Platform和Adobe Journey Optimizer
- **描述：**&#x200B;在本模块中，您将使用Adobe Journey Optimizer构建基于触发器的历程。
- **时间投资：** 60分钟

[3.2 Adobe Journey Optimizer：外部数据源和自定义操作](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **受众：**&#x200B;数据工程师、数据架构师、编排工程师、营销人员
- **先决条件：**&#x200B;访问Adobe Experience Platform、Adobe Journey Optimizer、开放天气API、Twilio
- **描述：**&#x200B;在本模块中，您将使用Adobe Journey Optimizer在线和离线侦听客户行为，并通过各种渠道以智能、情境式和实时的方式对其进行响应。
- **时间投资：** 90分钟

[3.3 Adobe Journey Optimizer：Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **受众：**&#x200B;数据工程师、数据架构师、编排工程师、营销人员
- **先决条件：**&#x200B;访问Adobe Experience Platform和Offer decisioning
- **描述：**&#x200B;在本模块中，您将以实践方式使用Adobe Experience Platform - Offers/Decisioning应用程序服务来配置个性化优惠和您自己的优惠活动。
- **时间投资：** 120分钟

[3.4 Adobe Journey Optimizer：基于事件的历程](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **受众：**&#x200B;电子邮件营销人员、编排专家、数据工程师、数据架构师、数据分析师
- **先决条件：**&#x200B;访问Adobe Experience Platform和Journey Optimizer
- **描述：**&#x200B;在本模块中，您将学习关于Journey Optimizer的所有知识，这有助于公司为其客户设计和提供互联、情境式和个性化的体验。
- **时间投资：** 120分钟

### 4.Adobe Customer Journey Analytics

[4.1Customer Journey Analytics：使用Analysis Workspace在Adobe Experience Platform之上构建功能板](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **受众：**&#x200B;数据工程师、数据架构师、数据分析师
- **先决条件：**&#x200B;访问Adobe Experience Platform和Customer Journey Analytics
- **描述：**&#x200B;在本模块中，通过配置包含全渠道数据（如网站交互、移动设备应用程序交互、呼叫中心交互、店内交互等）的仪表板，您将获得从在线到离线的洞察。
- **时间投资：** 120分钟

[4.2Customer Journey Analytics：使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **受众：**&#x200B;数据工程师、数据架构师、数据分析师
- **先决条件：**&#x200B;对Adobe Experience Platform、Customer Journey Analytics、Google Cloud Platform、Google BigQuery的访问权限
- **描述：**&#x200B;在本模块中，您将设置自己的Google Cloud Platform实例，在Google Cloud Platform中加载演示数据，然后使用BigQuery Source Connector将该数据从Google Cloud Platform摄取到Adobe Experience Platform中。 最后，您将使用Customer Journey Analytics来可视化这些数据。
- **时间投资：** 120分钟
- **下载这些资源**：
   - [JSON — 示例数据：演示 — 忠诚度数据](./assets/json/bqLoyalty.json)

### 5.数据Distiller

[5.1查询服务](./modules/datadistiller/module5.1/query-service.md)

- **受众：**&#x200B;数据工程师、数据架构师、数据分析师、BI专家
- **先决条件：**&#x200B;对Adobe Experience Platform、查询服务、Power BI或Tableau的访问权限
- **描述：**&#x200B;在本模块中，您将学习如何使用Adobe Experience Platform查询服务。
- **时间投资：** 90分钟
- **下载这些资源**：
   - [JSON — 示例数据：演示系统 — 网站的事件数据集](./assets/json/ee.json)
   - [JSON — 示例数据：演示系统 — 呼叫中心的事件数据集](./assets/json/callcenter.json)
   - [JSON — 示例数据：演示系统 — 忠诚度用户档案数据集](./assets/json/loyalty.json)





