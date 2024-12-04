---
title: 查询服务 — 先决条件
description: 查询服务 — 先决条件
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1先决条件

## 安装PSQL命令行实用程序

按照Adobe Experience Platform文档中概述的说明安装psql客户端：
[PSQL安装指南](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html)

安装PSQL后，可能需要通过在终端窗口中运行以下命令来更新&#x200B;**PATH**：

对于macOS（将以下命令中的XX替换为您安装的PSQL的版本号）：

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## 安装Power BI

仅适用于Windows用户

[安装MicrosoftPower BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html)

请确保安装文档中所述的&#x200B;**npgsql**&#x200B;的精确版本，否则您将无法将Power BI连接到Adobe Experience Platform查询服务。

## 安装表格

对于Windows或Mac用户

根据文档[安装Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html)。

Tableau自动为您提供14天的试用期。

如果您想要在这14天之后使用Tableau，则需要许可证密钥。

下一步： [5.1.2快速入门](./ex2.md)

[返回模块5.1](./query-service.md)

[返回所有模块](../../../overview.md)
