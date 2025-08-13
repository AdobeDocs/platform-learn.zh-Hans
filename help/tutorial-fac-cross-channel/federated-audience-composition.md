---
title: 使用联合数据丰富Experience Platform受众
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 使用联合数据丰富Experience Platform受众
description: 在此可视化练习中，Experience Platform受众使用联合数据进行了扩充。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: 0bbdc93969b4716407ecf51499d572cb50f5a0d3
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---


# 使用联合数据丰富Experience Platform受众

联合受众组合允许您利用从企业数据仓库联合的组合受众数据来扩充Adobe Experience Platform (AEP)中的现有受众。 该数据不会保留在 Adobe Experience Platform 客户轮廓中。

## 在联合组合中读取AEP受众

在此可视化练习中，我们使用存储在AEP配置文件服务中的&#x200B;**SecurFinancial贷款申请页面访客**&#x200B;受众启动联合合成。 它使用Snowflake中的联合数据，根据信用评分和贷款活动确定预批准。

![federated-composition-example](assets/snowflake-preapproval.png)

### 步骤

1. **将AEP受众**&#x200B;映射到联合受众组合目标。
2. **将映射的受众作为读取受众来构建合成**。
3. **协调读取受众中的身份**&#x200B;以连接联合数据。

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

我们将看另一个使用联合数据来[支持“即时”个性化](drive-in-the-moment-personalization.md)的示例！
