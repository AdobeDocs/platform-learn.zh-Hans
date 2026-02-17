---
title: 设置关系数据基础
description: 设置关系数据基础
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: 4d420ad101c87b58a2bcc425cd4d8da08ad04c8e
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 2%

---

# 3.8.1设置关系数据基础

通过转到[https://experience.adobe.com](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![AJO OC](./images/aechome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。

![AJO OC](./images/ajohome.png)

## 3.8.1.1基于关系的架构设置

基于关系模式是基于模型的数据模型的形式化定义。

它指定：

- 表集
- 每个表中的列
- 约束
- 表之间的关系

在基于模型的数据模型中组织架构或表就是将您的数据结构化为多个表。 确保每个表存储一种类型的实体/架构。

当将数据摄取到中使用以用于Adobe Journey Optimizer编排的营销活动时，以下源可用：

- Amazon S3
- Google 云存储
- SFTP
- Snowflake
- Google BigQuery
- 数据登陆区
- Azure Databricks
- 本地文件上传

本练习的第一步是配置基于关系的XDM架构。 在左侧菜单中，向下滚动到&#x200B;**数据管理**&#x200B;并选择&#x200B;**架构**。 单击&#x200B;**+创建架构**。

![AJO OC](./images/ajoocdata1.png)

选择&#x200B;**关系**。

![AJO OC](./images/ajoocdata2.png)

选择&#x200B;**上传DDL文件**，然后单击&#x200B;**选择文件**。

![AJO OC](./images/ajoocdata3.png)

将文件[citisignal_ddl_tables_only.sql](./assets/citisignal_ddl_tables_only.sql)下载到桌面。

![AJO OC](./images/ajoocdata4.png)

选择文件&#x200B;**`citisignal_ddl_tables_only.sql`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdata5.png)

您应该会看到此内容。 单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdata6.png)

### 身份标识

您的某些架构包含个人标识符，这些字段应标记为&#x200B;**标识**，您需要选择适用于该特定标识类型的&#x200B;**命名空间**。

**`citisignal_accounts`**

对于此架构，请转到字段&#x200B;**account_id**&#x200B;并将&#x200B;**Identity**&#x200B;类型设置为&#x200B;**演示系统 — CRMID**。

![AJO OC](./images/ajoocdata7.png)

**`citisignal_recipients`**

对于此架构，请转到字段&#x200B;**account_id**&#x200B;并将&#x200B;**Identity**&#x200B;类型设置为&#x200B;**演示系统 — CRMID**，然后转到字段&#x200B;**email**&#x200B;并将&#x200B;**Identity**&#x200B;类型设置为&#x200B;**Email**。

![AJO OC](./images/ajoocdata8.png)

### 版本控制

为了跟踪将针对这些架构摄取的数据的更新，需要设置一个用于跟踪已上传数据版本的字段。 所有这些架构中用于此情况的字段是字段&#x200B;**lastmodified**，其中包含已上载数据的时间戳。

现在，您需要选中每个架构中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

**`citisignal_products`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata9.png)

**`citisignal_product_bundles`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata10.png)

**`citisignal_product_relationships`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata11.png)

**`citisignal_accounts`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata12.png)

**`citisignal_recipients`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata13.png)

**`citisignal_mobile_subscriptions`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata14.png)

**`citisignal_internet_subscriptions`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata15.png)

**`citisignal_tv_subscriptions`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata16.png)

**`citisignal_equipment_subscriptions`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata17.png)

**`citisignal_mobile_usage_summary`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata18.png)

**`citisignal_internet_usage_summary`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata19.png)

**`citisignal_offers`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata20.png)

**`citisignal_offer_eligibility`**

选中字段&#x200B;**lastmodified**&#x200B;的&#x200B;**版本控制**&#x200B;复选框。

![AJO OC](./images/ajoocdata21.png)

### 架构名称

当在共享沙盒中摄取这些架构以进行支持时，需要更改每个架构的名称，以便它在特定沙盒中是唯一的。 进行此更改的原因是避免架构命名冲突。

对于本实验，您应该将LDAP添加到每个架构名称之前，这意味着每个架构名称都应具有此前缀： `--aepUserLdap--_`

**`citisignal_products`**

将架构名称更改为`--aepUserLdap--_ citisignal_products`。

![AJO OC](./images/ajoocdatan9.png)

**`citisignal_product_bundles`**

将架构名称更改为`--aepUserLdap--_ citisignal_product_bundles`。

