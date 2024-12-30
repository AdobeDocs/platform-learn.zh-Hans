---
title: Adobe Journey Optimizer — 在电子邮件中应用个性化
description: 此练习介绍了如何在电子邮件内容中使用区段个性化
kt: 5342
doc-type: tutorial
exl-id: bb5f8130-0237-4381-bc1e-f6b62950b1fc
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# 3.4.3在电子邮件中应用个性化设置

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Experience Cloud。 单击&#x200B;**Adobe Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepTenantId--``。

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.3.1基于区段的个性化

在本练习中，您将使用基于区段会员资格的个性化文本来改进新闻稿电子邮件。

转到&#x200B;**历程**。 查找您在上一个练习中创建的新闻稿历程。 搜索`--aepUserLdap-- - Newsletter`。 单击您的历程以将其打开。

![Journey Optimizer](./images/sbp1.png)

你会看到这个。 单击&#x200B;**复制**。

![Journey Optimizer](./images/sbp2.png)

单击&#x200B;**复制**。

![Journey Optimizer](./images/sbp3.png)

选择您的&#x200B;**电子邮件**&#x200B;操作，然后单击&#x200B;**编辑内容**。

![Journey Optimizer](./images/sbp3a.png)

单击&#x200B;**向Designer发送电子邮件**。

![Journey Optimizer](./images/sbp4.png)

你会看到这个。

![Journey Optimizer](./images/sbp5.png)

打开&#x200B;**内容组件**，并将&#x200B;**文本**&#x200B;组件拖动到当前新闻稿内容下方。

![Journey Optimizer](./images/sbp6.png)

选择整个默认文本并将其删除。 然后单击工具栏中的&#x200B;**添加个性化**&#x200B;按钮。

![Journey Optimizer](./images/sbp7.png)

您随后将看到以下内容：

![Journey Optimizer](./images/seg1.png)

在左侧菜单中，单击&#x200B;**区段成员资格**。

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>如果在此列表中找不到您的区段，请向下滚动一点，查找有关如何手动检索区段ID的说明。

选择区段`Luma - Women's Category Interest`并单击&#x200B;**+**&#x200B;图标，它应该如下所示：

![Journey Optimizer](./images/seg3.png)

然后，您应该保留第一行不变，并用以下代码替换第2行和第3行：

``
    Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
    Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

然后，您将拥有以下权限：

![Journey Optimizer](./images/seg4.png)

单击&#x200B;**验证**&#x200B;以确保代码正确。 单击&#x200B;**保存**。

![Journey Optimizer](./images/sbp8.png)

您现在可以通过单击右上角的&#x200B;**保存**&#x200B;按钮保存此消息。 然后，单击&#x200B;**模拟内容**。

![Journey Optimizer](./images/sbp9.png)

选择作为本教程的一部分创建的其中一个配置文件，然后单击&#x200B;**预览**。 然后，您将看到配置的结果。

![Journey Optimizer](./images/sbp10.png)

你会看到这个。 然后，单击&#x200B;**关闭**。

![Journey Optimizer](./images/sbp10fff.png)

单击左上角主题行文本旁边的&#x200B;**箭头**，返回消息仪表板。

![Journey Optimizer](./images/sbp11.png)

单击左上角的箭头可返回您的历程。

![Journey Optimizer](./images/oc79afff.png)

单击&#x200B;**确定**&#x200B;以关闭您的电子邮件操作。

![Journey Optimizer](./images/oc79bfff.png)

将您的&#x200B;**计划**&#x200B;更改为&#x200B;**一次**&#x200B;并定义&#x200B;**日期/时间**。 单击&#x200B;**确定**。

>[!NOTE]
>
>消息发送日期和时间必须在一小时以上。

![Journey Optimizer](./images/sbp18.png)

单击历程中的&#x200B;**Publish**&#x200B;按钮。

![Journey Optimizer](./images/sbp19.png)

在弹出窗口中，再次单击&#x200B;**Publish**。

![Journey Optimizer](./images/sbp20.png)

您的基本新闻稿历程现已发布。 将根据您的计划发送您的新闻稿电子邮件，一旦发送完最后一封电子邮件，您的历程将立即停止。

![Journey Optimizer](./images/sbp20fff.png)

您已完成此练习。

下一步： [3.4.4为iOS设置和使用推送通知](./ex4.md)

[返回模块3.4](./journeyoptimizer.md)

[返回所有模块](../../../overview.md)
