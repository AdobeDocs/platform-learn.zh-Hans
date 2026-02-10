---
title: 在Adobe Journey Optimizer中使用Dynamic Media模板
description: 在Adobe Journey Optimizer中使用Dynamic Media模板
kt: 5342
doc-type: tutorial
exl-id: 0dd499cc-ec3b-42c3-9c08-6512ea5b9377
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

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

您应该会看到此内容。 你也是。 请注意允许您更改Dynamic Media模板参数的&#x200B;**PARAMETERS**。

![Journey Optimizer](./images/gsemail33.png)

## 1.4.2.2个性化Dynamic Media模板

如上一个练习中所述，AJO现在需要动态确定哪些值应该成为Dynamic Media模板的一部分。

与上一个练习中的&#x200B;**预览**&#x200B;步骤一样，**city_paris**、**city_dubai**&#x200B;和&#x200B;**city_ny**&#x200B;字段应设置为1，这意味着这些图像将被隐藏。

对于字段&#x200B;**title**，单击个性化图标。

![Journey Optimizer](./images/gsemail34.png)

用以下替换默认文本： `Hi {{profile.person.name.firstName}}`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/gsemail35.png)

对于字段&#x200B;**body**，单击个性化图标。

![Journey Optimizer](./images/gsemail36.png)

用以下替换默认文本： `CitiSignal is coming to {{profile.homeAddress.city}}!`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/gsemail37.png)

确保字段&#x200B;**`dynamic_city_hide`**&#x200B;设置为0。 单击字段&#x200B;**`dynamic_city_image`**&#x200B;的个性化图标。

![Journey Optimizer](./images/gsemail38.png)

用以下替换默认文本： `--aepUserLdap--CitiSignalDM/citisignal-fiber-max-is-coming_citisignal-{{profile._experienceplatform.individualCharacteristics.fiber_rollout.closest_rollout_city}}-1`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/gsemail39.png)

您应该会看到此内容。 由于动态变量在电子邮件编辑器的上下文中不可用，因此此处不再呈现图像。

单击&#x200B;**保存**。

![Journey Optimizer](./images/gsemail40.png)

最常测试您的配置，单击&#x200B;**模拟内容**，然后选择&#x200B;**模拟内容**。

![Journey Optimizer](./images/gsemail41.png)

然后您应该会看到类似这样的内容。 如果您没有可用的测试配置文件，则可以转到&#x200B;**管理测试配置文件**&#x200B;来添加它们。

一旦您的测试配置文件可用，其中包含测试此用例所需的数据，您就可以从一个配置文件切换到另一个配置文件，查看更改是否动态发生。

这是一个与纽约转出城市相关的个人资料。

![Journey Optimizer](./images/gsemail42.png)

这是一个与巴黎转出城市相关联的用户档案。

![Journey Optimizer](./images/gsemail43.png)

这是一段与迪拜转出城市相关的资料。

单击&#x200B;**关闭**。

![Journey Optimizer](./images/gsemail44.png)

您现在已经完成了此练习。 无需发布电子邮件营销活动。

## 后续步骤

返回[Adobe Experience Manager Assets和Dynamic Media](./aemassetsdm.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}