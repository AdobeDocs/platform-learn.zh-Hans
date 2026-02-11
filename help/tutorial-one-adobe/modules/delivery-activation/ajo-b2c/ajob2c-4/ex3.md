---
title: Adobe Journey Optimizer — 在电子邮件中应用个性化
description: 此练习介绍了如何在电子邮件内容中使用区段个性化
kt: 5342
doc-type: tutorial
exl-id: a1ad649e-d0c4-4e87-b784-1e2d99f34a2e
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 3.4.3在电子邮件中应用基于区段的个性化

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Experience Cloud。 单击&#x200B;**Adobe Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepTenantId--``。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.3.1基于区段的个性化

在本练习中，您将使用基于区段成员资格的个性化文本来改进您在上一个练习中创建的新闻稿电子邮件。

转到&#x200B;**营销活动**。 查找您在上一个练习中创建的新闻稿历程。 搜索`--aepUserLdap-- - CitiSignal Newsletter`。 右键单击3个点&#x200B;**...**，然后单击&#x200B;**复制**。

![Journey Optimizer](./images/sbp1.png)

你会看到这个。 将此项用于&#x200B;**标题**： `--aepUserLdap-- - CitiSignal Newsletter (SBP)`。 单击&#x200B;**复制**。

![Journey Optimizer](./images/sbp2.png)

单击重复的活动以将其打开。

![Journey Optimizer](./images/sbp3.png)

单击&#x200B;**编辑**&#x200B;以更改内容。

![Journey Optimizer](./images/sbp3a.png)

单击&#x200B;**编辑电子邮件正文**。

![Journey Optimizer](./images/sbp4.png)

你会看到这个。

![Journey Optimizer](./images/sbp5.png)

打开&#x200B;**内容组件**&#x200B;并将&#x200B;**1:1列**&#x200B;拖动到AirPods选件上方。

![Journey Optimizer](./images/sbp6.png)

将&#x200B;**Text**&#x200B;组件拖放到该1:1列中。

![Journey Optimizer](./images/sbp6a.png)

选择整个默认文本并将其删除。 然后单击工具栏中的&#x200B;**添加个性化**&#x200B;按钮。

![Journey Optimizer](./images/sbp7.png)

你会看到这个。 在左侧菜单中，单击&#x200B;**受众**。

![Journey Optimizer](./images/seg1.png)

选择区段`--aepUserLdap-- - Interest in Plans`并单击&#x200B;**+**&#x200B;图标以将其添加到画布。

![Journey Optimizer](./images/seg3.png)

然后，您应该保留第一行不变，并用以下代码替换第2行和第3行：

&grave;&grave;
    PS: It may be a good idea to check if your plan still meets your needs! Click here to be contacted by one of our experts!
{%else%}
    PS: Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: NEWSLETTER10
{%/if%}
&grave;&grave;

你就能拥有这个了。 单击&#x200B;**保存**。

![Journey Optimizer](./images/seg4.png)

将文本对齐方式更改为&#x200B;**居中对齐方式**。

![Journey Optimizer](./images/sbp9.png)

您现在可以通过单击右上角的&#x200B;**保存**&#x200B;按钮保存此消息。 然后，单击左上角主题行文本旁边的&#x200B;**箭头**。

![Journey Optimizer](./images/sbp9a.png)

单击&#x200B;**查看以激活**。

![Journey Optimizer](./images/oc79afff.png)

单击&#x200B;**激活**。

![Journey Optimizer](./images/oc79bfff.png)

您基于区段的个性化的新闻稿现已发布。 将根据您的计划发送您的新闻稿电子邮件，一旦发送完最后一封电子邮件，您的历程将立即停止。

如果您符合使用的区段的条件，将在您收到的电子邮件中看到以下内容：

![Journey Optimizer](./images/sbp20fff.png)

您已完成此练习。

## 后续步骤

返回[Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
