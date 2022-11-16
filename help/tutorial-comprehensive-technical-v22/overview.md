---
title: 概述
description: 数据工程师、数据分析师、数据架构师、数据科学家、编排工程师和营销人员可以从中充分了解Adobe Experience Platform及其所有应用程序服务的业务价值。
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 2%

---

# Adobe Experience Platform 综合技术教程

## 概述

本教程是数据工程师、数据分析师、数据架构师、数据科学家、编排工程师和营销人员全面了解Adobe Experience Platform及其所有应用程序服务的业务价值的最佳起点。 每个课程都重点介绍当今复杂的个性化生态系统中企业面临的真正挑战，并分析Experience Platform如何在各种实践练习中解决该挑战。 请观看此视频，了解Adobe Experience Platform将帮助您解决的问题。

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

本教程的内容十分丰富，可在以下应用程序中提供清晰的分析：

- Adobe Experience Platform
- Adobe Experience Platform 数据收集
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

本教程不仅关注Adobe应用程序，还考虑了品牌运营的更广泛生态系统。 为了做到这一点，在一些课程中，重点是如何 _非Adobe_ 应用程序与Adobe Experience Platform集成。 因此，您将深入了解以下应用程序如何与Adobe Experience Platform一起使用：

- Amazon:AWS Lambda、AWS S3、AWSKinesis
- Google:Google Cloud Platform、Google BigQuery、Google Display&amp;Video 360、Google AdWords
- Microsoft:Power BI、Azure EventHub、Azure Blob Storage
- Salesforce:塔布洛
- 阿帕奇·卡夫卡
- Postman
- ...

完成本教程后，您将能够：

- 配置架构、混合、数据集和标识
- 在Adobe Experience Platform数据收集中配置Adobe Experience Platform数据收集属性并设置新的Web SDK扩展
- 使用Adobe Experience Platform数据收集、Google标签管理器或Amazon Alexa将数据实时流式传输到Adobe Experience Platform
- 使用工作流或使用提取、转换、加载(ETL)应用程序将数据批量摄取到Adobe Experience Platform
- 在Adobe Experience Platform中可视化和使用实时客户资料
- 创建区段
- 使用多个Adobe Experience Platform API
- 使用SQL在Adobe Experience Platform中查询数据
- 在Adobe Experience Platform中配置、训练和评分机器学习模型
- 使用Journey Orchestration配置基于触发器的实时历程
- 使用Real-time CDP通过将区段激活到各种目标来采取操作
- 使用Customer Journey Analytics报告来自各种来源的全方位客户数据，包括Google BigQuery

## 先决条件

