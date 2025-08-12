---
title: 使用联合数据丰富Experience Platform受众
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 使用联合数据丰富Experience Platform受众
description: 在本课程中，我们使用联合数据丰富了Experience Platform受众。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---


# 使用联合数据丰富Experience Platform受众

联合受众组合允许您利用从企业数据仓库联合的组合受众数据来扩充Adobe Experience Platform (AEP)中的现有受众。 该数据不会保留在 Adobe Experience Platform 客户轮廓中。

## 丰富联合受众构成的方法

丰富联合受众组合的主要方法有两种。

### 1.在联合组合中读取AEP受众

在第一个示例中，我们将使用存储在AEP的配置文件服务中的&#x200B;**SecurFinancial贷款申请页面访客**&#x200B;受众启动联合合成。 我们将使用Snowflake中的联合数据丰富受众，以根据信用评分和贷款活动确定预批准。

![federated-composition-example](assets/snowflake-preapproval.png)

1. **将AEP受众**&#x200B;映射到联合受众组合目标。
2. **将映射的受众作为读取受众来构建合成**。
3. **协调读取受众中的身份**&#x200B;以连接联合数据。

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

### 2.使用联合受众丰富Experience Platform受众规则

在第二个示例中，我们将使用通过信用评分和贷款活动查询的联合受众来丰富贷款申请网页访客的行为受众。

通过在Edge上评估此受众，我们可以立即在网站上使用个性化优惠重新定位预批准的贷款申请页面访客。

![边缘受众扩充](assets/edge-audience-enrich.png)

1. **保存并启动**&#x200B;联合受众合成。 运行构成后，联合受众将显示在受众门户中。
2. **使用配置文件服务中的配置文件属性和体验事件构建受众规则**，合并您的联合受众。

让我们用[学习总结和最终收获](conclusion.md)！
