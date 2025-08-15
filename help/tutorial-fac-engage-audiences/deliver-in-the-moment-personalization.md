---
title: 使用Edge Network提供“即时”个性化
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: 使用Edge Network提供“即时”个性化
description: 在本练习中，将对Edge上的联合受众进行评估，以便进行即时“重定向”。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# 使用Edge Network提供“即时”个性化

联合受众组合允许您利用从企业数据仓库联合的组合受众数据来扩充Adobe Experience Platform (AEP)中的现有受众。 此数据将不会保留在Adobe Experience Platform中，但您可以使用[事件转发](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview){target="_blank"}功能将此数据直接发送到您的Data Warehouse。

在本练习中，我们使用通过信用评分和贷款活动查询的联合受众来丰富贷款申请网页访客的行为受众。

通过在Edge上评估此受众，我们立即在网站上使用个性化优惠重新定位预先批准的贷款申请页面访客。

![边缘受众扩充](assets/edge-audience-enrich.png)

## 步骤

1. **保存并启动**&#x200B;联合受众合成。 运行构成后，联合受众将显示在受众门户中。
2. **使用配置文件服务中的配置文件属性和体验事件构建受众规则**，合并您的联合受众。

让我们用[学习总结和最终收获](conclusion.md)！
