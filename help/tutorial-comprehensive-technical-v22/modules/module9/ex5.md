---
title: offer decisioning — 在电子邮件中使用您的决策
description: 通过电子邮件使用您的决策
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0fb8c244-1025-479f-b82e-374d1aa5e4dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 11%

---

# 9.5通过电子邮件使用您的决策

在本练习中，您将利用自己的决定来个性化电子邮件和短信的投放。

转到 **历程**. 查找在练习7.2中创建的历程，该历程名为 `--demoProfileLdap-- - Account Creation Journey`. 单击您的历程以将其打开。

![Journey Optimizer](./images/emailoffer1.png)

然后你会看到这个。 单击 **创建新版本**.

![Journey Optimizer](./images/journey1.png)

单击 **创建新版本**.

![Journey Optimizer](./images/journey2.png)

单击 **电子邮件** 操作，然后单击 **编辑内容**.

![Journey Optimizer](./images/journey3.png)

然后，您将看到消息仪表板。 单击 **Email Designer**.

![Journey Optimizer](./images/emailoffer2.png)

然后你会看到这个。

![Journey Optimizer](./images/emailoffer5.png)

然后你会看到这个。 拖动新 **1:1列** 结构组件。

![Journey Optimizer](./images/emailoffer6.png)

在菜单中，转到 **内容组件**. 选择 **优惠决策** 组件，并将此组件拖放到电子邮件的内容选件占位符中，如所示。 然后，单击 **添加**.

![Journey Optimizer](./images/emailoffer7.png)

选择要包含在电子邮件中的版面类型。 在 **版面** 下拉菜单选择 **电子邮件 — 图像**，然后选择您的决定 `--demoProfileLdap-- - Luma Decision`. 单击&#x200B;**添加**。

![Journey Optimizer](./images/emailoffer8.png)

现在，您会在电子邮件设计器中看到所有个性化选件和备用选件。 单击  **模拟内容** 用真实的客户用户档案预览电子邮件。

![Journey Optimizer](./images/emailoffer9.png)

首先，确定要用于预览的用户档案。 选择 **电子邮件** 命名空间，然后输入您在演示网站上创建的客户用户档案的电子邮件地址。 接下来，单击 **预览**.

![Journey Optimizer](./images/emailoffer10.png)

显示电子邮件并正确显示选件后，单击 **关闭** 按钮。

![Journey Optimizer](./images/emailoffer11.png)

最后，单击 **保存**.

![Journey Optimizer](./images/emailoffer12.png)

现在，单击箭头以返回到上一个屏幕。

![Journey Optimizer](./images/emailoffer13.png)

然后你会看到这个。 单击左上角的箭头以返回您的历程。

![Journey Optimizer](./images/emailoffer14.png)

单击 **确定** 关闭 **电子邮件** 操作。

![Journey Optimizer](./images/emailoffer14a.png)

单击 **发布** 以发布更新的历程。

![Journey Optimizer](./images/emailoffer14b.png)

单击以确认 **发布** 再次。

![Journey Optimizer](./images/emailoffer15.png)

您的消息现已发布。

![Journey Optimizer](./images/emailoffer16.png)

在演示网站上创建新帐户时，您现在将收到以下电子邮件：

![Journey Optimizer](./images/emailoffer17.png)

您已完成此练习。

下一步： [9.6使用API测试您的决策](./ex6.md)

[返回模块9](./offer-decisioning.md)

[返回到所有模块](./../../overview.md)
