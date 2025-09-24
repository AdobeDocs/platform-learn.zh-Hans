---
title: 智能服务 — 客户人工智能数据准备（引入）
description: 客户人工智能 — 数据准备（引入）
kt: 5342
doc-type: tutorial
exl-id: 2b49d86a-af75-4ecd-ab3f-0182f3b8da2f
source-git-commit: 15adbf950115f0b6bb6613e69a60b310f25de058
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---

# 2.2.1客户人工智能 — 数据准备（引入）

为了使智能服务从营销事件数据中发掘洞察信息，必须在语义上丰富并维护标准结构中的数据。 智能服务可利用Adobe的Experience Data Model (XDM)架构来实现这一点。
具体而言，在智能服务中使用的所有数据集都必须符合**使用者体验事件** XDM架构。

## 创建架构

在本练习中，您将创建一个包含&#x200B;**消费者体验事件mixin**&#x200B;的架构，它是&#x200B;**客户人工智能**&#x200B;智能服务所必需的。

通过转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](../../datacollection/dc1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](../../datacollection/dc1.2/images/sb1.png)

从左侧菜单中，单击&#x200B;**架构**&#x200B;并转到&#x200B;**浏览**。 单击&#x200B;**创建架构**。

![创建新架构](./images/createschemabutton.png)

在弹出窗口中，选择&#x200B;**手动**&#x200B;并单击&#x200B;**选择**。

![创建新架构](./images/schmanual.png)

接下来，选择&#x200B;**体验事件**，然后单击&#x200B;**下一步**。

![创建新架构](./images/xdmee.png)

您需要立即为架构提供一个名称。 作为架构的名称，请使用以下名称： `--aepUserLdap-- - Demo System - Customer Experience Event`并单击&#x200B;**完成**。

![创建新架构](./images/schname.png)

你会看到这个。 单击“字段组”下的&#x200B;**+添加**。

![创建新架构](./images/xdmee1.png)

搜索并选择以下&#x200B;**字段组**&#x200B;以添加到此架构：

- 使用者体验事件

![新CEE架构](./images/cee1.png)

- IdentityMap

单击&#x200B;**添加字段组**。

![新CEE架构](./images/cee2.png)

你会看到这个。 接下来，选择架构的名称。 您现在应通过单击&#x200B;**配置文件**&#x200B;切换来启用&#x200B;**配置文件**&#x200B;的架构。

![创建新架构](./images/xdmee3.png)

你会看到这个。 选中&#x200B;**此架构的数据将在identityMap字段中包含主标识的复选框。**&#x200B;的问题。单击&#x200B;**启用**。

![创建新架构](./images/xdmee4.png)

您现在应该拥有此项。 单击&#x200B;**保存**&#x200B;以保存您的架构。

![创建新架构](./images/xdmee5.png)

## 创建数据集

从左侧菜单中，单击&#x200B;**数据集**&#x200B;并转到&#x200B;**浏览**。 单击&#x200B;**创建数据集**。

![数据集](./images/createds.png)

单击&#x200B;**从架构创建数据集**。

![数据集](./images/createdatasetfromschema.png)

在下一个屏幕中，选择您在上一个练习中创建的数据集，其名称为`--aepUserLdap-- - Demo System - Customer Experience Event`。 单击&#x200B;**下一步**。

![数据集](./images/createds1.png)

作为数据集的名称，请使用`--aepUserLdap-- - Demo System - Customer Experience Event Dataset`。 单击&#x200B;**完成**。

![数据集](./images/createds2.png)

您的数据集现已创建。 启用&#x200B;**配置文件**&#x200B;切换。

![数据集](./images/createds3.png)

单击&#x200B;**启用**。

![数据集](./images/createds4.png)

您现在应该拥有以下权限：

![数据集](./images/createds5.png)

您现在可以开始摄取消费者体验事件数据并开始使用客户人工智能服务。

## 下载体验事件测试数据

在配置&#x200B;**架构**&#x200B;和&#x200B;**数据集**&#x200B;后，您现在可以摄取体验事件数据了。 由于客户人工智能要求具有特定数据要求，因此您将需要摄取外部准备的数据。

为本练习中的体验事件准备的数据必须符合[使用者体验事件XDM字段组](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)的要求和架构。

请从以下位置下载包含演示数据的zip文件： [https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip](https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip)。

您现在已下载名为&#x200B;**CUSTOM-CAI-EVENTS-WEB.zip**&#x200B;的文件。 将文件放在计算机的桌面上并解压缩，之后您将看到名为&#x200B;**CUSTOM-CAI-EVENTS-WEB**&#x200B;的文件夹。

![数据集](./images/ingest.png)

在该文件夹中，您将找到多个已排序的json文件，在下个练习中需要摄取这些文件。

![数据集](./images/ingest1a.png)

## 摄取体验事件测试数据

在Adobe Experience Platform中，转到&#x200B;**数据集**&#x200B;并打开名为&#x200B;**[!UICONTROL ldap - Demo System - Customer Experience Event数据集]**&#x200B;的数据集。

![数据集](./images/ingest1.png)

在数据集中，单击&#x200B;**选择文件**&#x200B;以添加数据。

![数据集](./images/ingest2.png)

在弹出窗口中，选择文件&#x200B;**WEBSITE-EE-1.json**，直到&#x200B;**WEBSITE-EE-5.json**，然后单击&#x200B;**打开**。

![数据集](./images/ingest3.png)

对文件&#x200B;**WEBSITE-EE-6.json**&#x200B;和&#x200B;**WEBSITE-EE-7.json**&#x200B;重复此摄取过程。

然后，您将看到正在导入的数据，并会在&#x200B;**正在加载**&#x200B;状态下创建新批次。 在上传文件之前，请勿导航离开此页面。

![数据集](./images/ingest4.png)

上传文件后，您会看到批次状态从&#x200B;**正在加载**&#x200B;更改为&#x200B;**正在处理**。

![数据集](./images/ingest5.png)

摄取和处理数据可能需要10-20分钟。

数据摄取成功后，各种上传的批次状态将更改为&#x200B;**成功**。

![数据集](./images/ingest7.png)

## 后续步骤

转到[2.2.2 Customer AI — 创建新实例（配置）](./ex2.md){target="_blank"}

返回[智能服务](./intelligent-services.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
