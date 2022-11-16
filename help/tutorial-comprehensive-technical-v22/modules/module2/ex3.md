---
title: 基础 — 数据摄取 — 配置数据集
description: 基础 — 数据摄取 — 配置数据集
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 5afd987b-ccf8-414d-98aa-a485d6130c2e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 7%

---

# 2.3配置数据集

在本练习中，您将配置所需的数据集，以捕获和存储用户档案信息和客户行为。 您在此中创建的每个数据集都将使用您在上一步中构建的架构之一。

## Story

在定义了问题的答案之后 **这位客户是谁？** 和 **此客户会怎么做？** 应该类似，您现在需要创建一个使用该信息的存储段，以接收和验证发送到Adobe Experience Platform的数据。

## 2.3.1 — 创建数据集

您现在需要创建2个数据集：

- 1个数据集，用于捕获回答 **这位客户是谁？**  — 问题。
- 1个数据集，用于捕获回答 **此客户会怎么做？**  — 问题。

通过转到以下URL登录Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **[!UICONTROL 沙盒]**. 要选择的沙盒已命名 ``--module2sandbox--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在Adobe Experience Platform中，单击 **[!UICONTROL 数据集]** 菜单。  然后您将看到：

![数据获取](./images/menudatasets.png)

让我们首先创建数据集以捕获网站注册信息。

您应该创建新数据集。 要创建新数据集，请单击按钮 **[!UICONTROL +创建数据集]**.

![数据获取](./images/createdataset.png)

单击 **[!UICONTROL +创建数据集]** 按钮，您将看到以下屏幕。

![数据获取](./images/datasetsetup.png)

您必须使用上一步中定义的架构定义数据集。 单击 **[!UICONTROL 从架构创建数据集]**  — 选项。

![数据获取](./images/datasetfromschema.png)

在下一个屏幕中，您必须选择在1中创建的架构， `--demoProfileLdap-- - Demo System - Profile Schema for Website`.

![数据获取](./images/schemaselection.png)

选择架构后，单击 **[!UICONTROL 下一个]** 继续。

![数据获取](./images/next.png)

让我们为您的数据集命名。

对于数据集的名称，请使用以下代码：

`--demoProfileLdap-- - Demo System - Profile Dataset for Website`

例如，对于ldap **[!UICONTROL 万热卢]**，此应为架构的名称：

**[!UICONTROL vangeluw — 演示系统 — 网站的配置文件数据集]**

这应该会给你这样的东西：

![数据获取](./images/datasetname.png)

单击 **[!UICONTROL 完成]** 完成数据集配置。

![数据获取](./images/finish.png)

您现在将看到以下内容：

![数据获取](./images/dsoverview1.png)

返回到 [!UICONTROL 数据集] 概述。 此时，您将在概述中看到您创建的数据集弹出窗口。

![数据获取](./images/dsoverview2.png)

接下来，您将配置第二个数据集以捕获网站交互。

您应该创建新数据集。 要创建新数据集，请单击按钮 **[!UICONTROL +创建数据集]**.

![数据获取](./images/createdataset.png)

单击 **[!UICONTROL +创建数据集]** 按钮，您将看到以下屏幕。

![数据获取](./images/datasetsetup.png)

您必须使用上一步中定义的架构定义数据集。 单击 **[!UICONTROL 从架构创建数据集]**  — 选项。

![数据获取](./images/datasetfromschema.png)

在下一个屏幕中，您必须选择在2.2中创建的架构， `--demoProfileLdap-- - Demo System - Event Schema for Website`.

![数据获取](./images/schemaselectionee.png)

选择架构后，单击 **[!UICONTROL 下一个]** 继续。

![数据获取](./images/next.png)

让我们为您的数据集命名。

作为数据集的名称，我们将使用：

`--demoProfileLdap-- - Demo System - Event Dataset for Website`

例如，对于ldap **[!UICONTROL 万热卢]**，此应为架构的名称：

**[!UICONTROL vangeluw — 演示系统 — 网站的事件数据集]**

这应该会给你这样的东西：

![数据获取](./images/datasetnameee.png)

单击 **[!UICONTROL 完成]** 完成数据集配置。

![数据获取](./images/finish.png)

然后您将看到：

![数据获取](./images/finish1.png)

返回到 [!UICONTROL 数据集] “概述”屏幕。

![数据获取](./images/datasetsoverview.png)

现在，您必须将数据集纳入Adobe Experience Platform的实时客户资料。

打开数据集 `--demoProfileLdap--`  — 演示系统 — 单击网站的配置文件数据集。

找到 [!UICONTROL 用户档案] 切换图标。

![数据获取](./images/ds1.png)

单击 [!UICONTROL 用户档案] 切换为启用此数据集 [!UICONTROL 用户档案].

![数据获取](./images/ds2.png)

单击 **[!UICONTROL 启用]**.

![数据获取](./images/ds3.png)

您的数据集现在已启用 [!UICONTROL 用户档案].

返回数据集概述并打开数据集 `--demoProfileLdap-- - Demo System - Event Dataset` ，方法是单击网站。

找到 [!UICONTROL 用户档案] 切换图标。

![数据获取](./images/ds4.png)

单击 [!UICONTROL 用户档案] 切换为启用 [!UICONTROL 用户档案].

![数据获取](./images/ds2.png)

单击 **[!UICONTROL 启用]**.

![数据获取](./images/ds5.png)

您的数据集现在已启用 [!UICONTROL 用户档案].

下一步： [2.4从离线源摄取数据](./ex4.md)

[返回到模块2](./data-ingestion.md)

[返回到所有模块](../../overview.md)
