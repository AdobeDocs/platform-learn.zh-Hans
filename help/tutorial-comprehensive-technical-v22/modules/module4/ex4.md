---
title: 查询服务 — Power BI/表格
description: 查询服务 — Power BI/表格
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 11525d05-1c19-4d41-8f47-4feb3e8aed66
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 4.4从查询生成数据集

## 目标

了解如何从查询结果生成Power BI集将MicrosoftPower BI桌面/表格直接连接到查询服务在Microsoft桌面/表格桌面中创建报表

## 课程上下文

用于查询数据的命令行界面令人兴奋，但它不太好。 在本课程中，我们将指导您完成推荐的工作流程，了解如何直接使用MicrosoftPower BI桌面/表格服务为利益相关方创建可视化报表。

## 4.4.1通过SQL查询创建数据集

查询的复杂性将影响查询服务返回结果所花费的时长。 而且，直接从命令行或其他解决方案(如MicrosoftPower BI/表格)进行查询时，查询服务会配置5分钟超时（600秒）。 在某些情况下，这些解决方案将配置更短的超时时间。 要运行较大的查询并提前加载返回结果所花费的时间，我们提供了一项功能，用于从查询结果生成数据集。 此功能利用标准的SQL功能，即创建表为选择(CTAS)。 它可在Platform UI的查询列表中使用，也可以直接通过PSQL的命令行运行。

在前一个 **输入您的姓名** 在PSQL中执行LDAP之前，将其与自己的ldap一起使用。

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
       l.--aepTenantId--.identification.core.loyaltyId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_loyalty_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

导航到Adobe Experience Platform UI - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

通过在搜索字段中输入ldap，您将在Adobe Experience Platform查询UI中搜索已执行的语句：

选择 **查询**，转到 **日志** 并在搜索字段中输入ldap。

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

选择查询并单击 **输出数据集**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

输入 `--demoProfileLdap-- Callcenter Interaction Analysis` 作为数据集的名称和描述，然后按 **运行查询** 按钮

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

因此，您将看到一个状态为的新查询 **已提交**.

![ctas-query-submitted.png](./images/ctas-query-submitted.png)

完成后，您将看到 **已创建数据集** （您可能需要刷新页面）。

![ctas-dataset-created-png](./images/ctas-dataset-created.png)

创建数据集后（可能需要5-10分钟），您可以继续练习。

下一步 — 选项A: [4.5查询服务和Power BI](./ex5.md)

下一步 — 选项B: [4.6查询服务和表格](./ex6.md)

[返回到模块4](./query-service.md)

[返回到所有模块](../../overview.md)
