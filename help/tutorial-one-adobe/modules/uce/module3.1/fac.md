---
title: 数据收集 — 联合受众构成
description: 数据收集 — 联合受众构成
kt: 5342
doc-type: tutorial
exl-id: cc2ac85e-e902-4bb7-ab54-aa39980f97aa
source-git-commit: 71fe7b82e09aa9bc26b03dd2358d008265f54629
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 3.1联合受众构成

在本模块中，目标是了解有关使用联合受众组合创建受众的所有信息。

Experience Platform中的联合受众构成(FAC)允许您通过企业数据仓库中的相应高价值属性访问和创建受众，这些属性丰富和补充了Experience Platform中的实时客户配置文件和受众，从而改进了分段、定位、激活和交付有影响力的客户体验。 使用联合受众合成，可通过元数据链接远程数据库来创建虚拟数据库。 此方法简化了访问，减少了重复，并增强了最终用户体验。 在为参与工作流组合受众时，团队可以灵活地将数据集直接摄取到Experience Platform中或访问数据仓库中的数据集。 此方法利用Data Warehouse投资和资产来补充Real-Time CDP和Journey Optimizer。 联合受众构成使客户能够跨关键的新用例模式利用和组合批量功能和实时功能：

- 联合受众分段：团队可以使用Real-Time CDP和Journey Optimizer中对营销人员友好的拖放受众合成UI创作受众，但将查询推送到Data Warehouse，从而将敏感的基础数据保留在仓库中而不会出现重复，并且提供对基本数据集的灵活访问。
- 受众扩充：在Real-Time CDP和Journey Optimizer中构建的受众可以使用其他企业数据进行扩充，以使用不会在Adobe Experience Platform中持久保留的更多基于配置文件和不基于配置文件的数据集来改进定位和个性化。 例如，零售品牌可用一系列“顶级实体店面”来补充最近在线购买者的受众，以构建跨渠道在线和店内促销的受众。
- 配置文件扩充：团队可以从数据仓库中选择配置文件属性，这些配置文件属性对于将即刻体验保留在Real-Time CDP中并通过Journey Optimizer访问的可操作客户配置文件中至关重要。 然后，这些附加数据点可用于下游分段和由事件行为触发的个性化，具体取决于用户操作和客户用例。 这将允许随联合受众一起提供的属性与保留在客户配置文件中的其他属性和行为信号一起用于即时分段和个性化。

联合受众组合为Real-Time CDP和Journey Optimizer客户提供了灵活性，让他们可以决定什么时候要使用哪些数据，并帮助避免不必要的数据集或集成模式重复。 这是联合方法的独特组合，联合方法使用企业数据策划受众和高价值属性，并且系统针对当下跨渠道参与进行了优化。 这减少了数据移动，但也带来了利用高价值受众和属性实现跨渠道一致的低延迟激活的新机会。

## 学习目标

- 了解如何将Snowflake与Adobe Experience Platform连接
- 了解如何在Adobe Experience Platform中为联合数据创建数据模型
- 了解如何在Adobe Experience Platform中创建联合受众合成

## 先决条件

- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Snowflake数据仓库

## 练习

[3.1.1设置您的Snowflake环境](./ex1.md)

在本练习中，您将设置Snowflake试用帐户，并将其连接到Adobe Experience Platform

[3.1.2创建架构、数据模型和链接](./ex2.md)

在本练习中，您将在AEP中为联合数据配置数据模型。

[3.1.3创建联合组合](./ex3.md)

在本练习中，您将在AEP中为联合数据配置数据模型。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>![技术内部人士](./../../../assets/images/techinsiders.png){width="50px" align="left"}
>
>如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](../../../overview.md)