![AJO OC](./images/ajoocdatan10.png)

**`citisignal_product_relationships`**

将架构名称更改为`--aepUserLdap--_ citisignal_product_relationships`。

![AJO OC](./images/ajoocdatan11.png)

**`citisignal_accounts`**

将架构名称更改为`--aepUserLdap--_ citisignal_accounts`。

![AJO OC](./images/ajoocdatan12.png)

**`citisignal_recipients`**

将架构名称更改为`--aepUserLdap--_ citisignal_recipients`。

![AJO OC](./images/ajoocdatan13.png)

**`citisignal_mobile_subscriptions`**

将架构名称更改为`--aepUserLdap--_ citisignal_mobile_subscriptions`。

![AJO OC](./images/ajoocdatan14.png)

**`citisignal_internet_subscriptions`**

将架构名称更改为`--aepUserLdap--_ citisignal_internet_subscriptions`。

![AJO OC](./images/ajoocdatan15.png)

**`citisignal_tv_subscriptions`**

将架构名称更改为`--aepUserLdap--_ citisignal_internet_subscriptions`。

![AJO OC](./images/ajoocdatan16.png)

**`citisignal_equipment_subscriptions`**

将架构名称更改为`--aepUserLdap--_ citisignal_equipment_subscriptions`。

![AJO OC](./images/ajoocdatan17.png)

**`citisignal_mobile_usage_summary`**

将架构名称更改为`--aepUserLdap--_ citisignal_mobile_usage_summary`。

![AJO OC](./images/ajoocdatan18.png)

**`citisignal_internet_usage_summary`**

将架构名称更改为`--aepUserLdap--_ citisignal_internet_usage_summary`。

![AJO OC](./images/ajoocdatan19.png)

**`citisignal_offers`**

将架构名称更改为`--aepUserLdap--_ citisignal_offers`。

![AJO OC](./images/ajoocdatan20.png)

**`citisignal_offer_eligibility`**

将架构名称更改为`--aepUserLdap--_ citisignal_offer_eligibility`。

![AJO OC](./images/ajoocdatan21.png)

您的架构现在已准备好进行保存。 单击&#x200B;**完成**。

![AJO OC](./images/ajoocdata22.png)

您应该会看到此内容。 单击&#x200B;**保存**。

![AJO OC](./images/ajoocdata23.png)

单击&#x200B;**打开作业**。

![AJO OC](./images/ajoocdata24.png)

您应该会看到此内容。 您应等到作业成功完成后再继续下一步。

![AJO OC](./images/ajoocdata25.png)

一旦作业成功完成，您就可以继续下一步骤。 这可能需要5-10分钟。

![AJO OC](./images/ajoocdata26.png)

现在，您的关系XDM架构已配置并且正在引入数据，您可以在下一个练习中开始使用该数据创建编排的活动。

## 3.8.1.2数据摄取

转到&#x200B;**数据集**。 然后，您应该会看到为您创建的每个架构创建的数据集。

![AJO OC](./images/ajoocdata27.png)

将文件[data.zip](./assets/data.zip)下载到您的桌面并解压缩。

![AJO OC](./images/ajoocdata28.png)

打开文件夹&#x200B;**数据**。 您应该会看到已创建的每个架构的CSV文件。 现在，您需要将该数据上传到每个相应的数据集中。 在本实验中，您将通过在每个数据集中上传本地文件来实现这一点。

![AJO OC](./images/ajoocdata29.png)

**`vangeluw_citisignal_products`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_products`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas9a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_products.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas9b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas9c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas9d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas9e.png)

**`vangeluw_citisignal_product_bundles`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_product_bundles`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas10a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_product_bundles.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas10b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas10c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas10d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas10e.png)

**`vangeluw_citisignal_product_relationships`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_product_relationships`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas11a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_product_relationships.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas11b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas11c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas11d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas11e.png)

**`vangeluw_citisignal_accounts`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_accounts`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas12a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_accounts.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas12b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas12c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas12d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas12e.png)

**`vangeluw_citisignal_recipients`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_recipients`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas13a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_recipients.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas13b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas13c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas13d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas13e.png)

**`vangeluw_citisignal_mobile_subscriptions`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_mobile_subscriptions`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas14a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_mobile_subscriptions.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas14b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas14c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas14d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas14e.png)

