---
title: 创建联合受众
seo-title: Create a federated audience | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: 创建联合受众
description: 在本练习中，我们将使用联合受众组合从Snowflake Data Warehouse创建一个受众。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a507cab5-dba9-4bf7-a043-d7c967e9e07d
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 创建联合受众

接下来，我们将指导您使用联合受众合成，从Snowflake Data Warehouse中创建受众。 受众包括信用积分为650分或以上且目前其SecurFinancial组合中无贷款的SecurFinancial客户。

## 步骤

1. 在&#x200B;**客户>受众**&#x200B;门户中，单击&#x200B;**联合合成**&#x200B;选项卡。
2. 单击&#x200B;**创建合成**。

   ![创建合成](assets/create-composition.png)

3. 为合成设置标签。 在我们的示例中： `SecurFinancial Customers - No Loans, Good Credit`。 单击&#x200B;**创建**。

4. 单击画布中的&#x200B;**+**&#x200B;按钮并选择&#x200B;**生成受众**。 出现右侧边栏。

5. 单击&#x200B;**选择架构**，选择适当的架构，然后单击&#x200B;**确认**。

6. 单击&#x200B;**继续**。 在查询生成器窗口中，单击&#x200B;**+**&#x200B;按钮，然后单击&#x200B;**自定义条件**。 编写条件。 我们的示例使用：

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *最后一个条件可确保使用营销偏好设置数据对选择电子邮件作为其首选通信渠道的客户进行分段*。

   **注意：**&#x200B;值字段区分大小写。

   ![查询生成器](assets/query-builder.png)

7. 单击下一个&#x200B;**+**&#x200B;按钮，然后单击&#x200B;**保存受众**。 为此步骤设置标签。 在我们的示例中，我们将它标记为`SecurFinancial Customers - No Loans, Good Credit`。

8. 添加相关的受众映射。 在此示例中：

   - **Source受众字段：**&#x200B;电子邮件
   - **Source受众字段：**&#x200B;当前产品
   - **Source受众字段：**&#x200B;名字

9. 选择用于配置文件的主要身份和命名空间。 以下是用于数据的标识和字段：

   - **主标识字段：**&#x200B;电子邮件
   - **身份命名空间：**&#x200B;电子邮件

10. 单击&#x200B;**保存**，然后单击&#x200B;**开始**&#x200B;以运行组合查询。

>[**摘要**]
>
> 在此示例中，产品和信用信息用于通过直接访问Snowflake中的企业数据来构建受众，而无需将其复制到Adobe Experience Platform。 一旦外部系统处理了查询，就只有相关的电子邮件、当前产品和名字值会引入受众定义以进行下游激活。 这适用于RTCDP支持的所有目标。

有关受众组合的详细信息，请访问[Experience League](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}。

现在已创建联合受众，我们将[将其映射到S3帐户](map-federated-audience-to-s3.md)。
