---
title: 区段激活到Microsoft Azure事件中心 — 在Adobe Experience Platform中设置事件中心RTCDP目标
description: 区段激活到Microsoft Azure事件中心 — 在Adobe Experience Platform中设置事件中心RTCDP目标
kt: 5342
doc-type: tutorial
exl-id: 0c2e94ec-00e8-4f47-add7-ca3a08151225
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 2.4.2在Adobe Experience Platform中配置Azure事件中心目标

## 2.4.2.1标识所需的Azure连接参数

要在Adobe Experience Platform中定义事件中心目标，您需要执行以下操作：

- 事件中心命名空间
- 事件中心
- Azure SAS密钥名称
- Azure SAS密钥

在上一个练习中已定义事件中心和EventHub命名空间： [练习1 - Azure中的设置事件中心](./ex1.md)

### 事件中心命名空间

要在Azure Portal中查找上述信息，请导航到[https://portal.azure.com/#home](https://portal.azure.com/#home)。 确保使用正确的Azure帐户。

选择Azure Portal中的&#x200B;**所有资源**：

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### 事件中心

查找资源类型为&#x200B;**事件中心命名空间**&#x200B;的资源，如果您遵循上一个练习中使用的命名约定，则事件中心命名空间将为`--aepUserLdap---aep-enablement`。 记下它，您将在下一个练习中需要它。

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

单击事件中心命名空间名称以获取详细信息：

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

选择&#x200B;**事件中心**&#x200B;以获取在事件中心命名空间中定义的事件中心列表，如果遵循上个练习中使用的命名约定，您将找到名为`--aepUserLdap---aep-enablement-event-hub`的事件中心。 记下它，您将在下一个练习中需要它。

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS密钥名称

为您的&#x200B;**事件中心命名空间**&#x200B;选择&#x200B;**共享访问策略**

![2-05-select-sas.png](./images/2-05-select-sas.png)

您将看到共享访问策略的列表。 我们正在查找的SAS密钥是&#x200B;**RootManageSharedAccessKey**。 这是SAS密钥名称。 写下来。

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS密钥值

单击&#x200B;**RootManageSharedAccessKey**&#x200B;以获取SAS密钥值。 按&#x200B;**复制到剪贴板**&#x200B;图标复制&#x200B;**主键**：

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### 目标值摘要

此时，您应该已经确定了在Adobe Experience Platform Real-time CDP中定义Azure事件中心目标所需的所有值。

| 目标属性名称 | 目标属性值 | 示例值 |
|---|---|---|
| sasKeyName | SAS密钥名称 | RootManageSharedAccessKey |
| sasKey | SAS密钥值 | srREx9ShJG1Rv7f/... |
| 命名空间 | 事件中心命名空间 | `--aepUserLdap---aep-enablement` |
| eventHubName | 事件中心 | `--aepUserLdap---aep-enablement-event-hub` |

## 2.4.2.2在Adobe Experience Platform中创建Azure事件中心目标

通过转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../modules/datacollection/module1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](./../../../modules/datacollection/module1.2/images/sb1.png)

转到&#x200B;**目标**，然后转到&#x200B;**目录**。

![数据获取](./images/sb2a.png)

选择&#x200B;**云存储**&#x200B;并转到&#x200B;**Azure事件中心**&#x200B;并单击&#x200B;**设置**&#x200B;或&#x200B;**配置**：

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

填写您在上一个练习中收集的目标值。 接下来，单击&#x200B;**连接到目标**。

![2-09-destination-values.png](./images/2-09-destination-values.png)

如果凭据正确，您将看到确认：**已连接**。

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

您现在需要以`--aepUserLdap---aep-enablement`格式输入名称和描述。 输入&#x200B;**eventHubName**（参阅上一个练习，它看起来像这样： `--aepUserLdap---aep-enablement-event-hub`），然后单击&#x200B;**下一步**。

![2-10-create-destination.png](./images/2-10-create-destination.png)

单击&#x200B;**保存并退出**。

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

您的目标现已创建并可在Adobe Experience Platform中使用。

![2-12-destination-created.png](./images/2-12-destination-created.png)

下一步： [2.4.3创建区段](./ex3.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
