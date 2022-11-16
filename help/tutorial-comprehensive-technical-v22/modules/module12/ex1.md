---
title: 使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据 — 创建您的Google云平台帐户
description: 使用BigQuery Source Connector在Adobe Experience Platform中摄取和分析Google Analytics数据 — 创建您的Google云平台帐户
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 632ff2fe-ae56-4481-b281-c11224b18639
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# 12.1创建您的Google Cloud Platform帐户

## 目标

- 创建Google Cloud Platform帐户
- 熟悉Google Cloud Platform Console
- 创建并准备BigQuery项目

## 12.1.1为何将Google BigQuery连接到Adobe Experience Platform以获取Google Analytics数据

Google云平台(GCP)是Google提供的一套公共云计算服务。 Google云平台包含一系列托管服务，可用于在Google硬件上运行的计算、存储和应用程序开发。

BigQuery是其中一项服务，它始终包含在Google Analytics360中。 Google Analytics数据在我们尝试直接从中获取数据时（例如，API）通常会进行采样。 这就是为什么Google包含BigQuery来获取不采样的数据，因此品牌可以使用SQL进行高级分析并从GCP的强大功能中受益。

Google Analytics数据每天使用批处理机制加载到BigQuery中。 因此，使用此GCP/BigQuery集成进行实时个性化和激活用例没有任何意义。

如果品牌想要根据Google Analytics数据提供实时个性化用例，它可以使用Google标签管理器在网站上收集该数据，然后将其实时流式传输到Adobe Experience Platform。

GCP/BigQuery Source Connector应用于……

- 跟踪网站上的所有客户行为，并在Adobe Experience Platform中加载该数据，以便进行无需实时激活的分析、数据科学和个性化用例。
- 再次将Google Analytics历史数据加载到Adobe Experience Platform中，以便进行分析和数据科学用例

## 12.1.2创建Google帐户

要获取Google Cloud Platform帐户，您需要Google帐户。

## 12.1.3激活您的Google云平台帐户

现在，您已拥有Google帐户，接下来可以创建Google云平台环境。 为此，请转至 [https://console.cloud.google.com/](https://console.cloud.google.com/).

在下一页中，接受条款和条件。

![演示](./images/ex1/1.png)

接下来，单击 **选择项目**.

![演示](./images/ex1/2.png)

单击 **新建项目**.

![演示](./images/ex1/createproject.png)

按照以下命名约定命名项目：

| 公约 | 示例 |
| ----------------- |-------------| 
| `--demoProfileLdap---googlecloud` | delaigle-googlecloud |

![演示](./images/ex1/3.png)

单击&#x200B;**创建**。

![演示](./images/ex1/3-1.png)

等到屏幕右上方的通知告知您创建已完成。 然后，单击 **查看项目**.

![演示](./images/ex1/4.png)

接下来，转到屏幕顶部的搜索栏并键入 **BigQuery**. 选择第一个结果。

![演示](./images/ex1/7.png)

然后，您将被重定向到BigQuery控制台，并会看到一条弹出消息。

**单击完成**。

![演示](./images/ex1/5.png)

此模块的目标是将Google Analytics数据导入Adobe Experience Platform。 为此，我们需要Google Analytics数据集中的虚拟数据。

单击 **添加数据** ，然后单击 **浏览公共数据集**.

![演示](./images/ex1/18.png)

然后，您将看到此窗口：

![演示](./images/ex1/19.png)

输入搜索词 **Google Analytics示例** ，然后选择第一个结果。

![演示](./images/ex1/20.png)

您将在以下屏幕中看到数据集的说明。 单击 **查看数据集**.

![演示](./images/ex1/21.png)

然后，您将被重定向到BigQuery，您将在其中看到此内容 **bigquery-public-data** 数据集 **资源管理器**.

![演示](./images/ex1/22a.png)

在 **资源管理器**，此时您应会看到许多表。 随时探索。 转到 `google_analytics_sample`。

![演示](./images/ex1/22.png)

单击以打开表 `ga_sessions`.

![演示](./images/ex1/23.png)

在继续下一个练习之前，请在计算机上的单独文本文件中记下以下内容：

| 凭据 | 命名 | 示例 |
| ----------------- |-------------| -------------|
| 项目名称 | `--demoProfileLdap---googlecloud` | 万热卢 |
| 项目ID | random | comperent-task-306413 |

您可以通过单击 **项目名称** 在顶部菜单栏中：

![演示](./images/ex1/projectMenu.png)

然后，您会在右侧看到您的项目ID:

![演示](./images/ex1/projetcselection.png)

现在，您可以转到练习12.2 ，在练习中，您将通过查询Google Analytics数据来弄脏手。

下一步： [12.2在BigQuery中创建第一个查询](./ex2.md)

[返回到模块12](./customer-journey-analytics-bigquery-gcp.md)

[返回到所有模块](./../../overview.md)
