---
title: 创建受众
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 创建受众
description: 在本课程中，我们将在Adobe Experience Platform与您的企业Data Warehouse之间配置连接以启用联合受众合成。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 3%

---


# 受众创建练习

本练习将指导您使用联合受众合成从Data Warehouse创建受众。 我们构建受众，以授予信用积分为650分或以上且目前其SecurFinancial组合中无贷款的SecurFinancial客户资格。

## 步骤

1. 在&#x200B;**客户>受众**&#x200B;门户中，单击&#x200B;**联合合成**&#x200B;选项卡。
2. 单击&#x200B;**创建合成**。

   ![创建合成](assets/create-composition.png)

3. 将合成标记为`SecurFinancial Customers - No Loans, Good Credit`。 单击&#x200B;**创建**。

4. 单击画布中的&#x200B;**+**&#x200B;按钮并选择&#x200B;**生成受众**。 将显示右侧边栏。

5. 单击&#x200B;**选择架构**&#x200B;并选择&#x200B;**FSI_CRM**&#x200B;架构，然后单击&#x200B;**确认**。

6. 单击&#x200B;**继续**。 在查询生成器窗口中，单击&#x200B;**+**&#x200B;按钮，然后单击&#x200B;**自定义条件**。 创建以下条件：

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *最后一个条件可确保使用营销偏好设置数据对选择电子邮件作为其首选通信渠道的客户进行分段*。

   **注意：**&#x200B;值字段区分大小写。

   现在，您的查询应如下所示：

   ![查询生成器](assets/query-builder.png)

7. 单击下一个&#x200B;**+**&#x200B;按钮，然后单击&#x200B;**保存受众**。 将此步骤标记为`SecurFinancial Customers - No Loans, Good Credit`。 使用与受众标签相同的值。

8. 添加以下受众映射：

   - **Source受众字段：**&#x200B;电子邮件
   - **Source受众字段：**&#x200B;当前产品
   - **Source受众字段：**&#x200B;名字

9. 选择用于配置文件的主要身份和命名空间：

   - **主标识字段：**&#x200B;电子邮件
   - **身份命名空间：**&#x200B;电子邮件

10. 单击&#x200B;**保存**，然后单击&#x200B;**开始**&#x200B;以运行刚刚构建的组合查询。

**注意：**&#x200B;我们使用产品和信用信息构建受众，这些受众未将敏感数据（如信用分数）移动到下游平台进行激活。

有关受众组合的详细信息，请访问[Experience League](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}。

现已创建联合受众，我们将继续[将其映射到S3帐户](map-federated-audience-to-s3.md)。
