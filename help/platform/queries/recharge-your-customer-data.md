---
title: 为您的客户数据重新充电，以提供令人振奋的体验
description: 了解如何减轻低质量数据的影响，缩短实现价值的时间，并通过在多种用例中使用相同的数据来提高ROI。
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 为您的客户数据重新充电，以提供令人振奋的体验

全渠道数据是支持营销人员用于编排激活和衡量所生成客户历程的可操作客户配置文件的关键要素。 但是，各组织在管理此类数据的质量、规模和多样性方面仍面临挑战。 它们需要简化的解决方案来减轻低质量数据的影响，缩短实现价值的时间，并通过在多种用例中使用相同的数据来提高ROI。
有关详细信息，请访问[查询服务文档](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hans)。

本视频探讨了以下内容：

* 您可以利用的Adobe Experience Platform数据准备功能
* 提高Adobe Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics的ROI

>[!VIDEO](https://video.tv.adobe.com/v/342533?learn=on&enablevpops)

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

>[!NOTE]
>
>此视频摘录自Adobe Summit 2020会话&#x200B;*[为体验注入电力的全渠道数据](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*。
