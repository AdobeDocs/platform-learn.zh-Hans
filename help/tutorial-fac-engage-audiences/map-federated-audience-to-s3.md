---
title: 将联合受众映射到S3
seo-title: Map a federated audience to S3 | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: 将联合受众映射到S3
description: 在本练习中，我们会将联合受众映射到下游Real-Time CDP目标，以支持个性化的离线体验。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 将联合受众映射到S3以利用受众属性进行扩充

您可以利用Data Warehouse中的受众属性，让受众在使用RTCDP目标的下游激活工作流中更加丰富。 对于SecurFinancial，这些联合属性可用于增强客户受众的离线个性化体验。 以下，联合受众映射到预配置的Amazon S3目标。

## 步骤

1. 导航到&#x200B;**目标**&#x200B;门户。

2. 单击预配置的Amazon S3目标旁边的&#x200B;**3点菜单**&#x200B;按钮，然后单击&#x200B;**激活受众**。

   ![激活受众](assets/activate-audiences.png)

3. 选择&#x200B;**S3目标**，然后单击&#x200B;**下一步**。

   ![select-s3-destination](assets/select-s3-destination.png)

4. 选择相应的受众。 在我们的示例中：**SecureFinancial客户 — 无贷款，信用良好**&#x200B;受众。

   ![select-s3-audience](assets/select-s3-audience.png)

5. 在&#x200B;**计划**&#x200B;部分中，使用默认设置并单击&#x200B;**下一步**。

6. 在&#x200B;**映射**&#x200B;步骤中，选择重复数据消除键。 在我们的示例中，`xdm: personalEmail.address`被包含并选为&#x200B;**重复数据消除键**。 然后单击&#x200B;**下一步**：

   ![重复数据删除键](assets/deduplication-key.png)

7. 在映射步骤中，根据联合受众构成中的受众字段映射选择扩充属性。 单击&#x200B;**铅笔（编辑）**&#x200B;图标以查看预先选定的属性。

   ![编辑属性](assets/edit-attributes.png)

   ![最终属性](assets/final-attribution.png)

8. 查看您的受众映射并点击&#x200B;**完成**。

>[**!SUMMARY**]
>
> 我们已成功构建受众并轻松将其激活到S3目标。 这个用户友好的界面允许营销团队快速构建和激活受众，而无需移动基础数据。

现在我们将[构建历程](build-journey-federated-audience.md)。
