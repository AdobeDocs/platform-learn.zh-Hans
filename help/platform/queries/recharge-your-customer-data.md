---
title: 为您的客户数据重新充电，以提供令人兴奋的体验
description: 了解如何通过在多个用例中使用相同的数据来减轻低质量数据的影响、缩短实现价值的时间并增加ROI。
role: Data Engineer, Data Architect, Developer
feature: Queries
kt: 10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# 为您的客户数据重新充电，以提供令人兴奋的体验

全渠道数据是加强营销人员用于编排激活和衡量所产生客户旅程的可操作客户用户档案的关键要素。 但是，在管理此数据的质量、规模和种类方面，组织面临着挑战。 他们需要简化的解决方案来减轻低质量数据的影响、缩短价值实现时间，并通过在多个用例中使用相同的数据来增加ROI。

本视频探讨：

* Adobe Experience Platform数据准备功能
* 提高Adobe Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics的ROI

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

有关详细信息，请访问 [查询服务文档](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hans).

>[!NOTE]
>
>此视频是Adobe Summit2020会话的摘录 *[为体验充电而充电的全渠道数据](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
