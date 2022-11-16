---
title: 区段激活到Microsoft Azure事件中心 — 在Adobe Experience Platform中设置事件中心RTCDP目标
description: 区段激活到Microsoft Azure事件中心 — 在Adobe Experience Platform中设置事件中心RTCDP目标
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b42b4ccb-1952-480b-b538-c1bd661e29eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 13.2在Adobe Experience Platform中配置Azure事件中心目标

## 13.2.1确定所需的Azure连接参数

要在Adobe Experience Platform中定义事件中心目标，您需要：

- 事件中心命名空间
- 事件中心
- Azure SAS密钥名称
- Azure SAS密钥

在上一个练习中定义了EventHub和EventHub命名空间： [练习1 — 在Azure中设置事件中心](./ex1.md)

### 事件中心命名空间

要在Azure Portal中查找上述信息，请导航至 [https://portal.azure.com/#home](https://portal.azure.com/#home). 确保使用正确的Azure帐户。

选择 **所有资源** 在Azure门户中：

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### 事件中心

查找资源类型的资源 **事件中心命名空间**，如果您遵循上一个练习中使用的命名约定，则事件中心命名空间将为 `--demoProfileLdap---aep-enablement`. 请注意，您将在下一个练习中需要它。

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

单击事件中心命名空间名称可获取详细信息：

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

选择 **事件中心** 要获取在事件中心命名空间中定义的事件中心列表，如果您遵循上一练习中使用的命名约定，将会找到一个名为 `--demoProfileLdap---aep-enablement-event-hub`. 请注意，您将在下一个练习中需要它。

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS密钥名称

选择 **共享访问策略** , **事件中心命名空间**

![2-05-select-sas.png](./images/2-05-select-sas.png)

您将看到共享访问策略的列表。 我们要查找的SAS密钥是 **RootManageSharedAccessKey**. 这是SAS密钥名称。 写下来。

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS密钥值

单击 **RootManageSharedAccessKey** 以获取SAS密钥值。 然后按 **复制到剪贴板** 图标以复制 **主键**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### 目标值摘要

此时，您应该已识别在Adobe Experience Platform实时CDP中定义Azure Event Hub目标所需的所有值。

| 目标属性名称 | 目标属性值 | 示例值 |
|---|---|---|
| sasKeyName | SAS密钥名称 | RootManageSharedAccessKey |
| sasKey | SAS密钥值 | srREx9ShJG1Rv7f/... |
| namespace | 事件中心命名空间 | `--demoProfileLdap---aep-enablement` |
| eventHubName | 事件中心 | `--demoProfileLdap---aep-enablement-event-hub` |

## 13.2.2在Adobe Experience Platform中创建Azure事件中心目标

通过转到以下URL登录Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的沙盒后，您将看到屏幕发生更改，现在您就位于专用沙盒中。

![数据获取](../module2/images/sb1.png)

转到 **目标**，然后转到 **目录**.

![数据获取](./images/sb2a.png)

选择 **云存储** 然后转到 **Azure事件中心** 单击 **设置** 或 **配置**:

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

填写您在上一个练习中收集的目标值。 接下来，单击 **连接到目标**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

如果您的凭据正确，您将看到确认消息： **已连接**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

现在，您需要以格式输入名称和描述 `--demoProfileLdap---aep-enablement`. 输入 **eventHubName** (请参阅上一个练习，其外观如下： `--demoProfileLdap---aep-enablement-event-hub`)并单击 **下一个**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

单击 **保存并退出**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

您的目标现已创建完成，可在Adobe Experience Platform中使用。

![2-12-destination-created.png](./images/2-12-destination-created.png)

下一步： [13.3创建区段](./ex3.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
