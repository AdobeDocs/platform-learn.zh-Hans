---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — Adobe Experience Platform中的XDM模式要求
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — Adobe Experience Platform中的XDM模式要求
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 1.7 Adobe Experience Platform中的XDM架构要求

为确保Web SDK和alloy.js能够将数据摄取到Adobe Experience Platform中，需要将特定XDM Mixin加入Adobe Experience Platform的XDM架构中。

转到 [https://experience.adobe.com/platform](https://experience.adobe.com/platform) 并登录。

![AEP Debugger](./images/exp1.png)

登录后，通过单击文本选择相应的沙盒 **生产产品** 的蓝线。 选择沙盒 `--aepSandboxId--`.

选择沙盒后，您将看到屏幕发生更改，现在您就位于沙盒中。

![AEP Debugger](./images/exp2.png)

在左侧菜单中，转到 **模式** 打开 **演示系统 — 网站的事件模式（全局v1.1）** 架构。

![AEP Debugger](./images/exp3.png)

在该架构上，您将看到字段组 **AEP Web SDK ExperienceEvent Mixin** 已添加。 此字段组将所有最低要求的字段添加到架构中。 Adobe Experience Platform中将由Web SDK使用的每个体验事件架构都将始终要求该字段组成为架构的一部分。

![AEP Debugger](./images/exp4.png)

在 [模块2](./../module2/data-ingestion.md) 您将了解如何将字段组添加到架构。

下一步： [摘要和优点](./summary.md)

[返回到模块1](./data-ingestion-launch-web-sdk.md)

[返回到所有模块](./../../overview.md)
