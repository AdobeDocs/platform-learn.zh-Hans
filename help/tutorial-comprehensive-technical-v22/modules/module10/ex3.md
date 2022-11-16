---
title: Adobe Journey Optimizer — 在电子邮件中应用个性化
description: 本练习说明了如何在电子邮件内容中使用区段个性化
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 573ecfba-4f1d-4242-8358-1d33109aaea3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 10%

---

# 10.3在电子邮件中应用个性化

通过转到Adobe Experience Cloud [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Adobe Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

您将被重定向到 **主页** 查看Journey Optimizer。 在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepTenantId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。

![ACOP](../module7/images/acoptriglp.png)

## 10.3.1基于区段的个性化

在本练习中，您将使用基于区段成员资格的个性化文本来改进新闻稿电子邮件消息。

转到 **历程**. 查找您在上一个练习中创建的Newsletter历程。 搜索 `--demoProfileLdap-- - Newsletter`. 单击您的历程以将其打开。

![Journey Optimizer](./images/sbp1.png)

然后你会看到这个。 单击 **复制**.

![Journey Optimizer](./images/sbp2.png)

单击**复制**。

![Journey Optimizer](./images/sbp3.png)

选择 **电子邮件** 操作并单击 **编辑内容**.

![Journey Optimizer](./images/sbp3a.png)

单击 **Email Designer**.

![Journey Optimizer](./images/sbp4.png)

然后你会看到这个。

![Journey Optimizer](./images/sbp5.png)

打开 **内容组件** 并拖动 **文本** 组件。

![Journey Optimizer](./images/sbp6.png)

选择整个默认文本并将其删除。 然后，单击 **添加个性化** 按钮。

![Journey Optimizer](./images/sbp7.png)

然后您将看到：

![Journey Optimizer](./images/seg1.png)

在左侧菜单中，单击 **区段成员资格**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>如果在此列表中找不到您的区段，请向下滚动一点以查找有关如何手动检索区段ID的说明。

选择区段 `Luma - Women's Category Interest` ，然后单击 **+** 图标，其应如下所示：

![Journey Optimizer](./images/seg3.png)

然后，您应当保持第一行原样，并使用以下代码替换第2行和第3行：

``
Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

然后，您将拥有：

![Journey Optimizer](./images/seg4.png)

单击 **验证** 以确保代码正确。 单击&#x200B;**保存**。

![Journey Optimizer](./images/sbp8.png)

现在，您可以通过单击 **保存** 按钮。 然后，单击 **模拟内容**.

![Journey Optimizer](./images/sbp9.png)

选择您在本教程中创建的其中一个用户档案，然后单击 **预览**. 然后，您将看到配置的结果。

![Journey Optimizer](./images/sbp10.png)

然后你会看到这个。 然后，单击 **关闭**.

![Journey Optimizer](./images/sbp10fff.png)

通过单击 **箭头** 主题行文本旁边的。

![Journey Optimizer](./images/sbp11.png)

单击左上角的箭头以返回您的历程。

![Journey Optimizer](./images/oc79afff.png)

单击 **确定** 以关闭电子邮件操作。

![Journey Optimizer](./images/oc79bfff.png)

更改 **计划** to **一次** 并定义 **日期/时间**. 单击 **确定**.

>[!NOTE]
>
>消息发送日期和时间必须在一小时内。

![Journey Optimizer](./images/sbp18.png)

单击 **发布** 按钮。

![Journey Optimizer](./images/sbp19.png)

在弹出窗口中，单击 **发布** 再次。

![Journey Optimizer](./images/sbp20.png)

您的基本新闻稿历程现已发布。 您的新闻稿电子邮件将根据您的计划发送，并且在发送最后一封电子邮件后，您的历程将立即停止。

![Journey Optimizer](./images/sbp20fff.png)

您已完成此练习。

下一步： [10.4为iOS设置和使用推送通知](./ex4.md)

[返回到模块10](./journeyoptimizer.md)

[返回到所有模块](../../overview.md)
