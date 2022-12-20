---
title: 运行查询
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 运行查询
description: 在本课程中，您将学习如何设置、写入和执行查询以验证您摄取的数据。
role: Data Architect, Data Engineer
feature: Queries
kt: 4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 2%

---

# 运行查询

<!-- 15 min-->
在本课程中，您将学习如何设置、写入和执行查询以验证您摄取的数据。

Adobe Experience Platform查询服务允许您使用标准SQL在Platform中查询数据，从而帮助您理解数据。 使用查询服务，您可以加入数据湖中的任何数据集，并作为新数据集捕获查询结果，以用于报表、机器学习或将查询结果摄取到实时客户配置文件中。

**数据架构师** 和 **数据工程师** 将需要在本教程之外使用查询服务。

在开始练习之前，请观看此简短视频，进一步了解查询服务：
>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 简单查询

让我们从一些简单的查询开始：

1. 在Platform用户界面中，转到 **查询** 在左侧导航中
1. 选择 **创建查询** 按钮以打开要运行和执行查询的文本框
1. 在编辑器中输入以下查询，然后按Shift+Enter或Shift+Return以执行查询。

   ```
   SHOW TABLES
   ```

1. 这会显示可用表的列表

   ![显示表查询](assets/queries-showTables.png)


1. 现在尝试使用此查询，替换 `_techmarketingdemos` 具有您自己的租户命名空间，如果您回想，该命名空间在您的架构中可见。

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![从忠诚度数据集中选择数据](assets/queries-loyaltySelect.png)

1. 如果存在任何错误，则会在 **[!UICONTROL 控制台]** 选项卡，如下图所示
   ![查询中出错](assets/queries-error.png)

1. 通过成功的查询， **[!UICONTROL 名称]** it `Luma Gold Level Customers`
1. 选择 **[!UICONTROL 保存]** 按钮
   ![保存查询](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## 其他练习

稍后将向教程中添加其他查询服务练习。
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## 其他资源

* [查询服务文档](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hans)
* [查询服务API引用](https://www.adobe.io/experience-platform-apis/references/query-service/)

最后一堂实习课， [创建区段](build-segments.md)!
