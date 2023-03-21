---
title: Bootcamp -Customer Journey Analytics — 从分析到操作
description: Bootcamp -Customer Journey Analytics — 从分析到操作
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: e5c2ad88967d7f6a45d3a5cc09ca4c9bc9a62a08
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 4.6从洞察到行动

## 目标

- 了解如何根据在Customer Journey Analytics中收集的视图构建受众
- 在Real-Time CDP和Adobe Journey Optimizer中使用此受众

## 4.6.1创建受众并发布该受众

在您的项目中，您创建了一个名为 **调情** 并能够查看呼叫中心被分类为 **积极**. 现在，您将能够与这些用户一起创建一个区段，并在历程或通信渠道中激活他们。

第一步是：在上一个练习中创建的面板中，选择行 **1. 通话感觉 — 积极**，右键单击并选择 **从选定范围中创建受众** 选项：

![演示](./images/aud1.png)

接下来，按照模型为受众命名 **yourLastName - CJA受众呼叫感觉良好**:

![演示](./images/aud2.png)

请注意，可以预览正在创建的受众：

![演示](./images/aud3.png)

最后，单击 **发布**.

![演示](./images/aud4.png)

## 4.6.2将受众用作区段的一部分

回Adobe Experience Platform，去 **区段>浏览** 并且您将能够看到在CJA中创建的区段已准备就绪，可用于激活和历程！

![演示](./images/aud5.png)

现在，让我们在Facebook激活和客户历程中使用此区段！

## 4.6.3实时使用您在Real-Time CDP中的区段

在Adobe Experience Platform，转到 **区段>浏览** 并查找在CJA中创建的受众：

![演示](./images/aud6.png)

单击您的区段，然后单击 **激活到目标**:

![演示](./images/aud7.png)

选择名为的目标 **bootcamp-facebook**，然后单击 **下一个**.

![演示](./images/aud8.png)

单击 **下一个** 再次。

![演示](./images/aud9.png)

选择 **受众的来源** 选项，并将其设置为 **直接从客户处**，单击 **下一个**.

![演示](./images/aud10.png)

单击&#x200B;**完成**。

![演示](./images/aud11.png)

您的区段现在已连接到Facebook的自定义受众。 现在，让我们在Adobe Journey Optimizer中使用相同的区段。

## 4.6.4在Adobe Journey Optimizer中使用您的区段

在Adobe Experience Platform中，单击 **Journey Optimizer**，然后在左侧菜单中，单击 **历程** 并通过单击 **创建历程**.

![演示](./images/aud20.png)

![演示](./images/aud21.png)

![演示](./images/aud22.png)

然后，在左侧菜单的 **事件**，选择 **区段鉴别** 并将其拖动到历程中：

![演示](./images/aud23.png)

在区段下，单击 **编辑** 要选择区段，请执行以下操作：

![演示](./images/aud24.png)

选择您之前在CJA中创建的受众，然后单击  **保存**.

![演示](./images/aud25.png)

准备！ 从此处，您可以为符合此区段资格的客户创建旅程。

[返回到用户流量4](./uc4.md)

[马多洛斯岛](./../../overview.md)
