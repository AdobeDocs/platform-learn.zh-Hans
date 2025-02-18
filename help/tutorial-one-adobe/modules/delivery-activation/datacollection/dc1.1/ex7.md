---
title: 基础 — Adobe Experience Platform数据收集和Web SDK扩展的设置 — Adobe Experience Platform中的XDM架构要求
description: 基础 — Adobe Experience Platform数据收集和Web SDK扩展的设置 — Adobe Experience Platform中的XDM架构要求
kt: 5342
doc-type: tutorial
exl-id: 124c9c54-27f1-4784-9a5c-2c9d8ba620d5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 1.1.7 Adobe Experience Platform中的XDM架构要求

为了确保Web SDK能够将数据摄取到Adobe Experience Platform，需要特定的XDM mixin才能成为Adobe Experience Platform中XDM架构的一部分。

转到[https://experience.adobe.com/platform](https://experience.adobe.com/platform)并登录。

![AEP调试器](./images/exp1.png)

登录后，单击屏幕顶部蓝线中的文本&#x200B;**Production Prod**&#x200B;以选择相应的沙盒。 选择沙盒`--aepSandboxName--`。

选择沙盒后，您会看到屏幕变化，现在您已经进入沙盒。

![AEP调试器](./images/exp2.png)

在左侧菜单中，转到&#x200B;**架构**&#x200B;并打开网站的&#x200B;**演示系统 — 事件架构(Global v1.1)**&#x200B;架构。

![AEP调试器](./images/exp3.png)

在该架构中，您会看到已添加字段组&#x200B;**AEP Web SDK ExperienceEvent**&#x200B;字段组。 此字段组将所有最低要求字段添加到架构中。 Web SDK将使用Adobe Experience Platform中的每个Experience Event架构，始终要求将该字段组作为架构的一部分。

![AEP调试器](./images/exp4.png)

在[模块1.2数据摄取](./../dc1.2/data-ingestion.md)中，您将了解如何向架构添加字段组。

下一步：

## 后续步骤

转到[摘要和优点](./summary.md){target="_blank"}

返回到[Adobe Experience Platform数据收集和Web SDK标记扩展的设置](./data-ingestion-launch-web-sdk.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
