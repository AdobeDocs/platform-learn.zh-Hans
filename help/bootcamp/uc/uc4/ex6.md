---
title: Bootcamp -Customer Journey Analytics — 从洞察到行动
description: Bootcamp -Customer Journey Analytics — 从洞察到行动
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 4.6从洞察到行动

## 目标

- 了解如何基于Customer Journey Analytics中收集的视图构建受众
- 在Real-Time CDP和Adobe Journey Optimizer中使用此受众

## 4.6.1创建受众并将其发布

在您的项目中，您创建了一个名为&#x200B;**呼叫感觉**&#x200B;的过滤器，并且能够查看被分类为&#x200B;**正面**&#x200B;的呼叫中心用户数量。 现在，您将能够与这些用户创建区段，并在历程或通信渠道中激活他们。

第一步是：在上一个练习创建的面板中，选择行&#x200B;**1。 电话感受 — 积极**，右键单击并选择&#x200B;**从所选内容创建受众**&#x200B;选项：

![演示](./images/aud1.png)

接下来，按照模型&#x200B;**yourLastName - CJA受众呼叫感觉良好**&#x200B;为您的受众提供一个名称：

![演示](./images/aud2.png)

请注意，可以预览正在创建的受众：

![演示](./images/aud3.png)

最后，单击&#x200B;**Publish**。

![演示](./images/aud4.png)

## 4.6.2将受众用作区段的一部分

返回Adobe Experience Platform，转到&#x200B;**区段>浏览**，您将能够看到在CJA中创建的区段已准备就绪，可用于您的激活和历程！

![演示](./images/aud5.png)

现在，让我们在Facebook激活和客户历程中使用此区段！

## 4.6.3实时使用您在Real-Time CDP中的区段

在Adobe Experience Platform中，转到&#x200B;**区段>浏览**，然后查找您在CJA中创建的受众：

![演示](./images/aud6.png)

单击您的区段，然后单击&#x200B;**激活到目标**：

![演示](./images/aud7.png)

选择名为&#x200B;**bootcamp-facebook**&#x200B;的目标，然后单击&#x200B;**下一步**。

![演示](./images/aud8.png)

再次单击&#x200B;**下一步**。

![演示](./images/aud9.png)

选择&#x200B;**受众来源**&#x200B;选项，并将其设置为&#x200B;**直接从客户处设置**，单击&#x200B;**下一步**。

![演示](./images/aud10.png)

单击&#x200B;**完成**。

![演示](./images/aud11.png)

现在，您的区段已连接到Facebook的自定义受众。 现在，让我们在Adobe Journey Optimizer中使用同一区段。

## 4.6.4在Adobe Journey Optimizer中使用您的区段

在Adobe Experience Platform中，单击&#x200B;**Journey Optimizer**，然后在左侧菜单中单击&#x200B;**历程**，然后单击&#x200B;**创建历程**&#x200B;开始创建旅程。

![演示](./images/aud20.png)

![演示](./images/aud21.png)

![演示](./images/aud22.png)

然后，在左侧菜单的&#x200B;**事件**&#x200B;下，选择&#x200B;**区段鉴别**，并将其拖动到历程：

![演示](./images/aud23.png)

在“区段”下，单击&#x200B;**编辑**&#x200B;以选择一个区段：

![演示](./images/aud24.png)

选择您之前在CJA中创建的受众，然后单击&#x200B;**保存**。

![演示](./images/aud25.png)

准备好了！ 从此处，您可以为符合此区段资格的客户创建历程。

[返回用户流程4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
