---
title: 基础 — Adobe Experience Platform数据收集和Web SDK扩展的设置 — Edge Network、数据流和服务器端数据收集
description: 基础 — Adobe Experience Platform数据收集和Web SDK扩展的设置 — Edge Network、数据流和服务器端数据收集
kt: 5342
doc-type: tutorial
exl-id: e97d40b5-616d-439c-9d6b-eaa4ebf5acb0
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 1.1.2Edge Network、数据流和服务器端数据收集

## 上下文

在本练习中，您将创建一个&#x200B;**数据流**。 **数据流**&#x200B;告知Adobe Edge服务器在Web SDK收集数据后将数据发送到何处。 例如，是否要将数据发送到Adobe Experience Platform？ Adobe Analytics？ Adobe Audience Manager？ Adobe Target？

数据流始终在Adobe Experience Platform数据收集用户界面中进行管理，并且对于通过Web SDK收集Adobe Experience Platform数据至关重要。 即使您使用非Adobe标签管理解决方案实施Web SDK，仍需要在Adobe Experience Platform数据收集用户界面中创建数据流。

在下一个练习中，您将在浏览器中实施Web SDK。 然后，您会更加清楚地了解正在收集的数据是什么样的。 目前，我们只是告诉数据流将数据转发到何处。

## 创建数据流

在[快速入门](./../../../modules/gettingstarted/gettingstarted/ex2.md)中，您已创建数据流，但我们未讨论该数据流的背景和原因。

Satastream会告知Adobe Edge服务器，在Web SDK收集数据后将发送到何处。 例如，是否要将数据发送到Adobe Experience Platform？ Adobe Analytics？ Adobe Audience Manager？ Adobe Target？ 数据流在Adobe Experience Platform数据收集用户界面中进行管理，并且对于使用Web SDK收集数据至关重要，无论您是否正在通过Adobe Experience Platform数据收集实施Web SDK。

让我们查看您的&#x200B;**[!UICONTROL 数据流]**：

转到[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)。

单击左侧菜单中的&#x200B;**[!UICONTROL 数据流]**。

![单击左侧导航中的“数据流”图标](./images/edgeconfig1.png)

打开名为`--aepUserLdap-- - Demo System Datastream`的数据流。

![命名数据流并保存](./images/edgeconfig2.png)

然后，您将看到数据流的详细信息。

![命名数据流并保存](./images/edgecfg1.png)

单击&#x200B;**Adobe Experience Platform**&#x200B;旁边的&#x200B;**...**，然后单击&#x200B;**编辑**。

![命名数据流并保存](./images/edgecfg1a.png)

你会看到这个。 目前，您仅启用了Adobe Experience Platform。 您的配置将类似于下面的配置。 (根据您的环境和Adobe Experience Platform实例，沙盒名称可能不同)

![命名数据流并保存](./images/edgecfg2.png)

您应像这样解释以下字段：

对于此数据流……

- 收集的所有数据都将存储在Adobe Experience Platform的`--aepSandboxName--`沙盒中
- 默认情况下，所有体验事件数据都会收集到数据集&#x200B;**演示系统 — 网站的事件数据集中(Global v1.1)**
- 默认情况下，所有配置文件数据都将收集到数据集&#x200B;**演示系统 — 网站的配置文件数据集(Global v1.1)**&#x200B;中（Web SDK当前尚不支持通过Web SDK本机摄取配置文件数据）
- 如果要对此数据流使用&#x200B;**Offer decisioning**&#x200B;应用程序服务，则需要选中用于Offer decisioning的框。 （这将是[模块3.3](./../../../modules/ajo-b2c/module3.3/offer-decisioning.md)的一部分）
- **默认启用Edge分段**，这意味着在摄取传入流量时，将在边缘评估符合条件的区段
- 如果要使用&#x200B;**Personalization目标**，您需要选中Personalization目标复选框。
- 
   - 如果要在此数据流中使用&#x200B;**Adobe Journey Optimizer**&#x200B;的功能，则需要选中Adobe Journey Optimizer的框。


目前，您的数据流不需要其他配置。

下一步： [1.1.3 Adobe Experience Platform数据收集简介](./ex3.md)

[返回模块1.1](./data-ingestion-launch-web-sdk.md)

[返回所有模块](./../../../overview.md)
