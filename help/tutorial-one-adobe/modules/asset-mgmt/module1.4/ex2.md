---
title: 在Adobe Journey Optimizer中使用Dynamic Media模板
description: 在Adobe Journey Optimizer中使用Dynamic Media模板
kt: 5342
doc-type: tutorial
source-git-commit: 261475b85bfb15f7e9f630d1c5203732c2d4c254
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 1.4.2在Adobe Journey Optimizer中使用Dynamic Media模板

## 1.4.2.1在Adobe Journey Optimizer中创建您的营销活动

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 然后，您将进入沙盒&#x200B;**的**&#x200B;主页`--aepSandboxName--`视图。

![ACOP](./images/acoptriglp.png)

您现在将创建一个营销活动。 上一个练习基于事件的历程依赖于传入体验事件或受众进入或退出来触发1个特定客户的历程，与此不同的是，营销活动面向整个受众一次，其中包含新闻稿、一次性促销活动或通用信息等独特内容，或者定期发送类似内容，如实例生日营销活动和提醒。

在菜单中，转到&#x200B;**营销活动**&#x200B;并单击&#x200B;**创建营销活动**。

![Journey Optimizer](./images/gsemail21.png)

选择&#x200B;**计划 — 营销**，然后单击&#x200B;**创建**。

![Journey Optimizer](./images/gsemail22.png)

在营销活动创建屏幕上，配置以下内容：

- **名称**： `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`。

单击&#x200B;**操作**。

![Journey Optimizer](./images/gsemail23.png)

单击&#x200B;**+添加操作**，然后选择&#x200B;**电子邮件**。

![Journey Optimizer](./images/gsemail24.png)

然后，选择现有的&#x200B;**电子邮件配置**，然后单击&#x200B;**编辑内容**。

![Journey Optimizer](./images/gsemail25.png)

你会看到这个。 对于&#x200B;**主题行**，请使用以下内容：

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

接下来，单击&#x200B;**编辑内容**。

![Journey Optimizer](./images/gsemail26.png)

从头开始选择&#x200B;**设计**。

![Journey Optimizer](./images/gsemail27.png)

您应该会看到此内容。

![Journey Optimizer](./images/gsemail28.png)

将2x **1:1列**&#x200B;添加到画布。

![Journey Optimizer](./images/gsemail29.png)

转到&#x200B;**片段**，将&#x200B;**标题**&#x200B;片段拖动到第一个1:1列，然后将&#x200B;**页脚**&#x200B;片段拖动到第二个1:1列。

![Journey Optimizer](./images/gsemail30.png)

在2个片段之间添加新的1:1列，然后将&#x200B;**图像**&#x200B;添加到该1:1列。 然后，单击&#x200B;**浏览**。

![Journey Optimizer](./images/gsemail31.png)

导航到存储Dynamic Media模板的文件夹。 选择您的Dynamic Media模板，然后单击&#x200B;**选择**。

![Journey Optimizer](./images/gsemail32.png)

您应该会看到此内容。

![Journey Optimizer](./images/gsemail33.png)

## 后续步骤

返回[Adobe Experience Manager Assets和Dynamic Media](./aemassetsdm.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
