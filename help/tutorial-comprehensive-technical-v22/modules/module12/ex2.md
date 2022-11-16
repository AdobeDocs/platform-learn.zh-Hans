---
title: 使用BigQuery Source Connector在Adobe Experience Platform中摄取并分析Google Analytics数据 — 在BigQuery中创建第一个查询
description: 使用BigQuery Source Connector在Adobe Experience Platform中摄取并分析Google Analytics数据 — 在BigQuery中创建第一个查询
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73154afc-c3e3-420c-9471-5bb106dbfd02
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 12.2在BigQuery中创建第一个查询

## 目标

- 浏览BigQuery UI
- 在BigQuery中创建SQL查询
- 将SQL查询的结果保存在BigQuery的数据集中

## 上下文

当Google Analytics数据位于BigQuery中时，维度、量度和其他变量都会进行嵌套。 此外，Google Analytics数据每天会加载到不同的表中。 这意味着尝试将BigQuery中的Google Analytics表直接连接到Adobe Experience Platform非常困难，而且不是一个好主意。

解决此问题的方法是将Google Analytics数据转换为可读格式，以便更轻松地将摄取到Adobe Experience Platform中。

## 12.2.1创建一个数据集以保存新的BigQuery表

转到 [BigQuery控制台](https://console.cloud.google.com/bigquery).

![演示](./images/ex3/1.png)

在 **资源管理器**，您将看到您的项目ID。 单击您的项目ID(请勿单击 **bigquery-public-data** 数据集)。

![演示](./images/ex3/2.png)

您可以看到尚未数据集，因此现在让我们创建一个数据集。
单击 **创建数据集**.

![演示](./images/ex3/4.png)

在屏幕的右侧，您将看到 **创建数据集** 菜单。

![演示](./images/ex3/5.png)

对于 **数据集ID**，请使用以下命名约定。 对于其他字段，请保留默认设置。

| 命名 | 示例 |
| ----------------- | ------------- | 
| `--demoProfileLdap--_BigQueryDataSets` | vangeluw_BigQueryDataSets |

![演示](./images/ex3/6.png)

接下来，单击 **创建数据集**.

![演示](./images/ex3/7.png)

然后，您将在创建数据集后返回BigQuery控制台。

![演示](./images/ex3/8.png)

## 12.2.2创建您的第一个SQL BigQuery

接下来，您将在BigQuery中创建第一个查询。 此查询的目标是获取Google Analytics示例数据并进行转换，以便在Adobe Experience Platform中摄取该数据。 转到 **编辑器** 选项卡。

![演示](./images/ex3/9.png)

请复制以下SQL查询并将其粘贴到该查询编辑器中。 请随时阅读查询并了解Google AnalyticsBigQuery语法。


```sql
SELECT
  CONCAT(fullVisitorId, CAST(hitTime AS String), '-', hitNumber) AS _id,
  TIMESTAMP(DATETIME(Year_Current, Month_Current, Day_Current, Hour, Minutes, Seconds)) AS timeStamp,
  fullVisitorId as GA_ID,
  -- Fake CUSTOMER ID
  CONCAT('3E-D4-',fullVisitorId, '-1W-93F' ) as customerID,
  Page,
  Landing_Page,
  Exit_Page,
  Device,
  Browser,
  MarketingChannel,
  TrafficSource,
  TrafficMedium,
  -- Enhanced Ecommerce
  TransactionID,
  CASE
      WHEN EcommerceActionType = '2' THEN 'Product_Detail_Views'
      WHEN EcommerceActionType = '3' THEN 'Adds_To_Cart'
      WHEN EcommerceActionType = '4' THEN 'Product_Removes_From_Cart'
      WHEN EcommerceActionType = '5' THEN 'Product_Checkouts'
      WHEN EcommerceActionType = '6' THEN 'Product_Refunds'
    ELSE
    NULL
  END
     AS Ecommerce_Action_Type,
  -- Entrances (metric)
  SUM(CASE
      WHEN isEntrance = TRUE THEN 1
    ELSE
    0
  END
    ) AS Entries,
    
--Pageviews (metric)
    COUNT(*) AS Pageviews,
    
 -- Exits 
    SUM(
    IF
      (isExit IS NOT NULL,
        1,
        0)) AS Exits,
        
 --Bounces
   SUM(CASE
      WHEN isExit = TRUE AND isEntrance = TRUE THEN 1
    ELSE
    0
  END
    ) AS Bounces,
        
  -- Unique Purchases (metric)
  COUNT(DISTINCT TransactionID) AS Unique_Purchases,
  -- Product Detail Views (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '2' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Detail_Views,
  -- Product Adds To Cart (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '3' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Adds_To_Cart,
  -- Product Removes From Cart (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '4' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Removes_From_Cart,
  -- Product Checkouts (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '5' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Checkouts,
  -- Product Refunds (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '7' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Refunds
  FROM (
  SELECT
    -- Landing Page (dimension)
    CASE
      WHEN hits.isEntrance = TRUE THEN hits.page.pageTitle
    ELSE NULL
  END
    AS Landing_page,
    
        -- Exit Page (dimension)
    CASE
      WHEN hits.isExit = TRUE THEN hits.page.pageTitle
    ELSE
    NULL
  END
    AS Exit_page,
    
    hits.page.pageTitle AS Page,
    hits.isEntrance,
    hits.isExit,
    hits.hitNumber as hitNumber,
    hits.time as hitTime,
    date as Fecha,
    fullVisitorId,
    visitStartTime,
    device.deviceCategory AS Device,
    device.browser AS Browser,
    channelGrouping AS MarketingChannel,
    trafficSource.source AS TrafficSource,
    trafficSource.medium AS TrafficMedium,
    hits.transaction.transactionId AS TransactionID,
    CAST(EXTRACT(YEAR FROM CURRENT_DATE()) AS INT64) AS Year_Current,
    CAST(EXTRACT(MONTH FROM CURRENT_DATE()) AS INT64) AS Month_Current,
     CAST(EXTRACT(DAY FROM CURRENT_DATE()) AS INT64) AS Day_Current,
    CAST(EXTRACT(DAY FROM DATE_SUB(CURRENT_DATE(),INTERVAL 1 DAY)) AS INT64) AS Day_Current_Before,
    CAST(FORMAT_DATE('%Y', PARSE_DATE("%Y%m%d", date)) AS INT64) AS Year,
  CAST(FORMAT_DATE('%m', PARSE_DATE("%Y%m%d",date)) AS INT64) AS Month,
  CAST(FORMAT_DATE('%d', PARSE_DATE("%Y%m%d",date)) AS INT64) AS Day,
    CAST(EXTRACT (hour FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS Hour,
  CAST(EXTRACT (minute FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS Minutes,
  CAST(EXTRACT (second FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS SecondS,
    hits.eCommerceAction.action_type AS EcommerceActionType
  
  FROM
    `bigquery-public-data.google_analytics_sample.ga_sessions_*`,
     UNNEST(hits) AS hits
  WHERE
    _table_suffix BETWEEN '20170101'
    AND '20170331'
    AND totals.visits = 1
    AND hits.type = 'PAGE'
    )
    
GROUP BY
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9,
  10,
  11,
  12,
  13,
  14
    
  ORDER BY 2 DESC
```

准备就绪后，单击 **运行** 要运行查询，请执行以下操作：

![演示](./images/ex3/10.png)

执行查询可能需要几分钟。

查询运行完成后，您将在 **查询结果**.

![演示](./images/ex3/12.png)

## 12.2.3保存BigQuery SQL查询的结果

下一步是通过单击 **保存结果** 按钮。

![演示](./images/ex3/13.png)

作为输出的位置，选择 **BigQuery表**.

![演示](./images/ex3/14.png)

然后，您将看到一个新弹出窗口，其中 **项目名称** 和 **数据集名称** 已预填充。 数据集名称应为您在本练习开始时创建的数据集，且使用以下命名约定：

| 命名 | 示例 |
| ----------------- | ------------- | 
| `--demoProfileLdap--_BigQueryDataSets` | `vangeluw_BigQueryDataSets` |

您现在需要输入表名称。 请使用此命名约定：

| 命名 | 示例 |
| ----------------- |------------- | 
| `--demoProfileLdap--_GAdataTableBigQuery` | `vangeluw_GAdataTableBigQuery` |

![演示](./images/ex3/16.png)

单击&#x200B;**保存**。

在您创建的表中准备好数据之前，可能需要一些时间。 几分钟后，刷新浏览器。 然后，您应会在数据集中看到 `--demoProfileLdap--_GAdataTableBigquery` 表 **资源管理器** BigQuery项目内。

![演示](./images/ex3/19.png)

您现在继续下一个练习，您将在此练习中将此表连接到Adobe Experience Platform。

下一步： [12.3将GCP和BigQuery连接到Adobe Experience Platform](./ex3.md)

[返回到模块12](./customer-journey-analytics-bigquery-gcp.md)

[返回到所有模块](./../../overview.md)
