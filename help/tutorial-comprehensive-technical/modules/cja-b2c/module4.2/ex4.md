---
title: 使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据 — 将BigQuery中的数据加载到Adobe Experience Platform中
description: 使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据 — 将BigQuery中的数据加载到Adobe Experience Platform中
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# 4.2.4将数据从BigQuery加载到Adobe Experience Platform中

## 目标

- 将BigQuery数据映射到XDM架构
- 将BigQuery数据加载到Adobe Experience Platform
- 熟悉BigQuery Source连接器UI

## 开始之前

在练习12.3之后，您应该在Adobe Experience Platform中打开以下页面：

![演示](./images/datasets.png)

**如果您打开了它，请继续进行练习12.4.1。**

**如果您尚未打开它，请转到[Adobe Experience Platform](https://experience.adobe.com/platform/home)。**

在左侧菜单中，转到“源”。 您随后将看到&#x200B;**源**&#x200B;主页。 在&#x200B;**源**&#x200B;菜单中，单击&#x200B;**数据库**。

![演示](./images/sourceshome.png)

选择&#x200B;**Google BigQuery** Source连接器，然后单击&#x200B;**+配置**。

![演示](./images/bq.png)

然后，您会看到Google BigQuery帐户选择屏幕。

![演示](./images/0-c.png)

选择您的帐户，然后单击&#x200B;**下一步**。

![演示](./images/ex4/0-d.png)

您随后将看到&#x200B;**添加数据**&#x200B;视图。

![演示](./images/datasets.png)

## 4.2.4.1 BigQuery表选择

在&#x200B;**添加数据**&#x200B;视图中，选择您的BigQuery数据集。

![演示](./images/datasets.png)

您现在可以在BigQuery中看到Google Analytics数据的示例数据预览。

单击&#x200B;**下一步**。

![演示](./images/ex4/3.png)

## 4.2.4.2 XDM映射

您现在将看到以下内容：

![演示](./images/xdm4a.png)

现在，您必须创建新数据集或选择现有数据集以将Google Analytics数据加载到中。 对于此练习，已创建一个数据集和架构。 您无需创建新架构或数据集。

选择&#x200B;**现有数据集**。 打开下拉菜单以选择数据集。 搜索名为`Demo System - Event Dataset for BigQuery (Global v1.1)`的数据集并将其选定。 单击&#x200B;**下一步**。

![演示](./images/xdm6.png)

向下滚动。 您现在需要从Google Analytics/BigQuery将每&#x200B;**个Source字段**&#x200B;映射到一个XDM **目标字段**，按字段映射。

![演示](./images/xdm8.png)

在本练习中使用下面的映射表。

| 源字段 | 目标字段 |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | 渠道。_id |
| 时间戳 | 时间戳 |
| GA_ID | ``--aepTenantId--``.identification.core.gaid |
| 客户ID | ``--aepTenantId--``.identification.core.loyaltyId |
| 页面 | web.webPageDetails.name |
| 设备 | device.type |
| 浏览器 | environment.browserDetails.vendor |
| 营销渠道 | marketing.trackingCode |
| TrafficSource | channel.typeAtSource |
| 流量媒介 | channel.mediaType |
| 交易ID | commerce.order.payments.transactionID |
| E-commerce_Action_Type | 事件类型 |
| 页面查看次数 | web.webPageDetails.pageViews.value |
| 独特购买次数 | commerce.purchases.value |
| Product_Detail_View | commerce.productViews.value |
| Adds_To_Cart | commerce.productListAdds.value |
| Product_Removes_From_Cart | commerce.productListRemovals.value |
| Product_Checkout | commerce.checkouts.value |

将上述映射复制并粘贴到Adobe Experience Platform UI后，请验证您是否未看到由于拼写错误或前导/尾随空格导致的任何错误。

您现在有了&#x200B;**映射**，如下所示：

![演示](./images/xdm34.png)

源字段&#x200B;**GA_ID**&#x200B;和&#x200B;**customerID**&#x200B;映射到此XDM架构中的标识符。 这将允许您使用其他数据集（如忠诚度或呼叫中心数据）扩充Google Analytics数据（Web/应用程序行为数据）。

单击&#x200B;**下一步**。

![演示](./images/ex4/38.png)

## 4.2.4.3连接和数据摄取调度

您现在将看到&#x200B;**计划**&#x200B;选项卡：

![演示](./images/xdm38a.png)

在&#x200B;**计划**&#x200B;选项卡中，您可以为此&#x200B;**映射**&#x200B;和数据定义数据摄取过程的频率。

由于您在Google BigQuery中使用不会刷新的演示数据，因此在本练习中无需设置计划。 您确实必须选择某些内容，并且要避免过多的无用数据摄取流程，您需要设置频率，如下所示：

- 频率： **周**
- 间隔： **200**

![演示](./images/ex4/39.png)

**重要信息**：请务必激活&#x200B;**回填**&#x200B;开关。

![演示](./images/ex4/39a.png)

最后但并非最不重要的一点是，您必须定义&#x200B;**delta**&#x200B;字段。

![演示](./images/ex4/36.png)

**delta**&#x200B;字段用于计划连接并仅上传进入BigQuery数据集的新行。 增量字段通常始终为时间戳列。 因此，对于未来的计划数据摄取，将仅摄取具有新的、更新的时间戳的行。

选择&#x200B;**时间戳**&#x200B;作为增量字段。

![演示](./images/ex4/37.png)

您现在拥有了此功能。

![演示](./images/xdm37a.png)

单击&#x200B;**下一步**。

![演示](./images/ex4/42.png)

## 4.2.4.4查看并启动连接

在&#x200B;**数据集流详细信息**&#x200B;视图中。 您需要命名连接，以便稍后查找。

请使用此命名约定：

| 字段 | 命名 | 示例 |
| ----------------- |-------------| -------------|
| 数据集流名称 | DataFlow - ldap - BigQuery网站交互 | DataFlow - vangeluw - BigQuery网站交互 |
| 描述 | DataFlow - ldap - BigQuery网站交互 | DataFlow - vangeluw - BigQuery网站交互 |

![演示](./images/xdm44.png)

单击&#x200B;**下一步**。

![演示](./images/ex4/45.png)

您现在可以看到连接的详细概述。 在继续之前，请确保所有内容均正确，因为某些设置此后不能再更改，例如XDM映射。

![演示](./images/xdm46.png)

单击&#x200B;**完成**。

![演示](./images/ex4/finish.png)

设置连接可能需要一些时间，因此，如果您看到以下内容，请不要担心：

![演示](./images/ex4/47.png)

创建连接后，您将看到以下内容：

![演示](./images/xdm48.png)

您现在已准备好继续下一个练习，在该练习中，您将使用Customer Journey Analytics功能基于Google Analytics数据构建强大的可视化图表。

下一步： [4.2.5使用Customer Journey Analytics分析Google Analytics数据](./ex5.md)

[返回模块4.2](./customer-journey-analytics-bigquery-gcp.md)

[返回所有模块](./../../../overview.md)
