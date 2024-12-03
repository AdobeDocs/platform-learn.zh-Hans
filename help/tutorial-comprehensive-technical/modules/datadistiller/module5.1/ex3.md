---
title: 查询服务 — 使用查询服务
description: 查询服务 — 使用查询服务
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: 31c14a9b-cb62-48ab-815c-caa6e832794f
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# 5.1.3使用查询服务

## 目标

- 查找和浏览数据集
- 了解如何在查询中处理Experience Data Model对象和属性

## 上下文

在本课程中，您将学习如何使用PSQL检索有关可用数据集的信息，如何编写Experience Data Model (XDM)的查询，以及使用查询服务和Citi Signal数据集编写您的第一个简单报表查询。

## 基本查询

在本教程中，您将了解用于检索有关可用数据集的信息的方法，以及如何通过XDM数据集中的查询正确检索数据。

在1之初，我们通过Adobe Experience Platform探索的所有数据集也可以通过SQL接口作为表进行访问。 要列出这些表，可以使用&#x200B;**show tables；**&#x200B;命令。

在&#x200B;**PSQL命令行接口**&#x200B;中执行&#x200B;**显示表；**。 （别忘了用分号结束您的命令）。

复制命令&#x200B;**show tables；**&#x200B;并在提示符处粘贴它：

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

在冒号处，按空格键查看结果集的下一页，或输入`q`还原到命令提示符。

Platform中的每个数据集都有其相应的查询服务表。 您可以通过数据集ui找到数据集的表：

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

`demo_system_event_dataset_for_website_global_v1_1`表是与`Demo System - Event Schema for Website (Global v1.1)`数据集对应的查询服务表。

要查询有关产品查看位置的信息，我们将选择&#x200B;**地域**&#x200B;信息。

复制下面的语句并将其粘贴到&#x200B;**PSQL命令行接口**&#x200B;中的提示符，然后按Enter：

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

在查询结果中，您会注意到体验数据模型(XDM)中的列可以是复杂类型，而不仅仅是标量类型。 在上面的查询中，我们希望确定发生&#x200B;**commerce.productViews**&#x200B;的地理位置。 要识别&#x200B;**commerce.productViews**，我们必须使用&#x200B;**在XDM模型中导航。** （点）表示法。

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

是否注意到结果是一个平面对象而不是单个值？ **placecontext.geo**&#x200B;对象包含四个属性：架构、国家/地区和城市。 当一个对象被声明为一列时，它将以字符串的形式返回整个对象。 XDM架构可能比您熟悉的架构更复杂，但它非常强大，其设计可支持许多解决方案、渠道和用例。

要选择对象的各个属性，请使用&#x200B;**。** （点）表示法。

复制下面的语句并将其粘贴到&#x200B;**PSQL命令行接口**&#x200B;中的提示符：

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

上述查询的结果应如下所示。
结果现在是一组简单的值：

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

不用担心，有一个简单的方法可以获得指向特定资产的路径。 在接下来的部分中，您将学习如何操作。

您将需要编辑查询，因此让我们先打开一个编辑器。

在Windows上

单击Windows工具栏中的&#x200B;**搜索**&#x200B;图标，在&#x200B;**搜索**&#x200B;字段中键入&#x200B;**记事本**，单击&#x200B;**记事本**&#x200B;结果：

![windows-start-notepad.png](./images/windows-start-notepad.png)

在Mac上

安装[Brackets](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg)，或者使用其他选择的文本编辑器（如果未安装），然后按照说明操作。 安装后，通过Mac的Spotlight搜索功能搜索&#x200B;**Brackets**&#x200B;并将其打开。

将以下语句复制到记事本或方括号：

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

返回到Adobe Experience Platform UI（应在浏览器中打开）或导航到[https://platform.adobe.com](https://platform.adobe.com)。

选择&#x200B;**架构**，在&#x200B;**搜索**&#x200B;字段中输入`Demo System - Event Schema for Website (Global v1.1)`并从列表中选择`Demo System - Event Schema for Website (Global v1.1) Schema`。

![browse-schema.png](./images/browse-schema.png)

通过单击对象来探索&#x200B;**演示系统 — 网站(Global v1.1)**&#x200B;的事件架构的XDM模型。 展开&#x200B;**placecontext**、**geo**&#x200B;和&#x200B;**架构**&#x200B;的树。 当您选择实际属性&#x200B;**longitude**&#x200B;时，您将在高亮显示的红色框中看到完整的路径。 要复制属性的路径，请单击复制路径图标。

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

切换到记事本/括号并从第一行删除&#x200B;**your_attribute_path_here**。 将光标放在第一行&#x200B;**选择**&#x200B;后并粘贴(CTRL-V)。

从记事本/方括号中复制修改后的语句，并将其粘贴到&#x200B;**PSQL命令行界面**&#x200B;中的提示符，然后按Enter键。

结果应如下所示：

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

下一步： [5.1.4查询、查询、查询……和流失分析](./ex4.md)

[返回模块5.1](./query-service.md)

[返回所有模块](../../../overview.md)
