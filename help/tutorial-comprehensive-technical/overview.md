---
title: 概述 — AEP和应用程序的全面技术教程
description: 面向数据工程师、数据分析师、数据架构师、数据科学家、编排工程师和营销人员的起点，全面了解Adobe Experience Platform及其所有应用程序服务的业务价值。
doc-type: multipage-overview
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: 24b0b774fe19e5938555491b3dc9d04717bb95c6
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 2%

---

# Adobe Experience Platform 综合技术教程

![技术内部人士](./assets/images/techinsiders.png){width="50px" align="left"}

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
- 在Adobe Experience Platform数据收集中配置Adobe Experience Platform数据收集属性，并设置新的Web SDK扩展
- 使用Adobe Experience Platform数据收集将数据实时流式传输到Adobe Experience Platform
- 使用工作流或使用提取、转换、加载(ETL)应用程序将数据批量摄取到Adobe Experience Platform中
- 在Adobe Experience Platform中可视化并使用实时客户个人资料
- 创建受众
- 使用多个Adobe Experience Platform API
- 使用SQL在Adobe Experience Platform中查询数据
- 配置和运行基于触发器的实时历程
- 使用Real-time CDP激活受众到各种目标以采取行动
- 使用Customer Journey Analytics报告来自各种来源(包括Google BigQuery)的全渠道客户数据

## 先决条件

如果您要使用自己的Adobe Experience Platform实例来参加本教程，请按照[此处](./setup.md)的说明来准备您的组织以参加本教程。

- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform数据收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 访问演示系统： [https://dsn.adobe.com/](https://dsn.adobe.com/)

## 视频

您可在我们的[Experience Makers社区YouTube频道](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw)的Tech Academy网络研讨会、训练营等视频中找到许多有趣的视频。

## 完成和认证

本教程是Adobe认证课程的一部分。 您可以转到[https://certification.adobe.com/courses/1258](https://certification.adobe.com/courses/1258)同时注册课程和本教程。

对于您使用以下教程完成的每个模块，您需要按照[此处](./completion.md)的指示提交完成证明。

## 内容

要检查以下内容的状态，请转到[状态页面](./status.md)。

[0.快速入门](./modules/gettingstarted/gettingstarted/getting-started.md)

在此基础模块中，您将设置所有内容，以便能够访问和使用演示环境。

**时间投资：** 30分钟

### 1.数据收集

[1.1基础 — Adobe Experience Platform数据收集和Web SDK的设置](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

在此基础模块中，您将了解Adobe Experience Platform数据收集和新的Web SDK扩展。

**时间投资：** 30分钟

[1.2 Foundation — 数据摄取](./modules/datacollection/module1.2/data-ingestion.md)

在此基础模块中，您将把来自各种来源的数据摄取到Adobe Experience Platform中

**时间投资：** 120分钟

[1.3联合受众构成](./modules/datacollection/module1.3/fac.md)

在本模块中，您将学习如何使用联合数据设置联合受众模型并生成受众。

**时间投资：** 90分钟

### 2.Real-Time CDPB2C

[2.1 Foundation — 实时客户资料](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

在此基础模块中，您将利用UI和API来探索Adobe Experience Platform中的Real-time Customer Profile。

**时间投资：** 90分钟

[2.2智能服务](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

在本模块中，您将学习如何设置、配置和使用Adobe Experience Platform智能服务。

**时间投资：** 60分钟

[2.3 Real-Time CDP — 构建受众并采取行动](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

在本模块中，您将配置受众并将受众激活到多个目标，包括Google DV360、Adobe Target和AWS S3。

**时间投资：** 90分钟

[2.4 Real-Time CDP：Audience Activation到Microsoft Azure事件中心](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

在本模块中，您将设置Microsoft Azure EventHub目标作为Adobe Experience Platform Real-time CDP的实时目标。 您还将设置和部署一个Azure函数，每当Adobe Experience Platform将受众有效负载交付到Azure EventHub目标时，该函数都将实时触发。 您将触发的Azure函数将显示Adobe Experience Platform Real-time CDP激活功能的机制。
在本模块中，您还将了解什么会触发Real-time CDP将有效负载实际传送到指定目标。 我们还将讨论受众资格的状态以及它与激活的关系。

**时间投资：** 90分钟

[2.5 Real-Time CDP连接：事件转发](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

在本模块中，您将使用之前配置的数据集、架构和Adobe Experience Platform数据收集属性来收集数据，然后将该数据服务器端转发到多个端点，例如Google Cloud Platform Pub/Sub和AWS Kinesis。

**时间投资：** 90分钟

[2.6将数据从Apache Kafka流式传输到Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

在本模块中，您将学习如何设置自己的Apache Kafka集群，定义主题、制作者和消费者，并使用适用于Kafka Connect的Adobe Experience Platform Sink Connector将数据流式传输到Adobe Experience Platform。

**时间投资：** 90分钟

### 3.Adobe Journey OptimizerB2C

[3.1 Adobe Journey Optimizer：编排](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

在本模块中，您将使用Adobe Journey Optimizer构建基于触发器的历程。

**时间投资：** 60分钟

[3.2 Adobe Journey Optimizer：外部数据源和自定义操作](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

在本模块中，您将使用Adobe Journey Optimizer在线和离线倾听客户行为，并通过各种渠道以智能、情境式和实时的方式对其进行响应。

**时间投资：** 90分钟

[3.3 Adobe Journey Optimizer：Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

在本模块中，您将使用Adobe Experience Platform - Offers/Decisioning应用程序服务以实践方式配置个性化优惠和您自己的优惠活动。

**时间投资：** 120分钟

[3.4 Adobe Journey Optimizer：基于事件的历程](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

在本模块中，您将学习关于Journey Optimizer的所有须知内容，这有助于企业为其客户设计和提供互联、情境式和个性化的体验。

**时间投资：** 120分钟

[3.5 Adobe Journey Optimizer：翻译服务](./modules/ajo-b2c/module3.5/ajotranslationsvcs.md)

在本模块中，您将学习如何设置并使用Adobe Journey Optimizer中的翻译服务将消息本地化给客户。

**时间投资：** 60分钟

### 4.Adobe Customer Journey Analytics

[4.1Customer Journey Analytics：使用Analysis Workspace在Adobe Experience Platform之上构建功能板](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

在本模块中，通过配置包含全渠道数据（如网站交互、移动设备应用程序交互、呼叫中心交互、店内交互等）的仪表板，您将获得在线和离线洞察。

**时间投资：** 120分钟

[4.2Customer Journey Analytics：使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

在本模块中，您将设置自己的Google Cloud Platform实例，在Google Cloud Platform中加载演示数据，然后您将使用BigQuery Source Connector将该数据从Google Cloud Platform摄取到Adobe Experience Platform中。 最后，您将使用Customer Journey Analytics来可视化这些数据。

**时间投资：** 120分钟

### 5.数据Distiller

[5.1查询服务](./modules/datadistiller/module5.1/query-service.md)

在本模块中，您将学习如何使用Adobe Experience Platform查询服务。

**时间投资：** 90分钟

![技术内部人士](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。
