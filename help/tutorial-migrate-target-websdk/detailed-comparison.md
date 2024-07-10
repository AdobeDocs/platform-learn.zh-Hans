---
title: at.js 2.x与Web SDK的比较 | 将Target从at.js 2.x迁移到Web SDK
description: 了解at.js 2.x与Platform Web SDK之间的差异，包括特性、功能、设置和数据流。
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 299b9586fb5c8e9c9ef3427e08035806af1d9a6b
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 1%

---

# at.js与平台Web SDK的比较

独立的Adobe Target at.js库与Platform Web SDK有显着差异。 下表可供参考，以帮助您评估在迁移过程中可能需要重点实施的各个方面。

在查看以下信息并评估您当前的技术at.js实施后，您应该能够了解以下内容：

- Platform Web SDK支持哪些目标功能
- 哪些at.js函数具有Platform Web SDK等效项
- 如何将Target设置与Platform Web SDK一起使用
- at.js和Platform Web SDK的数据流有何不同

如果您不熟悉Platform Web SDK，请不要担心 — 本教程将更详细地介绍以下项目。

## 功能比较

| | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 更新Target配置文件 | 支持 | 支持 |
| SPA的触发器视图 | 支持 | 支持 |
| 定位Recommendations | 支持 | 支持 |
| 获取基于表单的选件 | 支持 | 支持 |
| 跟踪事件 | 支持 | 支持 |
| A4T：单页应用程序 | 支持 | 支持 |
| A4T：点击跟踪 | 支持 | 支持 |
| A4T：客户端日志记录 | 支持 | 支持 |
| A4T：服务器端日志记录 | 支持 | 支持 |
| 应用优惠 | 支持 | 支持 |
| 在SPA中重新呈现视图，而不发送通知 | 支持 | 支持 |
| 混合应用程序 | 支持 | 支持 |
| QA URL | 支持 | 支持 |
| Mbox第三方ID | 支持 | 支持 |
| 客户属性 | 支持 | 支持 |
| 远程选件 | 支持 | 支持 |
| 重定向选件 | 支持 | 支持。 但是，不支持从具有Platform Web SDK的页面重定向到具有at.js的页面（并且是朝着相反的方向）。 |
| 设备上决策 | 支持 | 当前不支持 |
| 预取Mbox | 支持自定义范围和SPA VEC | 预取是Web SDK的默认模式 |
| 自定义事件 | 支持 | 不支持。 请参阅 [公共路线图](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) 了解当前状态。 |
| 响应令牌 | 支持 | 支持。 请参阅 [专用响应令牌文档](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) 有关代码示例和at.js与Platform Web SDK之间的差异 |
| 数据提供程序 | 支持 | 不支持。 自定义代码可用于触发Platform Web SDK `sendEvent` 从其他提供程序检索数据后的命令。 |


## 值得注意的标注

| | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 减少闪烁 | 异步实施的预隐藏代码片段使用的样式ID为 `at-body-style`. at.js会在收到响应后查找要删除样式的元素ID。 | 默认预隐藏代码片段使用的样式ID为 `alloy-prehiding`. Web SDK与at.js预隐藏代码片段不兼容，因此必须在迁移过程中更改它。 |
| 在页面加载时自动呈现内容 | 使用Target全局设置进行控制。 启用时间 `pageLoadEnabled` 设置为 `true`. | 在平台Web SDK中指定 `sendEvent` 命令。 通过设置 `renderDecisions` 选项至 `true`. |
| 手动呈现内容 | 此 `applyOffer()` 和 `applyOffers()` 函数仅支持设置HTML | 此 `applyPropositions` 命令支持设置、替换或附加HTML以增加灵活性 |
| 跟踪自定义事件 | 支持 `trackEvent()` 和 `sendNotifications()` 函数。 这些函数特定于Target，不会影响Adobe Analytics指标。 | 来自Platform Web SDK的所有数据 `sendEvent` 呼叫将转发到Target。 Target特别需要的补充数据应包含在 `sendEvent` 具有eventType的命令 `decisioning.propositionDisplay` 或 `decisioning.propositionInteract` 以确保Adobe Analytics指标不受影响。 |
| 目标CNAME | 支持。 这与用于Analytics和Experience CloudID服务的CNAME不同。 | 不再相关。 单个CNAME可用于所有Platform Web SDK调用。 |
| 调试 | 此 `mboxDisable`， `mboxDebug`、和 `mboxTrace` URL参数可用于使用浏览器的开发人员工具进行调试。<br><br>该Adobe Experience Platform Debugger也是一种受支持的调试工具。 | 此 `mboxDisable`， `mboxDebug`、和 `mboxTrace` 不支持URL参数。<br><br>您可以通过添加 `alloy_debug=true` 到您的查询字符串或正在执行 `alloy("setDebug", { "enabled": true });` 在开发人员控制台中。<br><br>Adobe Experience Platform Debugger浏览器扩展可用于启动边缘跟踪以进行调试。<br><br>请参阅 [调试Platform Web SDK](debugging.md) 文档，以了解更多信息。 |
| Analytics for Target (A4T) | 使用SDID值拼合Target和Analytics调用 | 本机支持，无需拼接 |

