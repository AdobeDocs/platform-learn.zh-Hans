---
title: Data Warehouse连接
seo-title: Configure a Data Warehouse connection | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Data Warehouse连接
description: 在本可视化练习中，我们将配置Adobe Experience Platform与您的企业Data Warehouse之间的连接以启用联合受众合成。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-configure-a-data-warehouse-connection.jpg
exl-id: 3935f3ff-7728-4cd1-855e-2cd02c2ecc59
source-git-commit: 15619a8419f608da6a77745fabf72c356a2ac4b4
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Data Warehouse连接

我们首先配置Adobe Experience Platform与您的企业Data Warehouse之间的连接以启用联合受众合成。 这允许您直接从支持的仓库查询数据，而无需复制。 此外，我们还基于Data Warehouse表创建架构和数据模型。

为了演示，我们连接到Snowflake帐户。 联合受众组合支持不断增加的云仓库连接列表。 查看[更新的集成列表](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}。

## 步骤

1. 浏览到左边栏上的&#x200B;**联合数据**&#x200B;部分。
2. 在&#x200B;**联合数据库**&#x200B;链接中，单击&#x200B;**添加联合数据库**&#x200B;按钮。
3. 添加名称并选择&#x200B;**Snowflake**。
4. 填写详细信息，单击&#x200B;**测试连接**&#x200B;按钮，然后单击&#x200B;**部署函数**&#x200B;按钮。

   ![snowflake-connection-setup](assets/snowflake-connection-setup.png)

   ![snowflake-connection-setup-step2](assets/snowflake-connection-setup-step2.png)

   ![snowflake-connection-setup-step3](assets/snowflake-connection-setup-step3.png)

## 创建架构

要在联合受众构成中创建架构，请执行以下步骤：

### 步骤

1. 在&#x200B;**联合数据**&#x200B;部分中，单击&#x200B;**模型**。
2. 浏览&#x200B;**架构**&#x200B;选项卡，然后单击&#x200B;**创建架构**&#x200B;按钮。
3. 在列表中选择源数据库，然后单击&#x200B;**添加表**&#x200B;选项卡。
4. 从联合源中选择表。 在我们的示例中：
   - FSI_CRM
   - FSI_CRM_CONSENT_PREFERENCE

   ![create-schema](assets/create-schema.png)

   ![select-table](assets/select-table.png)

选择表后，复查每个表中的列并选择主键。 为了支持业务案例，在两个表中都选择了&#x200B;**EMAIL**&#x200B;作为主键。

![create-schema](assets/create-schema.png)

![create-schema-step2](assets/create-schema-step2.png)

## 创建数据模型

数据模型允许您在表之间创建链接。 可以在同一数据库中的表之间创建链接，例如Snowflake中的表；也可以在不同数据库中的表之间创建链接，例如Snowflake中的表与Amazon Redshift中的表之间的链接。

### 步骤

1. 在&#x200B;**联合数据**&#x200B;部分中，单击&#x200B;**模型**，然后单击&#x200B;**数据模型**。
2. 单击&#x200B;**创建数据模型**&#x200B;按钮。
3. 提供数据模型的名称。
4. 单击&#x200B;**添加架构**&#x200B;并选择新的联合数据架构。 在此示例中，我们选择&#x200B;**FSI_CRM**&#x200B;和&#x200B;**FSI_CRM_CONSENT_PREFERENCE**&#x200B;架构。
5. 通过单击&#x200B;**创建链接**，创建这些表之间的链接。

创建链接时，请选择适用的基数：

- **1-N**：源表格的一个存在可以拥有目标表格的多个对应存在，但目标表格的一个存在最多可以拥有源表格的一个对应存在。
- **N-1**：目标表的一个存在可以具有源表的多个对应存在，但源表的一个存在最多可以具有目标表的一个对应存在。
- **1-1**：源表格的一个存在最多可以具有目标表格的一个对应存在。

以下是按照上述步骤创建的链接的预览。 该链接使CRM和同意表之间能够使用主键&#x200B;**EMAIL**&#x200B;执行联接。

![预览 — 数据模型](assets/preview-data-model.png)

现在，我们准备好[创建和受众](audience-creation-exercise.md)。
