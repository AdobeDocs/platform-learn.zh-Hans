---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Target
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# 1.1.6实施Adobe Target

## 更新数据流以使用Adobe Target

如果您希望将Web SDK收集的数据发送到Adobe Target，并从Adobe Target获得响应，以便为每位客户提供个性化体验，请按照以下步骤操作。

转到[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)并转到&#x200B;**数据流**。

在屏幕右上角，选择沙盒名称，应为`--aepSandboxName--`。 打开名为`--aepUserLdap-- - Demo System Datastream`的特定数据流。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1b.png)

你会看到这个。 要启用Adobe Target，请单击&#x200B;**添加服务**。

![AEP调试器](./images/aa2.png)

你会看到这个。 选择服务&#x200B;**Adobe Target**，您可以在此之后选择提供其他信息。 单击&#x200B;**保存**。

![AEP调试器](./images/at1.png)

## 后续步骤

转到Adobe Experience Platform](./ex7.md){target="_blank"}中的[1.1.7 XDM架构要求

返回到[Adobe Experience Platform数据收集和Web SDK标记扩展的设置](./data-ingestion-launch-web-sdk.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
