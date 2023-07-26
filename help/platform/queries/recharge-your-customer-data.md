---
title: 为您的客户数据重新充电，以提供令人振奋的体验
description: 了解如何减轻低质量数据的影响，缩短实现价值的时间，并通过在多种用例中使用相同的数据来提高ROI。
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 42427df298e2c5ae734ce050e935378db51e66a1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# 为您的客户数据重新充电，以提供令人振奋的体验

全渠道数据是支持营销人员用于编排激活和衡量所生成客户历程的可操作客户配置文件的关键要素。 但是，各组织在管理此类数据的质量、规模和多样性方面仍面临挑战。 它们需要简化的解决方案来减轻低质量数据的影响，缩短实现价值的时间，并通过在多种用例中使用相同的数据来提高ROI。

本视频探讨了以下内容：

* 您可以利用的Adobe Experience Platform数据准备功能
* 从Adobe Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics中提高ROI

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## SQL示例

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

欲知更多信息，请访问 [查询服务文档](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hans).

>[!NOTE]
>
>本视频摘自Adobe Summit2020会话 *[为体验充电全渠道数据](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
