---
title: 概述 — 全面的技术教程 — 一个Adobe
description: 全面的技术教程 — 一个Adobe
doc-type: multipage-overview
exl-id: 5bc0d621-0662-4d94-80a0-b6c173c0ac9e
source-git-commit: 9169b0f9be7f192fd7e16ddcc2ae32f6a8cca92c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# 全面的技术教程 — 一个Adobe

![技术内部人士](./assets/images/techinsiders.png){width="50px" align="left"}

## 概述

本教程的内容非常多样，提供了对以下应用程序的清晰洞察：

- Adobe Firefly服务
- Adobe Photoshop
- Adobe Workfront和Adobe Workfront Fusion
- Adobe Experience Manager Cloud Service、Sites、Assets和Edge Delivery Services
- Adobe Experience Platform
- Adobe Real-Time CDP
- Adobe Journey Optimizer


本教程不仅关注Adobe应用程序，还考虑到品牌运营的更广泛生态系统。 为此，在一些课程中，重点关注非Adobe应用程序如何与Adobe应用程序集成。 这样，您就可以深入了解以下应用程序如何与Adobe Experience Platform配合使用：

- Amazon AWS
- Google Cloud Platform
- Microsoft Azure
- Postman
- Snowflake
- ...

## 先决条件

如果您希望使用自己的Adobe Experience Cloud实例来参加本教程，则需要在您的实例中配置以下应用程序，并且您需要能够访问：

- Adobe Firefly [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}
- Adobe Photoshop
- Adobe Workfront
- Adobe Workfront Fusion [https://fusion.adobe.com/](https://fusion.adobe.com/){target="_blank"}
- Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform){target="_blank"}
- Adobe Experience Platform数据收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}
- 访问演示系统： [https://dsn.adobe.com/](https://dsn.adobe.com/){target="_blank"}

## 完成和认证

本教程是Adobe认证课程的一部分。 您可以转到[https://certification.adobe.com](https://certification.adobe.com)同时注册课程和本教程。

对于您使用以下教程完成的每个模块，您需要按照[此处](./completion.md)的指示提交完成证明。

## 内容状态

要检查以下内容的状态，请转到[状态页面](./status.md){target="_blank"}。

### 开始使用

[快速入门](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

在本基本模块中，您将准备所有内容，以便能够访问和使用演示环境。

### 1.工作流程和规划

### 2.创建与生产

[1.1 Adobe Firefly Services](./modules/creation-production/module1.1/firefly-services.md){target="_blank"}

在本模块中，您将使用Adobe Firefly Services API、Photoshop API和Microsoft Azure Storage Services生成图像并以编程方式存储这些图像。

[1.2使用Workfront Fusion实现创意工作流程自动化](./modules/creation-production/module1.2/automation.md){target="_blank"}

在此基础模块中，您将使用Adobe Workfront Fusion来自动化和扩展内容创建工作流。

### 3.资产管理

[1.1 Adobe Experience Manager Cloud Service和Edge Delivery Services](./modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}

在此基础模块中，您将设置Adobe Experience Manager Cloud Service项目、站点和Assets存储库。

使用Adobe Workfront进行[1.2工作流管理](./modules/asset-mgmt/module2.2/workfront.md){target="_blank"}

在本基本模块中，您将配置和使用Adobe Workfront来管理审批流程，并将使用与Adobe Experience Manager Assets、通用编辑器、Photoshop等的集成。

### 4.交付和激活

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

[2.4 Real-Time CDP：Audience Activation到Microsoft Azure事件中心](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

在本模块中，您将设置Microsoft Azure EventHub目标作为Adobe Experience Platform Real-time CDP的实时目标。

[2.5 Real-Time CDP连接：事件转发](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

在本模块中，您会将数据服务器端转发到多个端点，例如Google Cloud Platform Pub/Sub和AWS Kinesis。

[2.6将数据从Apache Kafka流式传输到Real-Time CDP](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

在本模块中，您将学习如何设置自己的Apache Kafka集群并将数据流式传输到Adobe Experience Platform。

#### Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer：编排](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

在本模块中，您将使用Adobe Journey Optimizer构建基于触发器的历程。

[3.2 Adobe Journey Optimizer：外部数据源和自定义操作](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

在本模块中，您将使用Adobe Journey Optimizer在线和离线倾听客户行为，并通过各种渠道以智能、情境式和实时的方式对其进行响应。

[3.3Adobe Journey Optimizer： Offer Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md)

在本模块中，您将使用Adobe Journey Optimizer配置个性化优惠和您自己的优惠决策。

[3.4 Adobe Journey Optimizer：基于事件的历程](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

在本模块中，您将学习关于Journey Optimizer的所有须知内容，这有助于企业为其客户设计和提供互联、情境式和个性化的体验。

[3.5 Adobe Journey Optimizer：翻译服务](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

在本模块中，您将学习如何设置并使用Adobe Journey Optimizer中的翻译服务将消息本地化给客户。

### 5.报表和见解

#### Adobe Customer Journey Analytics

[1.1 Customer Journey Analytics：使用Analysis Workspace在Adobe Experience Platform之上构建功能板](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

在本模块中，您将通过配置包含全渠道数据的功能板获得在线到离线洞察。

[1.2 Customer Journey Analytics：使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

在本模块中，您将设置自己的Google Cloud Platform实例，在Google Cloud Platform中加载演示数据，然后您将使用BigQuery Source Connector将该数据从Google Cloud Platform摄取到Adobe Experience Platform中。

#### 数据蒸馏器

[2.1查询服务](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

在本模块中，您将学习如何使用Adobe Experience Platform查询服务。

![技术内部人士](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。
