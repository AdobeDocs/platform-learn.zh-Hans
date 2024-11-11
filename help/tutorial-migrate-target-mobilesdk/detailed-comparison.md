---
title: Target扩展与Decisioning扩展的比较
description: 了解Target扩展与Decisioning扩展之间的差异，包括功能、功能、设置和数据流。
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 05b0146256c6f8644e42f851498a0f49ff44bf68
workflow-type: tm+mt
source-wordcount: '829'
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
| 自定义参数 | 支持 | 支持* |
| 配置文件参数 | 支持 | 支持* |
| 实体参数 | 支持 | 支持* |
| 目标受众 | 支持 | 支持 |
| Real-Time CDP受众 | ??? | 支持 |
| Real-Time CDP属性 | ??? | 支持 |
| 生命周期量度 | 支持 | 通过数据收集规则支持 |
| thirdPartyId (mbox3rdPartyId) | 支持 | 通过数据流中的身份映射和命名空间配置支持 |
| 通知（显示、点击） | 支持 | 支持 |
| 响应令牌 | 支持 | 支持 |
| Analytics for Target (A4T) | 仅客户端 | 客户端和服务器端 |
| 移动设备预览（QA模式） | 支持 | Assurance有限支持 |

>[!IMPORTANT]
>
> \*在请求中发送的参数适用于请求中的所有范围。 如果需要为不同的范围设置不同的参数，则必须发出其他请求。



## 值得注意的标注

>[!NOTE]
>
>不支持在保留给定页面的现有AppMeasurementAdobe Analytics实施的情况下，将Target迁移到Platform Web SDK。
>
> 可以将您的at.js(和AppMeasurement.js)实施逐页迁移到Platform Web SDK。 如果采用这种方法，最好使用`configure`命令将[`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled)和[`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled)选项设置为`true`。

## Target扩展函数和Decisioning扩展的等效项

许多Target扩展函数都具有与使用Decisioning扩展等效的方法，如下表所述。 有关[函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的更多详细信息，请参阅《Adobe Target开发人员指南》。

| 目标扩展 | Decisioning扩展 | 注释 |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | 使用`getPropositions` API时，不会进行远程调用以获取SDK中的非缓存作用域。 |
| `displayedLocations` | 选件 — > `displayed()` | 此外，`generateDisplayInteractionXdm`选件方法可用于为项目显示生成XDM。 随后，可以使用Edge Network SDK的sendEvent API附加其他XDM自由格式数据并将体验事件发送到远程。 |
| `clickedLocation` | 选件 — > `tapped()` | 此外，`generateTapInteractionXdm`选件方法可用于为项目点按生成XDM。 随后，可以使用Edge Network SDK的sendEvent API附加其他XDM自由格式数据并将体验事件发送到远程。 |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` |  | 使用来自SDK的Edge Network扩展身份的`removeIdentity` API停止向Edge网络发送访客标识符。 有关详细信息，请参阅[removeIdentity API文档](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)。 <br><br>注意： Mobile Core的`resetIdentities` API将清除SDK中所有存储的身份，包括Experience CloudID (ECID)，应谨慎使用它！ |
| `getSessionId` |  | `state:store`响应句柄包含与会话相关的信息。 Edge network extension可将未过期状态存储区项目附加到后续请求，从而帮助管理它。 |
| `setSessionId` |  | `state:store`响应句柄包含与会话相关的信息。 Edge network extension可将未过期状态存储区项目附加到后续请求，从而帮助管理它。 |
| `getThirdPartyId` | 不适用 | 使用用于Edge Network扩展的标识中的updateIdentities API提供第三方ID值。 然后，在数据流中配置第三方ID命名空间。 有关更多详细信息，请参阅[Target第三方ID移动设备文档](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `setThirdPartyId` | 不适用 | 使用用于Edge Network扩展的标识中的updateIdentities API提供第三方ID值。 然后，在数据流中配置第三方ID命名空间。 有关更多详细信息，请参阅[Target第三方ID移动设备文档](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `getTntId` |  | `locationHint:result`响应句柄包含Target位置提示信息。 假设Target Edge将与Experience Edge位于同一位置。<br> <br>Edge网络扩展使用EdgeNetwork位置提示来确定要将请求发送到的Edge网络群集。 要跨SDK（混合应用程序）共享Edge网络位置提示，请使用Edge Network扩展中的`getLocationHint`和`setLocationHint` API。 有关更多详细信息，请参阅[`getLocationHint` API文档](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |
| `setTntId` |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

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
