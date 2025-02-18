---
title: 使用BigQuery Google Analytics Connector在Adobe Experience Platform中摄取和分析Source数据 — 创建您的Google Cloud Platform帐户
description: 使用BigQuery Google Analytics Connector在Adobe Experience Platform中摄取和分析Source数据 — 创建您的Google Cloud Platform帐户
kt: 5342
doc-type: tutorial
exl-id: ba830c8c-e3e6-4e7e-ab53-5b7eb031ad29
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# 1.2.1开始使用Google Cloud平台

>[!NOTE]
>
>在本练习中，您需要具有对Google Cloud Platform环境的访问权限。 如果您尚无法访问GCP，请使用您的个人电子邮件地址创建一个新帐户。

## 1.2.1.1为何将Google BigQuery连接到Adobe Experience Platform以获取Google Analytics数据

Google Cloud Platform (GCP)是Google提供的一套公共云计算服务。 Google云平台包括一系列托管服务，可用于在Google硬件上运行的计算、存储和应用程序开发。

BigQuery是这些服务之一，并且始终包含在Google Analytics 360中。 当我们尝试直接从其中（例如API）获取数据时，Google Analytics数据经常被采样。 正因如此，Google包含BigQuery来获取未采样的数据，这样品牌就可以使用SQL进行高级分析，并从GCP的强大功能中获益。

Google Analytics数据每天使用批处理机制加载到BigQuery中。 因此，将此GCP/BigQuery集成用于实时个性化和激活用例没有任何意义。

如果品牌想要基于Google Analytics数据提供实时个性化用例，它可以使用Google Tag Manager在网站上收集该数据，然后将其实时流式传输到Adobe Experience Platform。

GCP/BigQuery Source连接器应该用于……

- 跟踪网站上的所有客户行为，并将这些数据加载到Adobe Experience Platform中，以便进行无需实时激活的分析、数据科学和个性化用例。
- 将Google Analytics历史数据加载到Adobe Experience Platform，同样用于分析和数据科学用例

## 1.2.1.2您的Google帐户

>[!NOTE]
>
>在本练习中，您需要具有对Google Cloud Platform环境的访问权限。 如果您尚无法访问GCP，请使用您的个人电子邮件地址创建一个新帐户。

## 1.2.1.3选择或创建项目

转到[https://console.cloud.google.com/](https://console.cloud.google.com/)。

接下来，单击&#x200B;**选择项目**&#x200B;或单击现有项目。

![演示](./images/ex12.png)

如果您还没有项目，请单击&#x200B;**新建项目**。 如果您已经有一个项目，则可以选择选择该项目，然后继续下一步。

![演示](./images/ex1createproject.png)

按照此命名约定命名您的项目。 单击&#x200B;**创建**。

| 公约 |
| ----------------- |
| `--aepUserLdap---googlecloud` |

![演示](./images/ex13.png)

等到屏幕右上方的通知告知您创建已完成。 然后，单击&#x200B;**选择项目**。

![演示](./images/ex14.png)

接下来，转到屏幕顶部的搜索栏并键入&#x200B;**BigQuery**。 选择第一个结果。

![演示](./images/ex17.png)

本模块的目标是将Google Analytics数据导入Adobe Experience Platform。 要实现这一点，首先需要使用Google Analytics数据集中的虚拟数据。

单击“**+添加”**，然后在右菜单中单击“**公共数据集**”。

![演示](./images/ex118.png)

随后您将看到此窗口：

![演示](./images/ex119.png)

在搜索栏中输入搜索词&#x200B;**Google Analytics示例**，然后单击第一个搜索结果。

![演示](./images/ex120.png)

您将看到以下屏幕以及数据集的描述。 单击&#x200B;**查看数据集**。

![演示](./images/ex121.png)

然后，您将被重定向到BigQuery，在&#x200B;**资源管理器**&#x200B;下将看到此&#x200B;**bigquery-public-data**&#x200B;数据集。

![演示](./images/ex122a.png)

在&#x200B;**资源管理器**&#x200B;中，您现在应该会看到一些表。 欢迎您尽情探索。 转到`google_analytics_sample`。

![演示](./images/ex122.png)

单击以打开表`ga_sessions`。

![演示](./images/ex123.png)

在继续进行下一个练习之前，请在您计算机上的单独文本文件中写下以下内容：

| 凭据 | 命名 | 示例 |
| ----------------- |-------------| -------------|
| 项目名称 | `--aepUserLdap---googlecloud` | 旺格卢 — 古格吕德 |
| 项目编号 | random | possible-bee-447102-h3 |

通过单击顶部菜单栏中的&#x200B;**项目名称**，可以找到您的项目名称和项目ID：

![演示](./images/ex1projectMenu.png)

然后，您将在右侧看到项目ID：

![演示](./images/ex1projetcselection.png)

现在，您可以进入下一个练习，通过查询Google Analytics数据，您将弄脏自己的手。

## 后续步骤

转到[1.2.2在BigQuery](./ex2.md){target="_blank"}中创建您的第一个查询

返回至[使用BigQuery Google Analytics Connector在Adobe Experience Platform中摄取和分析Source数据](./customer-journey-analytics-bigquery-gcp.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