**`vangeluw_citisignal_internet_subscriptions`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_internet_subscriptions`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas15a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_internet_subscriptions.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas15b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas15c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas15d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas15e.png)

**`vangeluw_citisignal_tv_subscriptions`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_tv_subscriptions`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas16a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_tv_subscriptions.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas16b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas16c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas16d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas16e.png)

**`vangeluw_citisignal_equipment_subscriptions`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_equipment_subscriptions`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas17a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_equipment_subscriptions.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas17b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas17c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas17d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas17e.png)

**`vangeluw_citisignal_mobile_usage_summary`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_mobile_usage_summary`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas18a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_mobile_usage_summary.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas18b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas18c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas18d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas18e.png)

**`vangeluw_citisignal_internet_usage_summary`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_internet_usage_summary`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas19a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_internet_usage_summary.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas19b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas19c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas19d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas19e.png)

**`vangeluw_citisignal_offers`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_offers`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas20a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_offers.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas20b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas20c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas20d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas20e.png)

**`vangeluw_citisignal_offer_eligibility`**

转到&#x200B;**源**，搜索`local`，然后单击&#x200B;**本地文件上传**&#x200B;下的&#x200B;**添加数据**。

![AJO OC](./images/ajoocdatas10.png)

为&#x200B;**启用更改数据捕获**&#x200B;启用切换。

选择数据集`vangeluw_citisignal_offer_eligibility`。

单击&#x200B;**下一步**。

![AJO OC](./images/ajoocdatas21a.png)

单击&#x200B;**选择文件**。 选择文件&#x200B;**`citisignal_offer_eligibility.csv`**&#x200B;并单击&#x200B;**打开**。

![AJO OC](./images/ajoocdatas21b.png)

单击&#x200B;**下一步**

![AJO OC](./images/ajoocdatas21c.png)

单击&#x200B;**完成**。

![AJO OC](./images/ajoocdatas21d.png)

几分钟后，您可以看到数据集中正在摄取的数据。

![AJO OC](./images/ajoocdatas21e.png)

所有数据现已摄取。

## 3.8.1.3配置文件目标Dimension

借助编排的营销活动，您可以利用Adobe Experience Platform的关系架构功能，在实体级别设计和提供有针对性的通信。 Experience Platform使用架构，以一致且可重用的方式描述数据结构。 当数据被摄取到Experience Platform中时，它会根据XDM架构进行构建。

虽然编排的营销活动分段主要在关系架构上运行，但实际消息投放始终在用户档案级别进行。

在配置定位时，您可以定义两个关键方面：

- 可定位架构：您可以指定哪些关系架构符合定位条件。 默认情况下使用名为Recipient的架构，但您可以配置替代方案，例如访客、客户等。

- 配置文件链接：系统必须了解目标架构如何映射到配置文件架构。 这是通过共享身份字段实现的，该字段存在于目标架构和配置文件架构中，并配置为身份命名空间。

您现在需要配置个人资料目标维度。 转到&#x200B;**管理** > **配置**，然后单击&#x200B;**配置文件目标Dimension**&#x200B;下的&#x200B;**管理**。

![AJO OC](./images/ajoocptd1.png)

您应该会看到此内容。 单击&#x200B;**创建**。

![AJO OC](./images/ajoocptd2.png)

对于&#x200B;**架构**，请选择`--aepUserLdap--_citisignal_accounts`。 对于&#x200B;**标识值**，请选择&#x200B;**account_id**。

单击&#x200B;**保存**。

![AJO OC](./images/ajoocptd3.png)

再次单击&#x200B;**创建**。

![AJO OC](./images/ajoocptd4.png)

对于&#x200B;**架构**，请选择`--aepUserLdap--_citisignal_recipients`。 对于&#x200B;**标识值**，请选择&#x200B;**account_id**。

单击&#x200B;**保存**。

![AJO OC](./images/ajoocptd5.png)

再次单击&#x200B;**创建**。

![AJO OC](./images/ajoocptd6.png)

对于&#x200B;**架构**，请选择`--aepUserLdap--_citisignal_recipients`。 对于&#x200B;**标识值**，请选择&#x200B;**电子邮件**。

单击&#x200B;**保存**。

![AJO OC](./images/ajoocptd7.png)

然后您应该拥有此项。

![AJO OC](./images/ajoocptd8.png)

在下一个练习中，您将开始将该数据用作编排的营销活动的一部分。

## 后续步骤

转到[创建您的编排营销活动](./ex2.md){target="_blank"}

返回至[Adobe Journey Optimizer：编排的营销活动](./ajocampaigns.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
