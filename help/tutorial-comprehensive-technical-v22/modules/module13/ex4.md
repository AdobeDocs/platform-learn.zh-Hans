---
title: 区段激活到Microsoft Azure事件中心 — 激活区段
description: 区段激活到Microsoft Azure事件中心 — 激活区段
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# 13.4激活区段

## 13.4.1将区段添加到Azure事件中心目标

在本练习中，您将添加区段 `--demoProfileLdap-- - Interest in Equipment` 至 `--demoProfileLdap---aep-enablement` Azure事件中心目标。

通过转到以下URL登录Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的沙盒后，您将看到屏幕发生更改，现在您就位于专用沙盒中。

![数据获取](../module2/images/sb1.png)

转到 **目标**，然后单击 **浏览**. 然后，您将看到所有可用的目标。 找到您的目标，然后单击 **+** 图标（如下所示）。

![5-01-select-destination.png](./images/5-01-select-destination.png)

然后你会看到这个。 使用LDAP搜索区段，然后选择 `--demoProfileLdap-- - Interest in Equipment` 从区段列表。

单击&#x200B;**下一步**。

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP可以向两种类型的目标（区段目标和配置文件目标）提供有效负载。

区段目标将收到预定义的区段资格有效负载，稍后将讨论该负载。 此类负载包含 **全部** 特定用户档案的区段资格。 即使不在目标激活列表中的区段也是如此。 此类区段目标的示例包括 **Azure事件中心** 和 **AWSKinesis**.

通过基于配置文件的目标，您可以从XDM配置文件合并架构中选择任何属性(firstName、lastName、...)，并将其包含在激活有效负载中。 例如， **电子邮件营销**.

因为您的Azure事件中心目标是 **区段** 目标，例如选择字段 `--aepTenantId--.identification.core.ecid`.

单击 **添加新字段**，单击浏览模式并选择字段 `--aepTenantId--identification.core.ecid` （删除自动显示的任何其他字段）。

单击&#x200B;**下一步**。

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

单击&#x200B;**完成**。

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

您的区段现在已激活到Microsoft事件中心目标。

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

下一步： [13.5创建Microsoft Azure项目](./ex5.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
