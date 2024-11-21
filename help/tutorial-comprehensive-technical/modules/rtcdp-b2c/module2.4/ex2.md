---
title: 区段激活到Microsoft Azure事件中心 — Azure中的设置事件中心
description: 区段激活到Microsoft Azure事件中心 — Azure中的设置事件中心
kt: 5342
doc-type: tutorial
exl-id: 0c2e94ec-00e8-4f47-add7-ca3a08151225
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---

# 2.4.2配置Microsoft Azure EventHub环境

Azure事件中心是一种高度可扩展的发布 — 订阅服务，每秒可以摄取数百万个事件并将它们流式传输到多个应用程序中。 这使您能够处理和分析由连接的设备和应用程序产生的大量数据。

## 什么是Azure事件中心？

Azure事件中心是一个大数据流式传输平台和事件摄取服务。 它每秒可以接收和处理数百万个事件。 发送到事件中心的数据可以使用任何实时分析提供程序或批处理/存储适配器进行转换和存储。

事件中心代表事件管道的&#x200B;**前门**，在解决方案体系结构中通常称为事件引入器。 事件摄取器是位于事件发布者(如Adobe Experience Platform RTCDP)和事件使用者之间的组件或服务，用于将事件流的生产与事件的消费分离。 事件中心提供了一个具有时间保留缓冲的统一流平台，将事件生成器与事件使用者分离。

## 创建事件中心命名空间

转到[https://portal.azure.com/#home](https://portal.azure.com/#home)并选择&#x200B;**创建资源**。

![1-01-open-azure-portal.png](./images/101openazureportal.png)

在资源屏幕中，在搜索栏中输入&#x200B;**事件**。 找到&#x200B;**事件中心**&#x200B;卡，单击&#x200B;**创建**，然后单击&#x200B;**事件中心**。

![1-02-search-event-hubs.png](./images/102searcheventhubs.png)

如果这是您第一次在Azure中创建资源，则需要创建新的&#x200B;**资源组**。 如果您已经有一个资源组，则可以选择该资源组（或创建一个新资源组）。

单击&#x200B;**新建**&#x200B;并将您的群组命名为`--aepUserLdap---aep-enablement`，单击&#x200B;**确定**。

![1-04-create-resource-group.png](./images/104createresourcegroup.png)

按照指示填写其余字段：

- 命名空间：定义您的命名空间，命名空间必须是唯一的，请使用以下模式`--aepUserLdap---aep-enablement`
- 位置：选择任意位置
- 定价层： **基本**
- 吞吐量单位： **1**

单击&#x200B;**审阅+创建**。

![1-05-create-namespace.png](./images/105createnamespace.png)

单击&#x200B;**创建**。

![1-07-namespace-create.png](./images/107namespacecreate.png)

资源组的部署可能需要1-2分钟，如果部署成功，您将看到以下屏幕：

![1-08-namespace-deploy.png](./images/108namespacedeploy.png)

## 在Azure中设置事件中心

转到[https://portal.azure.com/#home](https://portal.azure.com/#home)并选择&#x200B;**所有资源**。

![1-09-all-resources.png](./images/109allresources.png)

从资源列表中，单击您的`--aepUserLdap---aep-enablement`事件中心命名空间：

![1-10-list-resources.png](./images/110listresources.png)

在`--aepUserLdap---aep-enablement`详细信息屏幕中，转到&#x200B;**实体**&#x200B;并单击&#x200B;**事件中心**：

![1-11-eventhub-namespace.png](./images/111eventhubnamespace.png)

单击&#x200B;**+事件中心**。

![1-12-add-event-hub.png](./images/112addeventhub.png)

使用`--aepUserLdap---aep-enablement-event-hub`作为名称，然后单击&#x200B;**审阅+创建**。

![1-13-create-event-hub.png](./images/113createeventhub.png)

单击&#x200B;**创建**。

![1-13-create-event-hub.png](./images/113createeventhub1.png)

在事件中心命名空间下的&#x200B;**事件中心**&#x200B;中，您现在将看到&#x200B;**事件中心**&#x200B;已列出。

![1-14-event-hub-list.png](./images/114eventhublist.png)

## 设置您的Azure存储帐户

要在以后的练习中调试您的Azure事件中心函数，您需要在Visual Studio代码项目设置中提供Azure存储帐户。 您现在将创建该Azure存储帐户。

转到[https://portal.azure.com/#home](https://portal.azure.com/#home)并选择&#x200B;**创建资源**。

![1-15-event-hub-storage.png](./images/115eventhubstorage.png)

在搜索中输入&#x200B;**存储帐户**，找到&#x200B;**存储帐户**&#x200B;的卡，然后单击&#x200B;**存储帐户**。

![1-16-event-hub-search-storage.png](./images/116eventhubsearchstorage.png)

指定您的&#x200B;**资源组**（在本练习开始时创建），使用`--aepUserLdap--aepstorage`作为存储帐户名称并选择&#x200B;**本地冗余存储(LRS)**，然后单击&#x200B;**查看+创建**。

![1-18-event-hub-create-review-storage.png](./images/118eventhubcreatereviewstorage.png)

单击&#x200B;**创建**。

![1-19-event-hub-submit-storage.png](./images/119eventhubsubmitstorage.png)

创建存储帐户将需要几秒钟的时间：

![1-20-event-hub-deploy-storage.png](./images/120eventhubdeploystorage.png)

完成后，屏幕将显示&#x200B;**转到资源**&#x200B;按钮。

单击&#x200B;**主页**。

![1-21-event-hub-deploy-ready-storage.png](./images/121eventhubdeployreadystorage.png)

您的存储帐户现在显示在&#x200B;**最近的资源**&#x200B;下。

![1-22-event-hub-deploy-resources-list.png](./images/122eventhubdeployresourceslist.png)

下一步： [2.4.3在Adobe Experience Platform中配置Azure事件中心目标](./ex3.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
