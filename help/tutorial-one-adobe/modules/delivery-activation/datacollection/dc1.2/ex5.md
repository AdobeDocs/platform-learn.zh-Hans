---
title: 基础 — 数据摄取 — 从离线源摄取数据
description: 基础 — 数据摄取 — 从离线源摄取数据
kt: 5342
doc-type: tutorial
exl-id: 9fce6ece-f454-45de-9c95-35d604b3ae95
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 1.2.5数据登陆区

在本练习中，目标是使用Azure Blob Storage设置您的数据登陆区Source连接器。

数据登录区是由Adobe Experience Platform设置的Azure Blob存储界面，允许您访问安全、基于云的文件存储设施，以将文件导入Platform。 数据登陆区支持基于SAS的身份验证，其数据受标准Azure Blob存储安全机制的静态和中转保护。 基于SAS的身份验证允许您通过公共Internet连接安全地访问数据登陆区容器。

>[!NOTE]
>
> Adobe Experience Platform **对上传到Data Landing Zone容器的所有文件强制实施严格的七天生存时间(TTL)**。 所有文件都会在七天后删除。


## 先决条件

要将blob或文件复制到Adobe Experience Platform数据登陆区，您将使用命令行实用程序AzCopy 。 您可以通过[https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)下载操作系统的版本，在该页面上向下滚动到&#x200B;**下载AzCopy可移植二进制文件**&#x200B;并选择适合您的操作系统的版本。

![dlz-install-az-copy.png](./images/dlzinstallazcopy.png)

- 解压缩下载的文件

![dlz-install-az-copy.png](./images/dlz1.png)

- 下载包含示例网站交互的示例数据文件[global-context-websiteinteractions.csv](./../../../../assets/csv/data-ingestion/global-context-websiteinteractions.csv)，并将其保存到您解压缩&#x200B;**azcopy**&#x200B;的文件夹中。

![dlz-install-az-copy.png](./images/dlz2.png)

- 打开终端窗口并导航到桌面上的文件夹，您应会看到以下内容（azcopy和global-context-websiteinteractions.csv），例如OSX上的内容：

![dlz-unzip-azcopy.png](./images/dlzunzipazcopy.png)

## 1.2.5.2将数据登陆区连接到Adobe Experience Platform

通过转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。  选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](./images/sb1.png)

在左侧菜单中，转到&#x200B;**源**。 在源目录中，搜索&#x200B;**数据登录**。

![数据获取](./images/sourcesdlz.png)

单击&#x200B;**数据登陆区**&#x200B;卡，您将在右侧选项卡上看到凭据。

![dlz-view-credentials.png](./images/dlzviewcredentials.png)

单击指示的图标以复制&#x200B;**SASUri**。

![dlz-copy-sas-uri.png](./images/dlzcopysasuri.png)

## 将csv文件复制到AEP数据登陆区

现在，您将使用AZCopy通过Azure命令行工具将数据摄取到Adobe Experience Platform。

在azcopy安装位置打开终端并执行以下命令，将文件复制到AEP的数据登陆区域：

``./azcopy copy <your-local-file> <your SASUri>``

请务必用双引号将您的SASUri括起来。 将`<your-local-file>`替换为azcopy目录中的文件&#x200B;**global-context-websiteinteractions.csv**&#x200B;的本地副本的路径，并将`<your SASUri>`替换为您从Adobe Experience Platform UI复制的&#x200B;**SASUri**&#x200B;值。 您的命令应如下所示：

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

在终端中执行上述命令后，您会看到以下内容：

![dlz-exec-copy-command.png](./images/dlzexeccopycommand.png)

## 在数据登录区中查找文件

转到Adobe Experience Platform中的数据登陆区。

选择&#x200B;**源**，搜索&#x200B;**数据登录**，然后单击&#x200B;**设置**&#x200B;按钮。

![dlz-inspect-datalanding-zone.png](./images/dlzinspectdatalandingzone.png)

这将打开数据登陆区。 您将在数据登陆区域的&#x200B;**选择数据**&#x200B;面板中看到您刚刚上传的文件。

![dlz-datalanding-zone-open.png](./images/dlzdatalandingzoneopen.png)

## 处理您的文件

选择您的文件，然后选择&#x200B;**分隔符**&#x200B;作为数据格式。 然后，您将看到数据的预览。 单击&#x200B;**下一步**。

![dlz-datalanding-select-file.png](./images/dlzdatalandingselectfile.png)

您现在可以开始映射上传的数据以匹配数据集的XDM架构。

选择&#x200B;**现有数据集**，然后选择数据集&#x200B;**演示系统 — 网站(Global v1.1)**&#x200B;的事件数据集。 单击&#x200B;**下一步**。

![dlz-target-dataset.png](./images/dlztargetdataset.png)

现在，您可以将csv文件中的传入源数据映射到数据集XDM架构的目标字段。

![dlz-start-mapping.png](./images/dlzstartmapping.png)

>[!NOTE]
>
> 不要介意映射的潜在错误。 您将在下一步中更正映射。

## 映射字段

首先，单击&#x200B;**清除所有映射**&#x200B;按钮。 然后，您可以从干净映射开始。

![dlz-clear-mappings.png](./images/mappings1.png)

接下来，单击&#x200B;**新建字段类型**，然后选择&#x200B;**添加新字段**。

![dlz-clear-mappings.png](./images/dlzclearmappings.png)

要映射&#x200B;**ecid**&#x200B;源字段，请选择字段&#x200B;**identities.ecid**，然后单击&#x200B;**选择**。

![dlz-map-identity.png](./images/dlzmapidentity.png)

接下来，单击&#x200B;**映射目标字段**。

![dlz-map-select-target-field.png](./images/dlzmapselecttargetfield.png)

选择架构结构中的字段``--aepTenantId--``.identification.core.ecid。

![dlz-map-target-field.png](./images/dlzmaptargetfield.png)

您需要映射几个其他字段，请单击&#x200B;**+新建字段类型**，然后单击&#x200B;**添加新字段**&#x200B;并为此映射添加字段

| 源 | 目标 |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| 时间戳 | 时间戳 |
| 时间戳 | _id |

![dlz-add-other-mapping.png](./images/dlzaddothermapping.png)

完成后，屏幕应如下所示。 单击&#x200B;**下一步**。

![dlz-mapping-result.png](./images/dlzmappingresult.png)

单击&#x200B;**下一步**。

![dlz-default-scheduling.png](./images/dlzdefaultscheduling.png)

单击&#x200B;**完成**。

![dlz-import-finish.png](./images/dlzimportfinish.png)

## 监测数据流

要监视数据流，请转到&#x200B;**源**、**数据流**，然后单击您的数据流：

![dlz-monitor-dataflow.png](./images/dlzmonitordataflow.png)

加载数据可能需要几分钟的时间，如果加载成功，您将看到&#x200B;**成功**&#x200B;的状态：

![dlz-monitor-dataflow-result.png](./images/dlzmonitordataflowresult.png)

## 后续步骤

转到[摘要和优点](./summary.md){target="_blank"}

返回[数据摄取](./data-ingestion.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
