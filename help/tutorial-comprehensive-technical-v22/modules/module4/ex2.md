---
title: 查询服务 — 使用查询服务
description: 查询服务 — 使用查询服务
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dbf19991-cb09-43cf-887c-52996dfd2986
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 4.2使用查询服务

## 目标

- 查找和浏览数据集
- 了解如何在查询中处理体验数据模型对象和属性

## 上下文

在本课程中，您将学习如何使用PSQL检索有关可用数据集的信息，如何为Experience Data Model(XDM)编写查询，以及如何使用查询服务和Citi Signal数据集编写您的第一个简单报表查询。

## 4.2.1基本查询

在此步骤中，您将了解如何检索有关可用数据集的信息，以及如何使用XDM数据集中的查询正确检索数据。

我们在1开头通过Adobe Experience Platform探索的所有数据集也可以通过SQL接口作为表进行访问。 要列出这些表，您可以使用 **显示表格；** 命令。

执行 **显示表格；** 在 **PSQL命令行界面**. （请不要忘记以分号结束命令）。

复制命令 **显示表格；** 并在提示符下粘贴：

![command-prompt-show-tables.png](./images/command-prompt-show-tables.png)

您将看到以下结果：

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

在冒号中，按空格键查看结果集的下一页，或输入 `q` 还原到命令提示符。

Platform中的每个数据集都有其对应的“查询服务”表。 您可以通过数据集用户界面找到数据集的表：

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

的 `demo_system_event_dataset_for_website_global_v1_1` 表是与 `Demo System - Event Schema for Website (Global v1.1)` 数据集。

要查询有关产品在何处被查看的信息，我们将选择 **地域** 信息。

复制下面的语句，并将其粘贴到 **PSQL命令行界面** 和按Enter:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

在查询结果中，您会注意到体验数据模型(XDM)中的列可能是复杂类型，而不仅仅是标量类型。 在上面的查询中，我们希望确定 **commerce.productViews** 确实发生了。 识别 **commerce.productViews** 我们必须使用 **.** （点）表示法。

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
(1 row)
```

请注意，结果是平面对象，而不是单个值？ 的 **placecontext.geo** 对象包含四个属性：模式、国家/地区和城市。 当对象声明为列时，它将以字符串的形式返回整个对象。 XDM架构可能比您熟悉的更复杂，但它非常强大，旨在支持许多解决方案、渠道和用例。

要选择对象的单个属性，请使用 **.** （点）表示法。

复制下面的语句，并将其粘贴到 **PSQL命令行界面**:

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

上述查询的结果应当如下所示。
现在，结果是设置了一组简单值：

```text
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

不用担心，有一种轻松的方法可以获取特定资产的路径。 在以下部分中，您将学习如何操作。

您需要编辑查询，因此我们先打开一个编辑器。

在Windows上

单击 **搜索** 图标，键入 **记事本** 在 **搜索** 字段，单击 **记事本** 结果：

![windows-start-notepad.png](./images/windows-start-notepad.png)

在Mac

安装 [括号](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) 或者，如果您未安装文本编辑器并按照相关说明进行操作，则可以使用您选择的其他文本编辑器。 安装后，搜索 **括号** 通过Mac的焦点搜索将其打开。

将以下语句复制到记事本或括号中：

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

返回到Adobe Experience Platform UI（应在浏览器中打开）或导航到 [https://platform.adobe.com](https://platform.adobe.com).

选择 **模式**，输入 `Demo System - Event Schema for Website (Global v1.1)` 在 **搜索** 字段和选择 `Demo System - Event Schema for Website (Global v1.1) Schema` 列表。

![browse-schema.png](./images/browse-schema.png)

探索XDM模型 **演示系统 — 网站的事件模式（全局v1.1）**，方法是单击对象。 展开树以 **置入文本**, **地域** 和 **模式**. 选择实际属性时 **经度**，则会在突出显示的红色框中看到完整路径。 要复制属性的路径，请单击复制路径图标。

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

切换到记事本/括号并删除 **your_attribute_path_here** 从第一行开始。 将光标放在 **选择** 并粘贴(CTRL-V)。

从记事本/括号中复制修改后的语句，并将其粘贴到 **PSQL命令行界面** 并按enter。

结果应该如下所示：

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

下一步： [4.3查询、查询、查询……和流失分析](./ex3.md)

[返回到模块4](./query-service.md)

[返回到所有模块](../../overview.md)
