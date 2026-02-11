---
title: 设置关系数据基础
description: 设置关系数据基础
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

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

现在，您的关系XDM架构已配置并且正在引入数据，您可以在下一个练习中开始使用该数据创建编排的活动。

## 3.8.1.2数据摄取


## 后续步骤

转到[创建您的编排营销活动](./ex2.md){target="_blank"}

返回[Adobe Journey Optimizer：营销活动](./ajocampaigns.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
