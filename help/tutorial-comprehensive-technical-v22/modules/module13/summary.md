---
title: 区段激活到Microsoft Azure事件中心 — 摘要和优势
description: 区段激活到Microsoft Azure事件中心 — 摘要和优势
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 摘要和优点

祝贺您，感谢您花时间学习Microsoft Azure活动中心和Adobe Experience Platform!
在本模块中，您学习了如何设置Azure事件中心实例以及如何将其连接到Adobe Experience Platform。

## 优点

让我们强调Adobe Experience Platform与Microsoft Azure事件中心集成的好处：

- Microsoft Azure事件中心作为Adobe Experience Platform目标，让您能够实时捕获区段鉴别并使用Azure事件中心函数对其进行处理。 借助此Azure事件中心功能，您可以构建任何类型的自定义区段激活处理程序，从而集成任何类型的第三方目标。

- 尽管目标仅由指定的区段触发，但激活有效负载将包含给定用户档案符合条件的所有区段。

- 区段仅在状态发生更改时才会触发激活。 例如，如果某个用户档案在三个月内四次符合某个区段的条件，则只会激活前两个区段。 第一个是状态从更改为 **实现**，则第二个ID会由 **实现** to **现有**.

- 激活已知配置文件的区段时，激活有效负载中会包含完整身份映射。 您的Azure函数可以使用任何可用标识将区段映射到第三方应用程序中管理的配置文件，同时使用应用程序的客户标识符。

- 在此模块中，事件中心函数已部署在本地（Visual Studio代码中的调试模式），为您提供了许多疑难解答和调试选项。

## 看这个

- 不适用

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