>[!NOTE]
>
>不支持在保留给定页面的现有AppMeasurementAdobe Analytics实施的情况下，将Target迁移到Platform Web SDK。
>
> 可以将您的at.js(和AppMeasurement.js)实施逐页迁移到Platform Web SDK。 如果采用这种方法，最好设置 [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) 和 [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) 选项 `true` 使用 `configure` 命令。

## at.js函数和Platform Web SDK等效项

许多at.js函数都有一个等效的方法，使用Platform Web SDK时，如下表所述。 欲知关于 [at.js函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)，请参阅Adobe Target开发人员指南。

| at.js 2.x函数 | Platform Web SDK等效项 |
| --- | --- | 
| `getOffer()` 和 `getOffers()` | 要请求和 [自动呈现](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) 定位基于VEC的体验，使用 `sendEvent` 命令并设置 `renderDecisions` 选项设置为true。<br><br>要请求基于表单的体验或 [手动渲染](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) 内容，指定数组 `decisionScopes` (mbox)与 `sendEvent` 命令。 |
| `applyOffer()` 和 `applyOffers()` | 使用 [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) 命令以应用内容。 您可以选择设置、替换HTML或将其附加到特定选择器。 |
| `triggerView()` | Platform Web SDK自动触发 [视图更改](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) 对于SPA VEC，如果 `web.webPageDetails.viewName` 属性在 `xdm` 的选项 `sendEvent` 命令。 |
| `trackEvent()` 和 `sendNotifications()` | 使用 `sendEvent` 命令和 [特定 `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) 设置：<br><br>`decisioning.propositionDisplay` 表示活动的呈现<br><br>`decisioning.propositionInteract` 表示用户与活动（如鼠标单击）的交互。 |
| `targetGlobalSettings()` | 没有直接等效项。 请参阅 [Target设置比较](detailed-comparison.md) 以了解更多详细信息。 |
| `targetPageParams()` 和 `targetPageParamsAll()` | 所有传入数据 `xdm` 的选项 `sendEvent` 命令映射到Target mbox参数。 由于mbox参数使用序列化的点表示法命名，迁移到Platform Web SDK可能需要您更新现有受众和活动以使用新的mbox参数名称。 <br><br>作为的一部分传递的数据 `data.__adobe.target` 的 `sendEvent` 命令已映射到 [Target配置文件和Recommendations特定参数](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| at.js自定义事件 | 不支持。 请参阅 [公共路线图](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) 了解当前状态。 [响应令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) 作为的一部分 `propositions` 作为回应 `sendEvent` 呼叫。 |

## at.js设置和平台Web SDK等效项

可以使用Target UI中的各种设置配置和下载at.js库。 这些设置也可以更新为 [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) 函数。 下表将这些设置与Platform Web SDK中的可用设置进行了比较。

| at.js设置 | Platform Web SDK等效项 |
| --- | --- |
| `bodyHiddenStyle` | 设置 [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) 使用 `configure` 命令 |
| `bodyHidingEnabled` | 如果 `prehidingStyle` 是使用 `configure` 命令，则会启用此功能。 如果未定义样式，则Platform Web SDK不会尝试隐藏任何内容。 |
| `clientCode` | 自动配置 |
| `cookieDomain` | 不适用 |
| `crossDomain` | 设置 `thirdPartyCookiesEnabled` 选项至 `true` 使用 `configure` 命令为跨域用例启用第一方和第三方Cookie |
| `cspScriptNonce` 和 `cspStyleNonce` | 请参阅相关文档 [配置CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | 不支持 |
| `decisioningMethod` | 所有Platform Web SDK `sendEvent` 命令使用服务器端决策。 不支持混合决策和设备上决策。 |
| `defaultContentHiddenStyle` 和 `defaultContentVisibleStyle` | 仅适用于at.js 1.x。与at.js 2.x类似，可以使用自定义代码缓解基于表单的体验出现的任何闪烁。 |
| `deviceIdLifetime` | 不支持。 如果 `targetMigrationEnabled` 设置为 `true` 使用 `configure` 命令， `mbox` Cookie在设备生命周期设置为2年的情况下进行设置。 此值不可配置。 |
| `enabled` | 通过数据流配置启用或禁用目标功能 |
| `globalMboxAutoCreate` | 设置 `renderDecisions` 选项至 `true` 使用 `sendEvent` 用于自动获取和渲染基于VEC的体验的命令。<br><br>请求 `decisionScope` 对象 `__view__` 如果您希望手动渲染基于VEC的体验。 |
| `imsOrgId` | 设置 `orgId` 使用 `configure` 命令 |
| `optinEnabled` 和 `optoutEnabled` | 请参阅平台Web SDK [隐私选项](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). 此 `defaultConsent` 选项适用于Platform Web SDK支持的所有Adobe解决方案。 |
| `overrideMboxEdgeServer` 和 `overrideMboxEdgeServerTimeout` | 不适用。 所有Platform Web SDK请求都使用Adobe Experience Platform Edge网络。 |
| `pageLoadEnabled` | 设置 `renderDecisions` 选项至 `true` 使用 `sendEvent` 命令 |
| `secureOnly` | 不支持。 Platform Web SDK使用设置所有Cookie `secure` 和 `sameSite="none"` 属性。 |
| `selectorsPollingTimeout` | 不支持。 Platform Web SDK使用的值为5秒。 如果需要，可以使用自定义代码手动渲染内容。 |
| `serverDomain` | 使用 `edgeDomain` 使用设置 `configure` 命令 |
| `telemetryEnabled` | 不适用 |
| `timeout` | 不支持。 建议您确保任何闪烁缓解代码都包含适当的超时。 |
| `viewsEnabled` | 不支持。 始终在第一次访问时获取Target视图的内容 `sendEvent()` 调用if `renderDecisions` 设置为 `true` 或 `__view__` decisionScope包含在请求中。 |
| `visitorApiTimeout` | 不适用 |


## 系统图比较

下图应该有助于您了解使用at.js的Target实施与使用Platform Web SDK的实施之间的数据流差异。

### at.js 2.x系统图

![at.js 2.0页面加载行为](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| 调用 | 详细信息 |
| --- | --- |
| 1 | 调用返回Experience CloudID (ECID)。 如果用户通过了身份验证，则另一调用会同步客户ID。 |
| 2 | at.js库会同步加载并隐藏文档正文（也可以选择预先隐藏页面上实施的代码段，以异步方式加载at.js）。 |
| 3 | 将会发出页面加载请求，其中包括已配置的所有参数，如ECID、SDID和客户ID。 |
| 4 | 配置文件脚本执行并进入配置文件存储区。 存储区向受众库请求符合条件的受众(例如，从Analytics、Audience Manager等共享的受众)。 客户属性会以批量过程发送到配置文件存储区。 |
| 5 | Target会根据URL、请求参数和配置文件数据，决定可为访客返回哪些当前页面和未来视图的活动和体验。 |
| 6 | 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。<br><br>当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。<br><br>单页应用程序的未来视图的目标内容将缓存在浏览器中，因此当视图触发时，可以立即应用它而无需额外的服务器调用。 |
| 7 | 从页面发送到数据收集服务器的Analytics数据。 |
| 8 | Target数据会通过SDID匹配到Analytics数据，并且会进行相应处理以保存到Analytics报表存储中。 之后，便可以在Analytics和Target中通过A4T报表查看Analytics数据。 |

请参阅开发人员指南，了解如何 [使用at.js为单页应用程序实施Target](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Platform Web SDK系统图

![使用Platform Web SDK的Adobe Target Edge Decisioning示意图](assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载Platform Web SDK。 Platform Web SDK使用XDM数据、数据流环境ID、传入参数和客户ID（可选）向边缘网络发送请求。 页面（或容器）为预隐藏。 |
| 2 | 边缘网络将请求发送到边缘服务，以使用访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）扩充其内容。 |
| 3 | 边缘网络使用访客ID和传入的参数将扩充的个性化请求发送到Target边缘。 |
| 4 | 配置文件脚本在执行后进入到Target配置文件存储中。 配置文件存储从受众库中获取区段(例如，从Adobe Analytics、Adobe Audience Manager、Adobe Experience Platform共享的区段)。 |
| 5 | 根据URL请求参数和配置文件数据，Target可确定将为访客显示的当前页面视图和未来预取视图的活动和体验。 然后，Target将此数据发送回边缘网络。 |
| 6 | a.边缘网络将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br><br>b.作为用户操作在单页应用程序(SPA)中显示的视图的个性化内容将缓存以供即时呈现，而无需额外的服务器调用。<br><br>c.边缘网络发送访客ID和Cookie中的其他值（例如同意、会话ID、身份、Cookie检查、个性化等等）。 |
| 7 | 边缘网络将Analytics for Target (A4T)详细信息（活动、体验和转化元数据）转发到Analytics边缘。 |

请参阅开发人员指南，了解如何 [使用适用于单页应用程序的Platform Web SDK实施Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

在您从技术角度充分了解了当前的Target实施以及您使用的功能后，下一步是执行 [初始设置](initial-setup.md).

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少重要信息，请发帖告诉我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