- 访问 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Experience Platform数据收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 对演示系统的访问： [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 关于本教程

在这些课程中，您将使用支持多个行业的演示网站来实施Adobe Experience Platform和应用程序服务。 演示网站和移动设备应用程序具有丰富的数据层和功能，使您能够构建逼真的实施。 它提供对演示品牌(例如 **卢马**, **花旗信号**, **EXP新闻**, **MUTUAL365**, **卡韦洛** 还有几个。 您将在自己的Experience Cloud组织中构建自己的Adobe Experience Platform数据收集客户端资产，并将其映射到您的演示网站。 然后，将生成发送到您自己的Adobe Experience Platform实例的数据。

## 架构

在开始动手练习之前，请先查看本教程背后的架构。 正如您在上述概述中所看到的，本教程将深入介绍Adobe Experience Platform的多项特性和功能，但同时也将讨论跨多个源和目标的多个集成。 为了让您能够正确了解本教程背后的架构以及Adobe Experience Platform在您的企业生态系统中的整体定位，请首先查看架构视频和图表。

转到 [架构](./architecture.md).


## 视频

![视频](./assets/images/yt.jpeg)

您可以从我们的技术学院活动中找到许多有趣的视频，从Bootcamps，以及关于我们 [Experience Maker社区YouTube渠道](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

已创建多个视频，展示了Adobe Experience Platform与非Adobe应用程序之间支持和强大集成的元素。 单击以下链接以查找这些视频的概述。

转到 [视频](./videos.md).



## 如何衡量您完成的Adobe Experience Platform全面技术教程？

如果您以Adobe合作伙伴或Adobe员工的身份参与本教程，则需要在每个启用模块完成后提交您的进度。

您可以在此处找到提交完成的要求和流程： [测量完成](./completion.md)

## 内容

[0.入门](./modules/module0/getting-started.md)

- **受众：** Adobe Experience Platform综合技术教程的所有参与者
- **先决条件：** 访问演示系统下一步，Adobe Experience Platform和Adobe Experience Platform数据收集。 访问Adobe Experience Platform环境的默认配置ID。
- **描述：** 在此基础模块中，您将设置所有内容，以便您能够访问和使用演示环境。
- **时间投资：** 30分钟

[1. Foundation — 设置Adobe Experience Platform数据收集和Web SDK](./modules/module1/data-ingestion-launch-web-sdk.md)

- **受众：** 数据工程师，数据架构师
- **先决条件：** 访问Adobe Experience Platform和Adobe Experience Platform数据收集。
- **描述：** 在此基础模块中，您将了解Adobe Experience Platform数据收集和新的Web SDK扩展。
- **时间投资：** 30分钟

[2.基础 — 数据获取](./modules/module2/data-ingestion.md)

- **受众：** 数据工程师，数据架构师
- **先决条件：** 访问Adobe Experience Platform和Adobe Experience Platform数据收集。
- **描述：** 在此基础模块中，您将从网站将数据摄取到平台
- **时间投资：** 120分钟

[3.基础 — 实时客户资料](./modules/module3/real-time-customer-profile.md)

- **受众：** 数据工程师、数据架构师、营销人员
- **先决条件：** 访问Adobe Experience Platform和Postman
- **描述：** 在此基础模块中，您将通过使用UI和API来探索Adobe Experience Platform中的实时客户资料。
- **时间投资：** 90分钟
- **下载这些资产**:
   - [Postman收藏集](./assets/postman/postman_profile.zip)

[4.查询服务](./modules/module4/query-service.md)

- **受众：** 数据工程师、数据架构师、数据分析师、BI专家
- **先决条件：** 访问Adobe Experience Platform、查询服务、Power BI或表格
- **描述：** 在本模块中，您将学习如何使用Adobe Experience Platform查询服务。
- **时间投资：** 90分钟
- **下载这些资产**:
   - [JSON — 示例数据：演示系统 — 网站的事件数据集](./assets/json/ee.json)
   - [JSON — 示例数据：演示系统 — 呼叫中心事件数据集](./assets/json/callcenter.json)
   - [JSON — 示例数据：演示系统 — 用于获取忠诚度的用户档案数据集](./assets/json/loyalty.json)

[5.智能服务](./modules/module5/intelligent-services.md)

- **受众：** 数据工程师、数据架构师、数据科学家
- **先决条件：** 访问Adobe Experience Platform, Intelligent Services
- **描述：** 在本模块中，您将学习如何设置、配置和使用Adobe Experience Platform Intelligent Services。
- **时间投资：** 60分钟

[6. Real-Time CDP — 构建区段并执行操作](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **受众：** 数据架构师、编排工程师、营销人员
- **先决条件：** 对Adobe Experience Platform、Real-time CDP、Adobe Audience Manager、Adobe Target、AWS S3的访问
- **描述：** 在本模块中，您将配置一个区段，将其启用为流分段，并将该区段激活到多个目标，包括Google DV360、Google AdWords、Adobe Audience Manager、Adobe Target和S3目标，如SalesforceMarketing Cloud。
- **时间投资：** 90分钟

[7.Adobe Journey Optimizer:编排](./modules/module7/journey-orchestration-create-account.md)

- **受众：** 数据工程师、数据架构师、编排工程师
- **先决条件：** 访问Adobe Experience Platform和Adobe Journey Optimizer
- **描述：** 在本模块中，您将使用Adobe Journey Optimizer构建基于触发器的历程。
- **时间投资：** 60分钟

[8.Adobe Journey Optimizer:外部数据源和自定义操作](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **受众：** 数据工程师、数据架构师、编排工程师、营销人员
- **先决条件：** 访问Adobe Experience Platform、Adobe Journey Optimizer、Open Weather API、Twilio
- **描述：** 在本模块中，您将使用Adobe Journey Optimizer来监听客户行为（在线和离线），并通过各种渠道以智能、情境和实时方式对其做出响应。
- **时间投资：** 90分钟

[9.Adobe Journey Optimizer:offer decisioning](./modules/module9/offer-decisioning.md)

- **受众：** 数据工程师、数据架构师、编排工程师、营销人员
- **先决条件：** 访问Adobe Experience Platform和Offer decisioning
- **描述：** 在本模块中，您将以实际操作方式使用Adobe Experience Platform - Offers/Decisioning应用程序服务来配置个性化选件和您自己的选件活动。
- **时间投资：** 120分钟

[十、Adobe Journey Optimizer:基于事件的历程](./modules/module10/journeyoptimizer.md)

- **受众：** 电子邮件营销人员，编排专家，数据工程师，数据架构师，数据分析师
- **先决条件：** 访问Adobe Experience Platform和Journey Optimizer
- **描述：** 在本模块中，您将了解关于Journey Optimizer的所有信息，这有助于公司设计并向其客户提供连接、情境式和个性化的体验。
- **时间投资：** 120分钟

[十一、Customer Journey Analytics:在Adobe Experience Platform上使用Analysis Workspace构建功能板](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **受众：** 数据工程师、数据架构师、数据分析师
- **先决条件：** 访问Adobe Experience Platform和Customer Journey Analytics
- **描述：** 在本模块中，您将通过配置包含全渠道数据（如网站交互、移动设备应用程序交互、呼叫中心交互、店内交互等）的功能板，获取从在线到离线的分析。
- **时间投资：** 120分钟

[十二、Customer Journey Analytics:使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **受众：** 数据工程师、数据架构师、数据分析师
- **先决条件：** 访问Adobe Experience Platform、Customer Journey Analytics、Google云平台、Google BigQuery
- **描述：** 在本模块中，您将设置自己的Google云平台实例，在Google云平台中加载演示数据，然后使用BigQuery源连接器将该数据从Google云平台摄取到Adobe Experience Platform。 最后，您将使用Customer Journey Analytics来可视化该数据。
- **时间投资：** 120分钟
- **下载这些资产**:
   - [JSON — 示例数据：演示 — 忠诚度数据](./assets/json/bqLoyalty.json)

[十三、Real-Time CDP:区段激活到Microsoft Azure事件中心](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **受众：** 数据工程师、数据架构师、数据分析师
- **先决条件：** 访问Adobe Experience Platform、Real-time CDP和Microsoft Azure
- **描述：** 在本模块中，您将设置一个Microsoft Azure EventHub目标，作为Adobe Experience Platform实时CDP的实时目标。 您还将设置和部署Azure函数，当Adobe Experience Platform将区段有效负载发送到您的Azure EventHub目标时，该函数将实时触发。 您将触发的Azure函数将显示Adobe Experience Platform实时CDP激活功能的机制。
在本模块中，您还将了解哪些触发了实时CDP来将有效负载实际交付到指定目标。 我们还将讨论区段资格的状态以及它与激活的关系。
- **时间投资：** 90分钟

[14.Real-Time CDP连接：事件转发](./modules/module14/aep-data-collection-ssf.md)

- **受众：** 数据工程师、数据架构师、数据分析师
- **先决条件：** 对Real-Time CDP连接、标记和事件转发属性的访问
- **描述：** 在此模块中，您将使用之前配置的数据集、架构和Adobe Experience Platform数据收集属性来收集数据，然后将该数据服务器端转发到所选的端点。
- **时间投资：** 90分钟

[15.将数据从Apache Kafka流到Real-Time CDP](./modules/module15/aep-apache-kafka.md)

- **受众：** 数据分析师、数据工程师、数据架构师
- **先决条件：** 访问Adobe Experience Platform
- **描述：** 在本模块中，您将学习如何使用Adobe Experience Platform Sink Connector for Kafka Connect设置您自己的Apache Kafka群集，定义主题、制作者和消费者，并将数据流入Adobe Experience Platform。
- **时间投资：** 90分钟

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.
