---
title: Offer Decisioning - Offer Decisioning 101
description: Offer Decisioning - Offer Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
exl-id: b46e0205-b0a1-4a14-95f6-9afe21cd2b5e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

# 3.3.1Offer Decisioning 101

## 3.3.1.1术语

要更好地了解Offer Decisioning，我们强烈建议您阅读[概述](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en)，了解Offer Decisioning应用程序服务如何与Adobe Experience Platform配合使用。

使用Offer Decisioning时，您需要了解以下概念：

| 搜索词 | 说明 |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **选件** | 优惠是营销消息，其中可能包含与其关联的规则，用于指定有资格查看优惠的人员。 优惠的状态为：草稿、已批准或已存档。 |
| **投放位置** | 为最终用户显示选件的位置（或渠道类型）和上下文（或内容类型）的组合。 实际上，它是移动设备、Web、社交、即时消息和非数字渠道中的文本、HTML、图像、JSON的组合。 |
| **规则** | 定义并控制最终用户获得选件的资格的逻辑。 |
| **个性化优惠** | 基于资格规则和约束的可自定义营销消息。 |
| **后备优惠** | 当最终用户不符合使用的收藏集中任何选件的资格时显示的默认选件。 |
| **上限** | 在选件定义中使用，以定义某个选件总计可向特定用户展示的次数。 |
| **优先级** | 根据选件的结果集确定优先级排名的级别。 |
| **收藏集** | 用于从个性化优惠列表中筛选出优惠的子集，以加快Offer Decisioning过程。 |
| **决策** | 营销人员希望决策引擎提供最佳优惠的一组优惠、投放位置和用户档案。 |
| **AEM Assets Essentials** | 跨Adobe Experience Cloud解决方案和Adobe Experience Platform存储、查找和选择资源的通用集中体验。 |

{style="table-layout:auto"}

## 3.3.1.2Offer Decisioning

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

在左侧菜单中，单击&#x200B;**选件**。 您现在将看到优惠菜单，其中包含优惠、收藏集和决策等内容。

![放置环境](./images/homedec.png)

单击&#x200B;**组件**。 您现在可以看到投放位置、收藏集限定符、规则和排名等内容。

![放置环境](./images/components.png)

## 3.3.1.3版面

转到&#x200B;**版面**。

![放置环境](./images/placements.png)

在&#x200B;**版面**&#x200B;选项卡中，您可以为优惠定义版面。 定义决策时，投放位置将定义结果优惠的显示位置（渠道类型）以及形式或形式（内容类型）。

如果您在环境中看不到任何投放位置，请按照下面和屏幕快照中的指示创建它们。

| 名称 | 渠道类型 | 内容类型 |
| ---------------------- | ------------ | ------------ |
| **非数字 — 文本** | 非数字 | 文本 |
| **Web - JSON** | Web | JSON |
| **Web - HTML** | Web | HTML |
| **Web — 文本** | Web | 文本 |
| **Web — 图像** | Web | 图像 |
| **电子邮件 — JSON** | 电子邮件 | JSON |
| **电子邮件 — HTML** | 电子邮件 | HTML |
| **电子邮件 — 文本** | 电子邮件 | 文本 |
| **电子邮件 — 图像** | 电子邮件 | 图像 |

{style="table-layout:auto"}

**注意**：请不要更改任何已可用的版面。

单击任意位置可可视化其设置。

![放置环境](./images/placement1.png)

您现在将看到投放位置的所有字段：

- 投放位置的&#x200B;**名称**
- **版面ID**
- 投放位置的&#x200B;**渠道类型**
- 投放位置的&#x200B;**内容类型**，可以是&#x200B;**文本**、**HTML**、**图像**&#x200B;或&#x200B;**JSON**
- **描述**&#x200B;字段，允许为投放位置添加其他描述

## 3.3.1.4决定规则

规则（也称为资格规则）等同于&#x200B;**受众**。 规则实际上是受众本身，两者之间唯一的区别是，规则可以与选件一起使用，以便在Adobe Experience Platform中为配置文件提供最佳选件。

由于您已经知道如何根据以前的启用模块定义受众，因此让我们快速重新访问分段环境：

转到&#x200B;**规则**。 单击&#x200B;**+创建规则**。

![决策规则](./images/rules.png)

然后，您将看到Adobe Experience Platform的受众创建界面。

![决策规则](./images/createrule1.png)

您现在可以访问实时客户个人资料的合并架构中的所有字段，并且可以构建任何规则。

另外，您只需转到&#x200B;**受众** > ``--aepTenantId--``，即可在Adobe Experience Platform中重复使用已定义的受众。

您随后将看到以下内容：

![决策规则](./images/decisionruleaud.png)

如果需要，您现在可以配置自己的规则。 在本练习中，您将需要两个规则：

- 全部 — 男性客户
- 全部 — 女性客户

如果这些规则尚不存在，请创建它们。 如果规则已存在，请使用这些规则，并且不要创建新规则。

用于生成规则的属性是&#x200B;**XDM Individual Profile** > **人员** > **性别**。

例如，以下是规则&#x200B;**all - Male Customers**&#x200B;的规则定义：

![决策规则](./images/allmale.png)

例如，以下是规则&#x200B;**all - Female Customers**&#x200B;的规则定义：

![决策规则](./images/allfemale.png)

## 3.3.1.5选件

转到&#x200B;**选件**&#x200B;并选择&#x200B;**选件**。 单击&#x200B;**+创建选件**。

![决策规则](./images/offers1.png)

然后您会看到此弹出窗口。

![决策规则](./images/offers2.png)

现在不创建任何选件 — 您将在下一个练习中创建任何选件。

现在，您会看到有两种类型的选件：

- 个性化优惠
- 后备优惠

个性化优惠是在特定情况下应显示的特定内容。 个性化优惠是专门构建的，可在满足特定条件时提供个性化和情境式体验。

后备优惠是在未满足个性化优惠标准时显示的优惠。

## 3.3.1.6决定

决策将投放位置、个性化优惠集合和备用优惠组合在一起，由Offer Decisioning引擎最终用于根据每个单独的个性化优惠特征（如优先级、资格限制和总/用户上限）为特定用户档案查找最佳优惠。

要配置您的&#x200B;**决策**，请单击&#x200B;**决策**。

![决策规则](./images/activity.png)

在下一个练习中，您将配置自己的优惠和决策。

## 后续步骤

转到[3.3.2配置优惠和决定](./ex2.md){target="_blank"}

返回[Offer Decisioning](offer-decisioning.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
