---
title: Target扩展与Decisioning扩展的比较
description: 了解Target扩展与Decisioning扩展之间的差异，包括功能、功能、设置和数据流。
source-git-commit: c907ccb9163ace8272f6881638a41362090bf3e5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Target扩展与Decisioning扩展的比较

Adobe Journey Optimizer - Decisioning扩展不同于适用于移动应用程序的Adobe Target扩展。 下表可供参考，以帮助您评估在迁移过程中可能需要重点实施的各个方面。

在查看以下信息并评估您当前的技术性Target扩展实施情况后，您应该能够了解以下内容：

- Adobe Journey Optimizer支持哪些Target功能 — Decisioning
- 哪些Adobe Target扩展函数具有Adobe Journey Optimizer — 决策等效项
- 如何将Target设置应用于Adobe Journey Optimizer - Decisioning
- Adobe Target扩展和Adobe Journey Optimizer - Decisioning扩展的数据流有何不同

如果您不熟悉Platform Web SDK，请不要担心 — 本教程将更详细地介绍以下项目。

## 功能比较

| 功能 | 目标扩展 | Decisioning扩展(通过Edge的Target) |
|---|---|---|
| 预取模式 | 支持 | 支持 |
| 执行模式 | 支持 | 不支持 |
| 自定义参数 | 支持 | 不支持每个mbox参数 |
| 登录受众 | 支持 | 支持 |
| 使用移动生命周期量度的受众分段 | 支持 | 通过数据收集规则支持 |
| thirdPartyId (mbox3rdPartyId) | 支持 | 通过数据流中的身份映射和命名空间配置支持 |
| 通知（显示、点击） | 支持 | 支持 |
| 响应令牌 | 支持 | 支持 |
| 动态选件 | 支持 | 支持 |
| Analytics for Target (A4T) | 仅客户端 | 客户端和服务器端 |
| 移动设备预览（QA模式） | 支持 | 有限支持 |



## 值得注意的标注

>[!NOTE]
>
>不支持在保留给定页面的现有AppMeasurementAdobe Analytics实施的情况下，将Target迁移到Platform Web SDK。
>
> 可以将您的at.js(和AppMeasurement.js)实施逐页迁移到Platform Web SDK。 如果采用这种方法，最好使用`configure`命令将[`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled)和[`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled)选项设置为`true`。

## Target扩展函数和Decisioning扩展的等效项

许多Target扩展函数都具有与使用Decisioning扩展等效的方法，如下表所述。 有关[函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的更多详细信息，请参阅《Adobe Target开发人员指南》。

| 目标扩展 | Decisioning扩展 |
| --- | --- | 
| |  |

## Target扩展设置和Decisioning扩展的等效项

可以使用……中的各种设置配置和下载Target扩展

| 目标扩展 | Decisioning扩展 |
| --- | --- | 
| |  |


## 系统图比较

下图应该有助于您了解使用Adobe Journey Optimizer - Decisioning扩展的Target实施与使用Adobe Target扩展的实施之间的数据流差异。

### Target扩展系统图



### Decisioning扩展系统图




>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
