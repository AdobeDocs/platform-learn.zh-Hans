---
title: Microsoft Azure活动中心Audience Activation — 摘要和优势
description: Microsoft Azure活动中心Audience Activation — 摘要和优势
kt: 5342
doc-type: tutorial
exl-id: 3b598ffc-875e-468d-b91c-882062e8203f
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# 摘要和优点

恭喜并感谢您投入时间学习Microsoft Azure活动中心和Adobe Experience Platform！
在本模块中，您已了解如何设置Azure事件中心实例，以及如何将其连接到Adobe Experience Platform。

## 优点

让我们重点介绍Adobe Experience Platform与Microsoft Azure事件中心集成的好处：

- 将Microsoft Azure事件中心作为Adobe Experience Platform目标可让您实时捕获受众资格，并使用Azure事件中心功能处理这些资格。 通过这样的Azure事件中心函数，您可以构建任何类型的自定义受众激活处理程序，并集成任何类型的第三方目标。

- 尽管目标仅由指定的受众触发，但激活有效负载将包含给定配置文件符合条件的所有受众。

- 受众仅在状态更改时触发激活。 例如，如果用户档案在三个月中四次符合某个受众的条件，则只会激活前两个受众。 第一个是从&#x200B;**已实现**&#x200B;的状态更改，第二个是由从&#x200B;**已实现**&#x200B;到&#x200B;**现有**&#x200B;的状态更改触发的。

- 为已知配置文件激活受众时，激活有效负载中包含完整的标识映射。 Azure函数可使用任意可用标识将受众映射到在第三方应用程序中管理的配置文件，同时使用该应用程序的客户标识符。

- 在此模块中，事件中心函数已本地部署（Visual Studio Code中的调试模式），为您提供了许多故障排除和调试选项。

## 看看这个

- 不适用

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
