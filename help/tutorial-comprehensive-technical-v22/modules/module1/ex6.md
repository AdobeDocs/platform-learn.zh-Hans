---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Target
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Target
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6实施Adobe Target

## 1.6.更新数据流以使用Adobe Target

如果您要将通过Web SDK收集的数据发送到Adobe Target，并从Adobe Target获得针对每位客户的个性化体验的响应，请执行以下步骤。

转到 [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) 然后转到 **数据流**.

在屏幕的右上角，选择您的沙盒名称，该名称应为 `--aepSandboxId--`. 打开您的特定数据流(名为 `--demoProfileLdap-- - Demo System Datastream`.

![单击左侧导航中的“边缘配置”图标](./images/edgeconfig1b.png)

然后你会看到这个。 要启用Adobe Target，请单击 **+添加服务**.

![AEP Debugger](./images/aa2.png)

然后你会看到这个。 选择服务 **Adobe Target**，之后您可以选择提供其他信息。 此时，无需保存此内容，因此请单击 **取消**.

![AEP Debugger](./images/at1.png)

下一步： [1.7 Adobe Experience Platform中的XDM架构要求](./ex7.md)

[返回到模块1](./data-ingestion-launch-web-sdk.md)

[返回到所有模块](./../../overview.md)
