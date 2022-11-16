---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 边缘网络、数据流和服务器端数据收集
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 边缘网络、数据流和服务器端数据收集
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6f7c540f-3804-483d-90f9-b26b4a252b8b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---

# 1.2边缘网络、数据流和服务器端数据收集

## 上下文

在本练习中，您将创建 **数据流**. A **数据流** 告知Adobe Edge服务器在Web SDK收集数据后将数据发送到何处。 例如，您要将数据发送到Adobe Experience Platform吗？ Adobe Analytics? Adobe Audience Manager? Adobe Target?

数据流始终在Adobe Experience Platform数据收集用户界面中进行管理，并且对于使用Web SDK进行Adobe Experience Platform数据收集至关重要。 即使您使用非Adobe标签管理解决方案实施Web SDK，您仍需要在Adobe Experience Platform数据收集用户界面中创建数据流。

在下一个练习中，您将在浏览器上实施Web SDK。 然后，您会更加清楚地了解正在收集的数据是什么样的。 目前，我们只是告诉数据流在何处转发数据。

## 创建数据流

在 [练习0.2](./../module0/ex2.md) 您已经创建了数据流，但我们没有讨论数据流的背景和原因。

数据流告知Adobe Edge服务器在Web SDK收集数据后将其发送到何处。 例如，您要将数据发送到Adobe Experience Platform吗？ Adobe Analytics? Adobe Audience Manager? Adobe Target? 数据流在Adobe Experience Platform数据收集用户界面中进行管理，对于使用Web SDK进行平台数据收集至关重要，无论您是否通过Adobe Experience Platform数据收集来实施Web SDK。

让我们回顾一下 **[!UICONTROL 数据流]**:

转到 [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

单击 **[!UICONTROL 数据流]** 或 **[!UICONTROL 数据流（测试版）]** 中。

![单击左侧导航中的数据流图标](./images/edgeconfig1.png)

搜索您的数据流，该数据流名为 `--demoProfileLdap-- - Demo System Datastream`.

![命名数据流并保存](./images/edgeconfig2.png)

然后，您将看到数据流的详细信息。

![命名数据流并保存](./images/edgecfg1.png)

单击 **...** 下一页 **Adobe Experience Platform** 单击 **编辑**.

![命名数据流并保存](./images/edgecfg1a.png)

然后你会看到这个。 目前，您只启用了Adobe Experience Platform。 您的配置将类似于以下配置。 (根据您的环境和Adobe Experience Platform实例，沙盒名称可能不同)

![命名数据流并保存](./images/edgecfg2.png)

您应将以下字段解释为：

对于此数据流……

- 收集的所有数据都将存储在 `--aepSandboxId--` Adobe Experience Platform中的沙盒
- 默认情况下，所有体验事件数据都会收集到数据集中 **演示系统 — 网站事件数据集（全局v1.1）**
- 默认情况下，所有配置文件数据都将收集到数据集中 **演示系统 — 网站的配置文件数据集（全局v1.1）** （Web SDK当前尚不支持在本地使用Web SDK摄取配置文件数据，该数据将在稍后阶段提供）
- 如果您想使用 **offer decisioning** 应用程序服务时，需要选中Offer decisioning框。 (这将是 [模块9](./../module9/offer-decisioning.md))
- 如果您想使用 **边缘分割**，则需要选中“边缘分段”复选框。
- 如果您想使用 **个性化目标**，则需要选中个性化目标复选框。

目前，您的数据流不需要其他配置。

下一步： [1.3Adobe Experience Platform数据收集简介](./ex3.md)

[返回到模块1](./data-ingestion-launch-web-sdk.md)

[返回到所有模块](./../../overview.md)
