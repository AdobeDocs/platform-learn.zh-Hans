---
title: Experience Decisioning - Experience Decisioning 101
description: Experience Decisioning - Experience Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 3.7.1 Experience Decisioning 101

## 3.7.1.1术语

要更好地了解Experience Decisioning，我们强烈建议您阅读有关Offer Decisioning应用程序服务如何与Adobe Experience Platform配合使用的[概述](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en)。

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

## 3.7.1.2体验决策

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 然后，您将进入沙盒&#x200B;**的**&#x200B;主页`--aepSandboxName--`视图。

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

在下一个练习中，您将配置自己的优惠和决策。

## 后续步骤

转到[3.7.2配置优惠和决定](./ex2.md){target="_blank"}

返回至[Experience Decisioning](ajo-decisioning.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
