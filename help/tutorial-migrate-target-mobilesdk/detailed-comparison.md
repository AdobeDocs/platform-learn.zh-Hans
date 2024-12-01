---
title: Target扩展与Decisioning扩展的比较
description: 了解Target扩展与Decisioning扩展之间的差异，包括功能、功能、设置和数据流。
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 8e4e23413c842f84159891287d09e8a6cfbbbc53
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 3%

---

# Target扩展与Decisioning扩展的比较

Adobe Journey Optimizer - Decisioning扩展不同于适用于移动应用程序的Adobe Target扩展。 下表可供参考，以帮助您评估在迁移过程中可能需要重点实施的各个方面。

在查看以下信息并评估您当前的技术性Target扩展实施情况后，您应该能够了解以下内容：

- Adobe Journey Optimizer支持哪些Target功能 — Decisioning
- 哪些Adobe Target扩展函数具有Adobe Journey Optimizer — 决策等效项
- 如何将Target设置应用于Adobe Journey Optimizer - Decisioning
- 使用Adobe Journey Optimizer - Decisioning扩展时的数据流动方式


## 功能比较

| 功能 | 目标扩展 | Decisioning扩展(通过Edge的Target) |
|---|---|---|
| 预取模式 | 支持 | 支持 |
| 执行模式 | 支持 | 不支持 |
| 自定义参数 | 支持 | 支持* |
| 轮廓参数 | 支持 | 支持* |
| 实体参数 | 支持 | 支持* |
| 目标受众 | 支持 | 支持 |
| Real-Time CDP受众 | 不支持 | 支持 |
| Real-Time CDP属性 | 不支持 | 支持 |
| 生命周期量度 | 支持 | 通过数据收集规则支持 |
| thirdPartyId (mbox3rdPartyId) | 支持 | 通过数据流中的身份映射和Target第三方ID命名空间支持 |
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
>即使在将应用程序代码迁移到Decisioning扩展后，仍应保持Target扩展标记配置和设置不变。 这有助于确保尚未将应用程序更新到新版本的客户能够继续使用Target。
>
>如果您使用Analytics for Target集成(A4T)，则在将Target实施迁移到Decisioning扩展时，请务必同时使用Edge Bridge扩展迁移Analytics实施。

## Target扩展函数和Decisioning扩展的等效项

许多Target扩展函数都具有与使用Decisioning扩展等效的方法，如下表所述。 有关[函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的更多详细信息，请参阅《Adobe Target开发人员指南》。

| 目标扩展 | Decisioning扩展 | 注释 |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | 使用`getPropositions` API时，不会进行远程调用以获取SDK中的非缓存作用域。 |
| `displayedLocations` | 选件 — > `displayed()` | 此外，`generateDisplayInteractionXdm`选件方法可用于为项目显示生成XDM。 随后，可以使用Edge Network SDK的sendEvent API附加其他XDM自由格式数据并将体验事件发送到远程。 |
| `clickedLocation` | 选件 — > `tapped()` | 此外，`generateTapInteractionXdm`选件方法可用于为项目点按生成XDM。 随后，可以使用Edge Network SDK的sendEvent API附加其他XDM自由格式数据并将体验事件发送到远程。 |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | 不适用 | 使用来自SDK的Edge Network扩展身份的`removeIdentity` API停止向Edge网络发送访客标识符。 有关详细信息，请参阅[removeIdentity API文档](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)。 <br><br>注意： Mobile Core的`resetIdentities` API将清除SDK中所有存储的身份，包括Experience CloudID (ECID)，应谨慎使用它！ |
| `getSessionId` | 不适用 | `state:store`响应句柄包含与会话相关的信息。 Edge network extension可将未过期状态存储区项目附加到后续请求，从而帮助管理它。 |
| `setSessionId` | 不适用 | `state:store`响应句柄包含与会话相关的信息。 Edge network extension可将未过期状态存储区项目附加到后续请求，从而帮助管理它。 |
| `getThirdPartyId` | 不适用 | 使用用于Edge Network扩展的标识中的updateIdentities API提供第三方ID值。 然后，在数据流中配置第三方ID命名空间。 有关更多详细信息，请参阅[Target第三方ID移动设备文档](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `setThirdPartyId` | 不适用 | 使用用于Edge Network扩展的标识中的updateIdentities API提供第三方ID值。 然后，在数据流中配置第三方ID命名空间。 有关更多详细信息，请参阅[Target第三方ID移动设备文档](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `getTntId` | 不适用 | `locationHint:result`响应句柄包含Target位置提示信息。 假设Target Edge将与Experience Edge位于同一位置。<br> <br>Edge网络扩展使用EdgeNetwork位置提示来确定要将请求发送到的Edge网络群集。 要跨SDK（混合应用程序）共享Edge网络位置提示，请使用Edge Network扩展中的`getLocationHint`和`setLocationHint` API。 有关更多详细信息，请参阅[`getLocationHint` API文档](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |
| `setTntId` | 不适用 | `locationHint:result`响应句柄包含Target位置提示信息。 假设Target Edge将与Experience Edge位于同一位置。<br> <br>Edge网络扩展使用EdgeNetwork位置提示来确定要将请求发送到的Edge网络群集。 要跨SDK（混合应用程序）共享Edge网络位置提示，请使用Edge Network扩展中的`getLocationHint`和`setLocationHint` API。 有关更多详细信息，请参阅[`getLocationHint` API文档](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |

## Target扩展设置和Decisioning扩展的等效项

Target扩展具有[可配置的设置](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)，这些设置是在具有Decisioning扩展的数据流](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup)中配置的[。

| 目标扩展 | Decisioning扩展 | 注释 |
| --- | --- | --- | 
| 客户端代码 | 不适用 | 边缘使用IMS组织详细信息自动设置 |
| 环境ID | 目标环境ID | 已在数据流中配置 |
| Target Workspace资产 | 资产令牌 | 已在数据流中配置 |
| 超时 | 不可配置 | Decisioning扩展的超时为10秒 |
| Server Domain | Edge Network域 | 在Adobe Experience PlatformEdge Network扩展中设置 |

>[!IMPORTANT]
>
> 即使将应用程序代码迁移到Decisioning扩展，Target扩展设置仍保持不变。 这有助于确保Target继续适用于尚未更新应用程序的用户。

## Decisioning扩展系统图

下图应该可以帮助您了解使用Adobe Journey Optimizer - Decisioning扩展的数据流。

具有客户端Mobile SDK的![Adobe Target Edge Decisioning](assets/diagram.png)


>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
