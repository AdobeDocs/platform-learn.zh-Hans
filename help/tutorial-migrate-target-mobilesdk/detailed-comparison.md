---
title: Target扩展与Optimize扩展的比较
description: 了解at.js 2.x与Platform Web SDK之间的差异，包括特性、功能、设置和数据流。
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Target扩展与Optimize扩展的比较

独立的Adobe Target at.js库与Platform Web SDK有显着差异。 下表可供参考，以帮助您评估在迁移过程中可能需要重点实施的各个方面。

在查看以下信息并评估您当前的技术at.js实施后，您应该能够了解以下内容：

- Platform Web SDK支持哪些目标功能
- 哪些at.js函数具有Platform Web SDK等效项
- 如何将Target设置与Platform Web SDK一起使用
- at.js和Platform Web SDK的数据流有何不同

如果您不熟悉Platform Web SDK，请不要担心 — 本教程将更详细地介绍以下项目。

## 功能比较

| | 目标扩展 | 优化扩展(通过Edge定位) | AJO基于代码的体验（消息传送SDK） |
|---|---|---|---|
| 预取模式 | 支持 | 支持 | 支持 |
| 执行模式 | 支持 | 不支持 | 不支持 |
| 自定义参数 | 支持 | 不支持每个mbox参数 | 不支持 |
| 登录受众 | 支持 | 支持 | 通过Campaign受众和试验保留设置支持 |
| 使用移动生命周期量度的受众分段 | 支持 | 通过数据收集规则支持 | 当前不支持体验定位 |
| thirdPartyId (mbox3rdPartyId) | 通过数据流中的身份映射和命名空间配置支持 | 不支持 |
| 通知（显示、点击） | 支持 | 支持 | 支持 |
| 响应令牌 | 支持 | 支持 | 没有等效项可用于返回内容以外的Campaign特定元数据 |
| 动态选件 | 支持 | 支持 | 支持在内容中呈现配置文件和决策项相关的令牌 |
| Analytics for Target (A4T) | 仅客户端 | 客户端和服务器端 | 不支持 |
| 移动设备预览（QA模式） | 支持 | 有限支持 | 进行中 |



## 值得注意的标注

>[!NOTE]
>
>不支持在保留给定页面的现有AppMeasurementAdobe Analytics实施的情况下，将Target迁移到Platform Web SDK。
>
> 可以将您的at.js(和AppMeasurement.js)实施逐页迁移到Platform Web SDK。 如果采用这种方法，最好使用`configure`命令将[`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled)和[`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled)选项设置为`true`。

## Target扩展函数和优化扩展等效项

许多Target扩展函数都使用下表概述的“优化”扩展提供了等效的方法。 有关[函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的更多详细信息，请参阅《Adobe Target开发人员指南》。

| 目标扩展 | 优化扩展 |
| --- | --- | 
| |  |

## Target扩展设置和优化扩展等效项

可以使用……中的各种设置配置和下载Target扩展

| 目标扩展 | 优化扩展 |
| --- | --- | 
| |  |


## 系统图比较

下图应该有助于您了解使用at.js的Target实施与使用Platform Web SDK的实施之间的数据流差异。

### Target扩展系统图



### 优化扩展系统图




>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备从Target扩展迁移到Optimize扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
