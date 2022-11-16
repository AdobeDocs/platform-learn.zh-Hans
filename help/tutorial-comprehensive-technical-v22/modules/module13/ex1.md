---
title: 区段激活到Microsoft Azure事件中心 — 在Azure中设置事件中心
description: 区段激活到Microsoft Azure事件中心 — 在Azure中设置事件中心
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 9434ac83-5554-48bf-838c-7346d571efbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# 13.1配置Microsoft Azure EventHub环境

Azure事件中心是一项高度可伸缩的发布订阅服务，每秒可摄取数百万个事件并将其流入多个应用程序。 这样，您就可以处理和分析连接的设备和应用程序所产生的大量数据。

## 13.1.1什么是Azure事件中心？

Azure事件中心是大数据流平台和事件摄取服务。 它每秒可以接收和处理数百万个事件。 通过使用任何实时分析提供程序或批量处理/存储适配器，可以转换和存储发送到事件中心的数据。

事件中心表示 **前门** 对于事件管道，在解决方案架构中通常称为事件引入器。 事件引入器是位于事件发布者(如Adobe Experience Platform RTCDP)和事件使用者之间的组件或服务，用于将事件流的生成与这些事件的使用情况脱钩。 事件中心提供具有时间保留缓冲的统一流平台，将事件生成者与事件消费者脱钩。

## 13.1.2创建事件中心命名空间

转到 [https://portal.azure.com/#home](https://portal.azure.com/#home) 选择 **创建资源**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

在资源屏幕中，输入 **事件** ，然后选择 **事件中心** 从下拉菜单中：

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

单击 **创建**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

如果这是您首次在Azure中创建资源，则需要创建新 **资源组**. 如果您已经有资源组，则可以选择该资源组（或创建一个新资源组）。

选择 **新建**，命名您的组 `--demoProfileLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

完成对字段的测试，如下所示：

- 命名空间：定义命名空间，它必须是唯一的，请使用以下模式 `--demoProfileLdap---aep-enablement`
- 位置： **西欧** 指阿姆斯特丹的Azure数据中心
- 定价层： **基本**
- 吞吐量单位： **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

单击 **查看+创建**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

单击&#x200B;**创建**。

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

部署资源组可能需要1-2分钟，成功后，您将看到以下屏幕：

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 13.1.3在Azure中设置事件中心

转到 [https://portal.azure.com/#home](https://portal.azure.com/#home) 选择 **所有资源**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

从资源列表中，选择 `--demoProfileLdap---aep-enablement` 命名空间：

![1-10-list-resources.png](./images/1-10-list-resources.png)

在 `--demoProfileLdap---aep-enablement` 详细信息屏幕，选择 **事件中心**:

![1-11-eventhub-namespace.png](./images/1-11-eventhub-namespace.png)

单击 **+事件中心**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

使用 `--demoProfileLdap---aep-enablement-event-hub` 作为名称，然后单击 **创建**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

单击 **事件中心** 在事件中心命名空间中。 现在，您应会看到 **事件中心** 列出。 如果是这种情况，您可以继续下一个练习。

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 13.1.4设置您的Azure存储帐户

要在以后的练习中调试Azure事件中心功能，您需要在Visual Studio代码项目设置中提供Azure存储帐户。 您现在将创建该Azure存储帐户。

转到 [https://portal.azure.com/#home](https://portal.azure.com/#home) 选择 **创建资源**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

输入 **存储** 搜索并选择 **存储帐户** 列表。

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

选择&#x200B;**创建**。

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

指定 **资源组** （在本练习的开头创建），使用 `--demoProfileLdap--aepstorage` 作为您的存储帐户名称，然后选择 **本地冗余存储(LRS)**，然后单击 **查看+创建**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

单击&#x200B;**创建**。

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

创建存储帐户需要几秒钟：

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

完成后，屏幕将显示 **转到资源** 按钮。

单击 **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

您的存储帐户现在在 **近期资源**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

下一步： [13.2在Adobe Experience Platform中配置Azure事件中心目标](./ex2.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
