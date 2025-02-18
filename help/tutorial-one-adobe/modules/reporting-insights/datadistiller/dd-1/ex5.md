---
title: 查询服务 — Power BI/Tableau
description: 查询服务 — Power BI/Tableau
kt: 5342
doc-type: tutorial
exl-id: 4c89fa24-44a5-4a9a-bb24-39ad4650c503
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 2.1.5从查询生成数据集

## 目标

了解如何从查询结果生成数据集
将Microsoft Power BI Desktop/Tableau直接连接到查询服务
在Microsoft Power BI桌面版/Tableau桌面版中创建报告

## 上下文

用于查询数据的命令行界面令人兴奋，但它并不表现良好。 在本课程中，我们将指导您完成一个推荐的工作流，介绍如何直接使用Microsoft Power BI Desktop/Tableau和查询服务为利益相关者创建可视化报表。

## 从SQL查询创建数据集

查询的复杂性将影响查询服务返回结果所需的时间。 并且当直接从命令行或其他解决方案(如Microsoft Power BI/Tableau)进行查询时，查询服务配置了5分钟超时（600秒）。 在某些情况下，这些解决方案将配置较短的超时。 为了运行较大的查询并提前加载返回结果所需的时间，我们提供了从查询结果生成数据集的功能。 此功能利用标准SQL功能，即“以选取方式创建表”(CTAS)。 查询列表在Platform UI中提供，也可以通过PSQL直接从命令行运行。

在上一个示例中，在PSQL中执行&#x200B;**之前，您已经使用自己的LDAP输入您的名称**。

```sql
select /* enter your name */
       e.--aepTenantId--.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l.--aepTenantId--.loyaltyDetails.level as loyaltystatus,
       l.--aepTenantId--.loyaltyDetails.points as loyaltypoints,
       l.--aepTenantId--.identification.core.crmId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_crm_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

导航到Adobe Experience Platform UI - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

您将在搜索字段中输入ldap，以便在Adobe Experience Platform查询UI中搜索已执行的语句：

选择&#x200B;**查询**，转到&#x200B;**日志**&#x200B;并在搜索字段中输入您的ldap。

![search-query-for-ctas.png](./images/searchqueryforctas.png)

选择您的查询，然后单击&#x200B;**以CTAS身份运行**。

![search-query-for-ctas.png](./images/searchqueryforctasa.png)

输入`--aepUserLdap-- Callcenter Interaction Analysis`作为数据集的名称和描述，然后单击&#x200B;**以CTAS**&#x200B;运行。

![create-ctas-dataset.png](./images/createctasdataset.png)

因此，您将看到状态为&#x200B;**已提交**&#x200B;的新查询。

![ctas-query-submitted.png](./images/ctasquerysubmitted.png)

完成后，您将看到&#x200B;**已创建数据集**&#x200B;的新条目（您可能需要刷新页面）。

![ctas-dataset-created.png](./images/ctasdatasetcreated.png)

创建数据集（可能需要5-10分钟）后，您可以继续此练习。

## 后续步骤

转到选项A： [2.1.6查询服务和Power BI](./ex6.md){target="_blank"}

转至选项B：[2.1.7查询服务和Tableau](./ex7.md){target="_blank"}

返回[查询服务](./query-service.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
