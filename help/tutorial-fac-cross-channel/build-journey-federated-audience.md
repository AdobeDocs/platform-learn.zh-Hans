---
title: 使用联合受众数据构建历程
seo-title: Build a journey with federated audience data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 使用联合受众数据构建历程
description: 在此可视化练习中，联合受众用于Journey Optimizer历程。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-build-a-journey-with-federated-audience-data.jpg
exl-id: a153667a-9b3a-4db7-9f58-b83e695009e0
source-git-commit: 15619a8419f608da6a77745fabf72c356a2ac4b4
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 1%

---

# 使用联合受众数据构建历程

联合受众可在Adobe Journey Optimizer (AJO)内的历程中使用。 这包括使用来自联合受众组合的查询属性来个性化消息传递。

为了继续介绍SecurFinancial案例，特别是客户重新定位和个性化用例，我们为预认证的客户策划了一个历程。 目标是根据从SecurFinancial的Data Warehouse联合的属性发送个性化电子邮件。

## 步骤

### 使用读取受众构建历程

1. 导航到&#x200B;**历程**&#x200B;门户，然后单击&#x200B;**创建历程**&#x200B;按钮。

   ![创建历程](assets/create-journey.png)

2. 使用新名称更新历程属性。 在我们的示例中： **`SecurFinancial - Home Loan Offer`**。

3. 单击&#x200B;**编排**，然后将&#x200B;**读取受众**&#x200B;磁贴拖放到画布上。

4. 单击屏幕右侧“受众”框旁边的&#x200B;**铅笔图标**。

5. 在搜索栏中，搜索受众。 在我们的示例中： **`SecureFinancial Customers - No Loans, Good Credit`**。 单击&#x200B;**保存**。

   ![创建历程](assets/select-audience.png)

6. 将所有设置保留为右侧菜单中的默认设置，然后单击“**保存**”。

   ![save-audience-settings](assets/save-audience-settings.png)

### 使电子邮件个性化

1. 单击&#x200B;**操作**，然后单击并将&#x200B;**电子邮件**&#x200B;拼贴拖到画布上。

2. 在右侧菜单中，单击&#x200B;**电子邮件配置**&#x200B;并选择&#x200B;**电子邮件营销**。 然后单击&#x200B;**编辑内容**。

3. 添加主题行。 在我们的示例中： **`Learn more about SecurFinancial Home Loan`**。 然后单击&#x200B;**编辑电子邮件正文**。

4. 单击右上角的&#x200B;**内容模板**&#x200B;按钮。 查找并选择相应的模板。 我们的示例使用`SecureFinancial Template`。 然后单击&#x200B;**确认**。

   ![journey-email-config](assets/journey-email-config.png)

   ![journey-email-confirm](assets/journey-email-confirm.png)

5. 查看模板并单击&#x200B;**使用模板**。

6. 您现在位于电子邮件Designer中。 将鼠标悬停在`{profile.person.name.firstName}`宏上并单击&#x200B;**个性化头像**。

7. 在个性化窗口中，向下展开至包含上传的联合受众的文件夹路径。 在我们的示例中： **`[sandbox] > audienceEnrichment > CustomerAudienceUpload`**

8. 单击&#x200B;**读取受众**&#x200B;文件夹。 您可以在此处找到联合受众的扩充属性。

9. 选择表达式生成器的&#x200B;**名字**&#x200B;属性。 电子邮件将动态地表示客户的名字值，以使电子邮件个性化。

10. 单击&#x200B;**保存**。

11. 现在，名字个性化已添加，请将`Hi, `添加到个性化变量之前。 然后单击&#x200B;**保存**。

    ![journey-email-save](assets/journey-email-save.png)

12. 单击&#x200B;**返回**&#x200B;按钮两次以返回历程画布。 然后在右侧的&#x200B;**操作：电子邮件**&#x200B;菜单中，单击&#x200B;**保存**。

   ![save-final-journey](assets/save-final-journey.png)

我们在AJO中使用联合受众和联合扩充属性创建了历程。

现在，我们将了解如何使用Experience Platform中的联合数据[扩充现有受众](federated-audience-composition.md)。
