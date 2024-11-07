---
title: 快速入门 — 创建数据流
description: 快速入门 — 创建数据流
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 0.3创建数据流

转到[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。 在上一个练习之后，您现在拥有两个数据收集属性：一个用于Web，一个用于移动设备。

![DSN](./images/launchprop.png)

这些属性几乎已准备就绪，可以使用，但在使用这些属性开始收集数据之前，您需要设置数据流。 您将了解有关什么是数据流以及它在练习1.2中的含义的更多信息。

目前，请按照以下步骤操作。

## 0.3.1为Web创建数据流

单击&#x200B;**[!UICONTROL 数据流]**&#x200B;或&#x200B;**[!UICONTROL 数据流(Beta)]**。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1a.png)

在屏幕右上角，选择沙盒名称，应为`--aepSandboxName--`。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1b.png)

单击&#x200B;**[!UICONTROL 新建数据流]**。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1.png)

对于&#x200B;**[!UICONTROL 友好名称]**&#x200B;和可选描述，请输入`--aepUserLdap-- - Demo System Datastream`。 对于事件架构，请选择&#x200B;**演示系统 — 网站的事件架构(Global v1.1)**。 单击&#x200B;**保存**。

![命名Edge配置并保存](./images/edgeconfig2.png)

你会看到这个。 单击&#x200B;**添加服务**。

![命名Edge配置并保存](./images/edgeconfig3.png)

选择将公开其他字段的服务&#x200B;**[!UICONTROL Adobe Experience Platform]**。 你会看到这个。

对于事件数据集，请选择&#x200B;**Demo System - Event Dataset for Website (Global v1.1)**；对于配置文件数据集，请选择&#x200B;**Demo System - Profile Dataset for Website (Global v1.1)**。 单击&#x200B;**保存**。

![命名Edge配置并保存](./images/edgeconfig4.png)

您现在将看到此内容。

![命名Edge配置并保存](./images/edgeconfig5.png)

就目前而言，就这样了。 在[模块1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)中，您将了解有关Web SDK以及如何配置其所有功能的更多信息。

在左侧菜单中，单击&#x200B;**[!UICONTROL 标记]**。

筛选搜索结果以查看您的两个数据收集属性。 通过单击&#x200B;**Web**&#x200B;的属性将其打开。

![命名Edge配置并保存](./images/edgeconfig10a.png)

你会看到这个。 单击&#x200B;**扩展**。

![命名Edge配置并保存](./images/edgeconfig11.png)

在Adobe Experience Platform Web SDK扩展中，单击&#x200B;**配置**。

![命名Edge配置并保存](./images/edgeconfig12.png)

你会看到这个。 对于&#x200B;**数据流**，您当前将看到一个虚拟值设置为1。 您现在需要单击&#x200B;**从列表中选择**&#x200B;单选按钮。 在下拉列表中，选择您之前创建的数据流。

![命名Edge配置并保存](./images/edgeconfig13.png)

确保已选择您的&#x200B;**数据流**。 提示：您可以通过键入`--aepUserLdap--`来轻松筛选下拉列表中的结果。

![命名Edge配置并保存](./images/edgeconfig14.png)

向下滚动，直到看到&#x200B;**数据收集**。 请确保未启用&#x200B;**启用点击数据收集**&#x200B;的复选框。 单击&#x200B;**保存**&#x200B;以保存更改。

![命名Edge配置并保存](./images/edgeconfig14a.png)

转到&#x200B;**发布流**。

![命名Edge配置并保存](./images/edgeconfig15.png)

单击&#x200B;**主要**&#x200B;的&#x200B;**...**，然后单击&#x200B;**编辑**。

![命名Edge配置并保存](./images/edgeconfig16.png)

单击&#x200B;**添加所有更改的资源**，然后单击&#x200B;**保存并生成以进行开发**。

![命名Edge配置并保存](./images/edgeconfig17.png)

您的更改现已发布，将在几分钟后准备就绪。

## 0.3.2为移动设备创建数据流

转到[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。

单击&#x200B;**[!UICONTROL 数据流]**&#x200B;或&#x200B;**[!UICONTROL 数据流(Beta)]**。

![单击左侧导航中的“数据流”图标](./images/edgeconfig1a.png)

在屏幕右上角，选择沙盒名称，应为`--aepSandboxName--`。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1b.png)

单击&#x200B;**[!UICONTROL 新建数据流]**。

![单击左侧导航中的“数据流”图标](./images/edgeconfig1.png)

对于&#x200B;**[!UICONTROL 友好名称]**&#x200B;和可选描述，请输入`--aepUserLdap-- - Demo System Datastream (Mobile)`。 对于事件架构，请选择&#x200B;**演示系统 — 移动应用程序的事件架构(Global v1.1)**。 单击&#x200B;**保存**。

单击&#x200B;**[!UICONTROL 保存]**。

![命名数据流并保存](./images/edgeconfig2m.png)

你会看到这个。 单击&#x200B;**添加服务**。

![命名数据流并保存](./images/edgeconfig3m.png)

选择将公开其他字段的服务&#x200B;**[!UICONTROL Adobe Experience Platform]**。 你会看到这个。

对于事件数据集，请选择&#x200B;**演示系统 — 移动设备应用程序的事件数据集(Global v1.1)**；对于配置文件数据集，请选择&#x200B;**演示系统 — 移动设备应用程序的配置文件数据集(Global v1.1)**。 单击&#x200B;**保存**。

![命名数据流配置并保存](./images/edgeconfig4m.png)

你会看到这个。

![命名数据流配置并保存](./images/edgeconfig5m.png)

您的数据流现已准备就绪，可用于移动设备的Adobe Experience Platform数据收集客户端资产。

转到&#x200B;**标记**&#x200B;并筛选搜索结果以查看您的两个数据收集属性。 通过单击&#x200B;**移动设备**&#x200B;的属性将其打开。

![命名Edge配置并保存](./images/edgeconfig10am.png)

你会看到这个。 单击&#x200B;**扩展**。

![命名Edge配置并保存](./images/edgeconfig11m.png)

在&#x200B;**Adobe Experience PlatformEdge Network**&#x200B;扩展上，单击&#x200B;**配置**。

![命名Edge配置并保存](./images/edgeconfig12m.png)

你会看到这个。 现在，您需要选择刚刚配置的正确沙盒和数据流。 要使用的沙盒是`--aepSandboxName--`，数据流名为`--aepUserLdap-- - Demo System Datastream (Mobile)`。

对于&#x200B;**Edge Network域**，请使用默认域&#x200B;**edge.adobedc.net**。

单击&#x200B;**保存**&#x200B;以保存更改。

![命名Edge配置并保存](./images/edgeconfig13m.png)

转到&#x200B;**发布流**。

![命名Edge配置并保存](./images/edgeconfig15m.png)

单击&#x200B;**Main**&#x200B;旁边的&#x200B;**...**，然后单击&#x200B;**编辑**。

![命名Edge配置并保存](./images/edgeconfig16m.png)

单击&#x200B;**添加所有更改的资源**，然后单击&#x200B;**保存并生成以进行开发**。

![命名Edge配置并保存](./images/edgeconfig17m.png)

您的更改现已发布，将在几分钟后准备就绪。

下一步： [0.4使用网站](./ex4.md)

[返回模块0](./getting-started.md)

[返回所有模块](./../../../overview.md)