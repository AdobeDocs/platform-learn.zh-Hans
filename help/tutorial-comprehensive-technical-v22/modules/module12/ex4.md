---
title: 使用BigQuery Source Connector在Adobe Experience Platform中摄取并分析Google Analytics数据 — 将数据从BigQuery加载到Adobe Experience Platform
description: 使用BigQuery Source Connector在Adobe Experience Platform中摄取并分析Google Analytics数据 — 将数据从BigQuery加载到Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 150df432-e87a-402a-b821-ca9e33c5fd80
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 3%

---

# 12.4将数据从BigQuery加载到Adobe Experience Platform

## 目标

- 将BigQuery数据映射到XDM架构
- 将BigQuery数据加载到Adobe Experience Platform
- 熟悉BigQuery Source Connector UI

## 开始之前

在练习12.3后，您应该在Adobe Experience Platform中打开此页面：

![演示](./images/datasets.png)

**如果已打开，请继续练习12.4.1。**

**如果没有打开，请转到 [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

在左侧菜单中，转到“源”。 然后您将看到 **源** 主页。 在 **源** 菜单，单击 **数据库**.

![演示](./images/sourceshome.png)

选择 **Google BigQuery** 源连接器并单击 **+配置**.

![演示](./images/bq.png)

然后，您将看到Google BigQuery帐户选择屏幕。

![演示](./images/0-c.png)

选择您的帐户并单击 **下一个**.

![演示](./images/ex4/0-d.png)

然后您将看到 **添加数据** 中。

![演示](./images/datasets.png)

## 12.4.1 BigQuery表选择

在 **添加数据** 查看，选择BigQuery数据集。

![演示](./images/datasets.png)

您现在可以在BigQuery中查看Google Analytics数据的示例数据预览。

单击&#x200B;**下一步**。

![演示](./images/ex4/3.png)

## 12.4.2 XDM映射

您现在将看到以下内容：

![演示](./images/xdm4a.png)

现在，您必须创建新数据集或选择现有数据集才能将Google Analytics数据加载到中。 在本练习中，已创建数据集和架构。 您无需创建新架构或数据集。

选择 **现有数据集**. 打开下拉菜单以选择数据集。 搜索名为的数据集 `Demo System - Event Dataset for BigQuery (Global v1.1)` 并选择它。 单击&#x200B;**下一步**。

![演示](./images/xdm6.png)

向下滚动。 您现在需要映射 **源字段** 从Google Analytics/BigQuery到XDM **目标字段**，按字段。

![演示](./images/xdm8.png)

在本练习中使用以下映射表。

| 源字段 | 目标字段 |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | channel._id |
| timeStamp | timestamp |
| GA_ID | ``--aepTenantId--``.identification.core.gaid |
| customerID | ``--aepTenantId--``.identification.core.loytactId |
| 页面 | web.webPageDetails.name |
| 设备 | device.type |
| 浏览器 | environment.browserDetails.vendor |
| 营销渠道 | marketing.trackingCode |
| 流量源 | channel.typeAtSource |
| TrafficMedium | channel.mediaType |
| 交易ID | commerce.order.payments.transactionID |
| Ecommerce_Action_Type | eventType |
| 页面查看次数 | web.webPageDetails.pageViews.value |
| Unique_Purchases | commerce.purchases.value |
| Product_Detail_Views | commerce.productViews.value |
| Adds_To_Cart | commerce.productListAdds.value |
| Product_Removes_From_Cart | commerce.productListRemovals.value |
| Product_Checkouts | commerce.checkouts.value |

将上述映射复制并粘贴到Adobe Experience Platform UI中后，请验证您是否因拼写错误或前导/尾随空格而看不到任何错误。

您现在拥有 **映射** 就像这个：

![演示](./images/xdm34.png)

源字段 **GA_ID** 和 **customerID** 映射到此XDM架构中的标识符。 这样，您就可以使用其他Google Analytics集（如忠诚度或呼叫中心数据）扩充客户数据（Web/应用程序行为数据）。

单击&#x200B;**下一步**。

![演示](./images/ex4/38.png)

## 12.4.3连接和数据摄取计划

您现在将看到 **计划** 选项卡：

![演示](./images/xdm38a.png)

在 **计划** 选项卡，则可以为此定义数据摄取流程的频率 **映射** 和数据。

当您在Google BigQuery中使用不会刷新的演示数据时，您无需在本练习中设置计划。 您必须选择某些内容，并避免过多无用的数据摄取流程，您需要设置如下频率：

- 频率： **周**
- 间隔： **200**

![演示](./images/ex4/39.png)

**重要信息**:确保激活 **回填** 切换。

![演示](./images/ex4/39a.png)

最后，您必须定义 **三角洲** 字段。

![演示](./images/ex4/36.png)

的 **三角洲** 字段，用于计划连接并仅上载进入BigQuery数据集的新行。 增量字段通常始终为时间戳列。 因此，对于将来的计划数据摄取，将只摄取具有最新新时间戳的行。

选择 **timeStamp** 作为增量字段。

![演示](./images/ex4/37.png)

你现在有这个。

![演示](./images/xdm37a.png)

单击&#x200B;**下一步**。

![演示](./images/ex4/42.png)

## 12.4.4审查和启动连接

在 **数据集流量详细信息** 中。 您需要命名连接，这将帮助您稍后查找。

请使用此命名约定：

| 字段 | 命名 | 示例 |
| ----------------- |-------------| -------------|
| 数据集流程名称 | DataFlow - ldap - BigQuery网站交互 | DataFlow - vangeluw - BigQuery网站交互 |
| 描述 | DataFlow - ldap - BigQuery网站交互 | DataFlow - vangeluw - BigQuery网站交互 |

![演示](./images/xdm44.png)

单击&#x200B;**下一步**。

![演示](./images/ex4/45.png)

现在，您将看到有关连接的详细概述。 在继续操作之前，请确保一切正确，因为某些设置在之后无法再更改，例如XDM映射。

![演示](./images/xdm46.png)

单击&#x200B;**完成**。

![演示](./images/ex4/finish.png)

设置连接可能需要一些时间，因此如果您看到以下内容，请不要担心：

![演示](./images/ex4/47.png)

创建连接后，您将看到：

![演示](./images/xdm48.png)

现在，您可以继续下一个练习，在接下来的练习中，您将使用Customer Journey Analytics基于Google Analytics数据构建强大的可视化图表。

下一步： [12.5使用Google Analytics分析Customer Journey Analytics数据](./ex5.md)

[返回到模块12](./customer-journey-analytics-bigquery-gcp.md)

[返回到所有模块](./../../overview.md)
