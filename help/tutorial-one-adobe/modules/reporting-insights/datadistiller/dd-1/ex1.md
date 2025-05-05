---
title: 查询服务 — 先决条件
description: 查询服务 — 先决条件
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 2.1.1先决条件

## 安装PSQL命令行实用程序

按照Adobe Experience Platform文档中概述的说明安装psql客户端：
[PSQL安装指南](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=zh-Hans)

安装PSQL后，可能需要通过在终端窗口中运行以下命令来更新&#x200B;**PATH**：

对于macOS（将以下命令中的XX替换为您安装的PSQL的版本号）：

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## 安装Power BI

仅适用于Windows用户

[安装Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=zh-Hans)

请确保安装文档中所述的&#x200B;**npgsql**&#x200B;的确切版本，否则无法将Power BI连接到Adobe Experience Platform查询服务。

## 安装表格

对于Windows或Mac用户

根据文档[安装Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=zh-Hans)。

Tableau自动为您提供14天的试用期。

如果您想要在这14天之后使用Tableau，则需要许可证密钥。

## 后续步骤

转到[2.1.2快速入门](./ex2.md){target="_blank"}

返回[查询服务](./query-service.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
