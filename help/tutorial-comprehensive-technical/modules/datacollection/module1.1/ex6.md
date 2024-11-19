---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Target
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 475e9a34-c80e-41e4-9660-61c79f26922d
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---

# 1.1.6实施Adobe Target

## 更新您的数据流以使用Adobe Target

如果您希望将Web SDK收集的数据发送到Adobe Target，并从Adobe Target中获取响应，从而为每个客户提供个性化体验，请按照以下步骤操作。

转到[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)并转到&#x200B;**数据流**。

在屏幕右上角，选择沙盒名称，应为`--aepSandboxName--`。 打开名为`--aepUserLdap-- - Demo System Datastream`的特定数据流。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1b.png)

你会看到这个。 要启用Adobe Target，请单击&#x200B;**+添加服务**。

![AEP调试器](./images/aa2.png)

你会看到这个。 选择服务&#x200B;**Adobe Target**，您可以在此之后选择提供其他信息。 单击&#x200B;**保存**。

![AEP调试器](./images/at1.png)

下一步： Adobe Experience Platform](./ex7.md)中的[1.1.7 XDM架构要求

[返回模块1.1](./data-ingestion-launch-web-sdk.md)

[返回所有模块](./../../../overview.md)
