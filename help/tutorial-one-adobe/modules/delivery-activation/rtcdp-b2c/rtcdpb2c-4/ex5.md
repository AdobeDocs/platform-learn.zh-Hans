---
title: Audience Activation到Microsoft Azure事件中心 — 激活受众
description: Audience Activation到Microsoft Azure事件中心 — 激活受众
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---

# 2.4.5激活受众

## 将受众添加到Azure事件中心目标

在本练习中，您要将受众`--aepUserLdap-- - Interest in Plans`添加到`--aepUserLdap---aep-enablement` Azure事件中心目标。

通过转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

转到&#x200B;**目标**，然后单击&#x200B;**浏览**。 然后，您将看到所有可用的目标。 找到您的目标并单击下面所示的3个圆点**...**，然后单击&#x200B;**激活受众**。

![5-01-select-destination.png](./images/501selectdestination.png)

你会看到这个。 使用ldap搜索受众，并从受众列表中选择`--aepUserLdap-- - Interest in Plans`。

单击&#x200B;**下一步**。

![5-04-select-segment.png](./images/504selectsegment.png)

单击&#x200B;**添加新字段**，单击浏览架构并选择字段`--aepTenantId--identification.core.ecid`（删除将自动显示的任何其他字段）。

单击&#x200B;**下一步**。

![5-05-select-attributes.png](./images/505selectattributes.png)

单击&#x200B;**完成**。

![5-06-destination-finish.png](./images/506destinationfinish.png)

现在，您的受众将会朝着您的Microsoft事件中心目标激活。

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

## 后续步骤

转到[2.4.6创建您的Microsoft Azure项目](./ex6.md){target="_blank"}

返回至[Real-Time CDP：Audience Activation至Microsoft Azure事件中心](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
