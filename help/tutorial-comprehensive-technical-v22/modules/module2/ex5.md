---
title: 基础 — 数据摄取 — 从离线源摄取数据
description: 基础 — 数据摄取 — 从离线源摄取数据
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 2.5数据登陆区

在本练习中，目标是使用Azure Blob Storage设置您的数据登陆区源连接器。

数据登陆区是由Adobe Experience Platform配置的Azure Blob存储界面，允许您访问安全的、基于云的文件存储工具，以将文件导入平台。 数据登陆区支持基于SAS的身份验证，其数据在静态和传输中均使用标准的Azure Blob存储安全机制进行保护。 基于SAS的身份验证允许您通过公共互联网连接安全地访问数据登陆区容器。

>[!NOTE]
>
> Adobe Experience Platform **强制实施严格的七天生存时间(TTL)** 上传到“数据登陆区”容器的所有文件。 七天后会删除所有文件。


## 2.5.1先决条件

要将Blob或文件复制到Adobe Experience Platform数据登陆区，您将使用命令行实用程序AzCopy。 您可以通过 [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- 解压缩下载的文件

![dlz-install-az-copy.png](./images/dlz1.png)

- 下载示例数据文件 [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv)，其中包含网站交互的示例，并将其保存到您解压缩的文件夹中 **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- 打开终端窗口并导航到桌面上的文件夹，您应会看到以下内容（azcopy和global-context-websiteinteractions.csv），例如在OSX上：

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2将数据登陆区连接到Adobe Experience Platform

通过转到以下URL登录Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--module2sandbox--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的沙盒后，您将看到屏幕发生更改，现在您就位于专用沙盒中。

![数据获取](./images/sb1.png)

在左侧菜单中，转到 **源**. 在源目录中，搜索 **数据登陆**. 在 **数据登陆区** 卡片，单击 **...** 选择 **查看凭据**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

单击顶部复制 **沙苏里**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 2.5.3将csv文件复制到AEP数据登陆区

现在，您将使用AZCopy的Azure命令行工具将数据摄取到Adobe Experience Platform中。

在azcopy安装位置打开终端，然后执行以下命令以将文件复制到AEP的数据登录区：

``./azcopy copy <your-local-file> <your SASUri>``

确保在SASUri周围加双引号。 替换 `<your-local-file>` 按文件本地副本的路径 **global-context-websiteinteractions.csv** 在azcopy目录中，并将 `<your SASUri>` 按 **沙苏里** 值。 您的命令应如下所示：

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

在终端中执行上述命令后，您将看到：

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4在数据登陆区查找文件

转到您的Adobe Experience Platform数据登陆区。

选择 **源**，搜索 **数据登陆** ，然后单击 **设置** 按钮。

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

这将打开数据登陆区。 您将看到您刚刚在数据登陆区 **选择数据** 的上界。

![dlz-datalanding-zone-open-png](./images/dlz-datalanding-zone-open.png)

## 2.5.5处理文件

选择文件，然后选择 **分隔** 格式。 然后，您将看到数据的预览。 单击&#x200B;**下一步**。

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

您现在可以开始映射已上传的数据，以匹配数据集的XDM架构。

选择 **现有数据集** 并选择数据集 **演示系统 — 网站事件数据集（全局v1.1）**. 单击&#x200B;**下一步**。

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

现在，您可以将来自csv文件的传入源数据映射到数据集XDM架构中的目标字段。

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> 不要介意映射存在潜在错误。 您将在下一步中更正映射。

## 2.5.6地图字段

首先，单击 **清除所有映射** 按钮。 然后，您可以从干净的映射开始。

![dlz-clear-mappings.png](./images/mappings1.png)

接下来，单击 **新字段类型** 然后选择 **添加新字段**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

映射 **ecid** 源字段，选择字段 **identities.ecid** 单击 **选择**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

接下来，单击 **映射目标字段**.

![dlz-map-select-target-field-png](./images/dlz-map-select-target-field.png)

选择字段 ``--aepTenantId--``架构结构中的.identification.core.ecid 。

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

您需要映射几个其他字段，请单击 **+新建字段类型** 后跟 **添加新字段** 并添加此映射的字段

| 来源 | Target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

完成后，您的屏幕应该如下所示。 单击&#x200B;**下一步**。

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

单击&#x200B;**下一步**。

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

单击&#x200B;**完成**。

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 2.5.7监控数据流

要监视数据流，请转到 **源**, **数据流** 并单击您的数据流：

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

加载数据可能需要几分钟时间，如果成功，您将看到 **成功**:

![dlz-monitor-dataflow-result-png](./images/dlz-monitor-dataflow-result.png)

下一步： [摘要和优点](./summary.md)

[返回到模块2](./data-ingestion.md)

[返回到所有模块](../../overview.md)
