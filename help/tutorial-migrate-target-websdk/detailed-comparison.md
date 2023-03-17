---
title: at.js 2.x与Web SDK的比较 |将Target从at.js 2.x迁移到Web SDK
description: 了解at.js 2.x与Platform Web SDK之间的差异，包括特性、函数、设置和数据流。
source-git-commit: 28a88e6865211d7d39c18bd48b95070ae0ba259b
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 8%

---

# at.js与Platform Web SDK的比较

独立的Adobe Target at.js库与Platform Web SDK有显着不同。 下表提供了一个参考，可帮助您评估在迁移过程中可能需要重点关注的实施区域。

在查看以下信息并评估当前的at.js技术实施后，您应该能够了解以下信息：

- Platform Web SDK支持哪些Target功能
- 哪些at.js函数具有与Platform Web SDK等效的函数
- 如何将Target设置应用于Platform Web SDK
- at.js和Platform Web SDK的数据流有何不同

如果您是初次使用Platform Web SDK，请不用担心 — 在本教程中，将详细介绍以下项目。

## 功能比较

|  | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 更新Target配置文件 | 受支持 | 受支持 |
| SPA的触发器视图 | 受支持 | 受支持 |
| Target Recommendations | 受支持 | 受支持 |
| 获取基于表单的选件 | 受支持 | 受支持 |
| 跟踪事件 | 受支持 | 受支持 |
| A4T:单页应用程序 | 受支持 | 受支持 |
| A4T:点击跟踪 | 受支持 | 受支持 |
| A4T:客户端日志记录 | 受支持 | 受支持 |
| A4T:服务器端日志记录 | 受支持 | 受支持 |
| 应用选件 | 受支持 | 受支持 |
| 在SPA中重新渲染视图，不发送通知 | 受支持 | 受支持 |
| 混合应用程序 | 受支持 | 受支持 |
| QA URL | 受支持 | 受支持 |
| Mbox第三方ID | 受支持 | 受支持 |
| 客户属性 | 受支持 | 支持 |
| 远程选件 | 受支持 | 受支持 |
| 重定向选件 | 受支持 | 受支持. 但是，不支持从具有Platform Web SDK的页面重定向到具有at.js（且方向相反）的页面。 |
| 设备内决策 | 受支持 | 当前不支持 |
| 预取Mbox | 支持自定义作用域和SPA VEC | 常规VEC当前不支持 |
| 自定义事件 | 受支持 | 不支持。请参阅 [公共路线图](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) 的值。 |
| 响应令牌 | 受支持 | 受支持. 请参阅 [专用响应令牌文档](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) ，以了解代码示例以及at.js和Platform Web SDK之间的差异 |
| 数据提供程序 | 受支持 | 不支持。自定义代码可用于触发平台Web SDK `sendEvent` 命令。 |


## 值得注意的标注

|  | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 闪烁缓解 | 异步实施的预隐藏代码片段使用的样式ID为 `at-body-style`. at.js会在收到响应后查找此元素ID以删除样式。 | 默认的预隐藏代码片段使用样式ID为 `alloy-prehiding`. Web SDK与at.js预隐藏代码片段不兼容，因此必须在迁移过程中对其进行更改。 |
| 在页面加载时自动渲染内容 | 使用Target全局设置进行控制。 在 `pageLoadEnabled` 设置为 `true`. | 在平台Web SDK中指定 `sendEvent` 命令。 通过设置 `renderDecisions` 选项 `true`. |
| 手动渲染内容 | 的 `applyOffer()` 和 `applyOffers()` 仅函数支持设置HTML | 的 `applyPropositions` 命令支持设置、替换或附加HTML，以增加灵活性 |
| 跟踪自定义事件 | 支持 `trackEvent()` 和 `sendNotifications()` 函数。 这些函数专用于Target，不会影响Adobe Analytics量度。 | 来自Platform Web SDK的所有数据 `sendEvent` 调用将转发到Target。 Target特别需要的补充数据应包含在 `sendEvent` 命令，事件类型为 `decisioning.propositionDisplay` 或 `decisioning.propositionInteract` 以确保Adobe Analytics量度不受影响。 |
| Target CNAME | 受支持. 这与用于Analytics的CNAME和Experience CloudID服务不同。 | 不再相关。 单个CNAME可用于所有平台Web SDK调用。 |
| 调试 | 的 `mboxDisable`, `mboxDebug`和 `mboxTrace` URL参数可用于使用浏览器的开发人员工具进行调试。<br><br>Adobe Experience Platform Debugger也是一款受支持的调试工具。 | 的 `mboxDisable`, `mboxDebug`和 `mboxTrace` 不支持URL参数。<br><br>您可以通过添加 `alloy_debug=true` 或执行 `alloy("setDebug", { "enabled": true });` 在开发人员控制台中。<br><br>Adobe Experience Platform Debugger浏览器扩展可用于启动边缘跟踪以进行调试。<br><br>请参阅 [调试平台Web SDK](debugging.md) 文档以了解更多信息。 |
| Analytics for Target (A4T) | 使用SDID值拼合Target和Analytics调用 | 本地支持，无需拼合 |

>[!NOTE]
>
>不支持将Target迁移到Platform Web SDK，同时保留给定页面的现有AppMeasurement Adobe Analytics实施。
>
> 可以将您的at.js（和AppMeasurement.js）实施一次迁移到Platform Web SDK中的一个页面。 如果您采用这种方法，最好将 [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) 和 [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) 选项 `true` 和 `configure` 命令。

## at.js函数和Platform Web SDK等效项

许多at.js函数都使用下表所述的Platform Web SDK来采用等效的方法。 有关 [at.js函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)，请参阅《Adobe Target开发人员指南》。

| at.js 2.x函数 | 平台Web SDK等效项 |
| --- | --- | 
| `getOffer()` 和 `getOffers()` | 请求和 [自动渲染](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) 基于Target VEC的体验，请使用 `sendEvent` 命令并设置 `renderDecisions` 选项设置为true。<br><br>要请求基于表单的体验，或 [手动渲染](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) 内容，指定 `decisionScopes` (mbox) `sendEvent` 命令。 |
| `applyOffer()` 和 `applyOffers()` | 使用 [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) 命令来应用内容。 您可以选择设置、替换HTML或将选项附加到特定选择器。 |
| `triggerView()` | Platform Web SDK会自动触发 [查看更改](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) ，如果 `web.webPageDetails.viewName` 属性在下设置 `xdm` 的 `sendEvent` 命令。 |
| `trackEvent()` 和 `sendNotifications()` | 使用 `sendEvent` 命令 [特定 `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) 设置：<br><br>`decisioning.propositionDisplay` 表示活动的呈现<br><br>`decisioning.propositionInteract` 表示用户与活动的交互，如鼠标单击。 |
| `targetGlobalSettings()` | 没有直接对等项。 请参阅 [Target设置比较](detailed-comparison.md) 以了解更多详细信息。 |
| `targetPageParams()` 和 `targetPageParamsAll()` | 在 `xdm` 的 `sendEvent` 命令映射到Target mbox参数。 由于mbox参数是使用序列化的点表示法命名的，因此迁移到Platform Web SDK可能需要您更新现有受众和活动，以使用新的mbox参数名称。 <br><br>作为 `data.__adobe.target` 的 `sendEvent` 命令映射到 [Target配置文件和Recommendations特定参数](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| at.js 自定义事件 | 不支持。请参阅 [公共路线图](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) 的值。 [响应令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) 作为 `propositions` 的 `sendEvent` 呼叫。 |

## at.js设置和平台Web SDK等效项

可以在Target UI中使用各种设置来配置和下载at.js库。 这些设置还可以使用 [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) 函数。 下表将这些设置与Platform Web SDK中可用的设置进行比较。

| at.js设置 | 平台Web SDK等效项 |
| --- | --- |
| `bodyHiddenStyle` | 设置 [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) 和 `configure` 命令 |
| `bodyHidingEnabled` | 如果 `prehidingStyle` 定义为 `configure` 命令，则此功能将处于启用状态。 如果未定义样式，则Platform Web SDK不会尝试隐藏任何内容。 |
| `clientCode` | 自动配置 |
| `cookieDomain` | 不适用 |
| `crossDomain` | 设置 `thirdPartyCookiesEnabled` 选项 `true` 和 `configure` 命令为跨域用例启用第一方和第三方cookie |
| `cspScriptNonce` 和 `cspStyleNonce` | 请参阅相关文档 [配置CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | 不支持 |
| `decisioningMethod` | 所有平台Web SDK `sendEvent` 命令使用服务器端决策。 不支持混合和设备上决策。 |
| `defaultContentHiddenStyle` 和 `defaultContentVisibleStyle` | 仅适用于at.js 1.x。与at.js 2.x类似，使用自定义代码可以减轻基于表单的体验出现的闪烁问题。 |
| `deviceIdLifetime` | 不支持。如果 `targetMigrationEnabled` 设置为 `true` 和 `configure` 命令， `mbox` cookie设置为设备生命周期设置为2年。 此值不可配置。 |
| `enabled` | 通过数据流配置，可以启用或禁用Target功能 |
| `globalMboxAutoCreate` | 设置 `renderDecisions` 选项 `true` 和 `sendEvent` 命令自动获取和渲染基于VEC的体验。<br><br>请求 `decisionScope` 表示 `__view__` 如果您希望手动渲染基于VEC的体验，请执行以下操作： |
| `imsOrgId` | 设置 `orgId` 和 `configure` 命令 |
| `optinEnabled` 和 `optoutEnabled` | 请参阅平台Web SDK [隐私选项](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). 的 `defaultConsent` 选项适用于Platform Web SDK支持的所有Adobe解决方案。 |
| `overrideMboxEdgeServer` 和 `overrideMboxEdgeServerTimeout` | 不适用. 所有平台Web SDK请求都使用Adobe Experience Platform边缘网络。 |
| `pageLoadEnabled` | 设置 `renderDecisions` 选项 `true` 和 `sendEvent` 命令 |
| `secureOnly` | 不支持。Platform Web SDK会使用 `secure` 和 `sameSite="none"` 属性。 |
| `selectorsPollingTimeout` | 不支持。Platform Web SDK使用5秒的值。 如有必要，可以使用自定义代码手动渲染内容。 |
| `serverDomain` | 使用 `edgeDomain` 设置 `configure` 命令 |
| `telemetryEnabled` | 不适用 |
| `timeout` | 不支持。建议您确保任何闪烁缓解代码都包含适当的超时。 |
| `viewsEnabled` | 不支持。Target视图的内容始终会在第一次获取时获取 `sendEvent()` 呼叫 `renderDecisions` 设置为 `true` 或 `__view__` decisionScope包含在请求中。 |
| `visitorApiTimeout` | 不适用 |


## 系统图比较

下图应该有助于您了解使用at.js的Target实施与使用平台Web SDK的实施之间的数据流差异。

### at.js 2.x系统图

![at.js 2.0页面加载时的行为](assets/target-at-js-2x-diagram.png){zoomable=&quot;yes&quot;}

| 调用 | 详细信息 |
| --- | --- |
| 1 | 调用会返回Experience CloudID(ECID)。 如果用户通过了身份验证，则另一个调用会同步客户ID。 |
| 2 | at.js库会同步加载并隐藏文档正文（也可以选择预先隐藏页面上实施的代码段，以异步方式加载at.js）。 |
| 3 | 将发出页面加载请求，其中包括已配置的所有参数、ECID、SDID和客户ID。 |
| 4 | 配置文件脚本执行并馈送到配置文件存储区。 存储区向受众库请求符合条件的受众(例如从Analytics、Audience Manager等共享的受众)。 客户属性会以批量过程发送到配置文件存储区。 |
| 5 | Target会根据URL、请求参数和配置文件数据来确定要将哪些活动和体验返回给访客以查看当前页面和未来视图。 |
| 6 | 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。<br><br>当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。<br><br>单页应用程序的未来视图的目标内容会缓存在浏览器中，因此在触发视图时，无需额外的服务器调用即可立即应用该内容。 (请参阅下一个图表，了解triggerView()行为。) |
| 7 | 从页面向数据收集服务器发送的Analytics数据。 |
| 8 | Target 数据会通过 SDID 匹配到 Analytics 数据，并且会进行相应处理以保存到 Analytics 报表存储中。之后，便可以在 Analytics 和 Target 中通过 A4T 报表查看 Analytics 数据。 |

请参阅开发人员指南，以了解有关如何 [使用at.js为单页应用程序实施Target](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Platform Web SDK 系统图

![Adobe Target Web SDK边缘决策图](assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载平台Web SDK。 Platform Web SDK会向边缘网络发送请求，其中包含XDM数据、数据流环境ID、传入参数和客户ID（可选）。 页面（或容器）已预隐藏。 |
| 2 | 边缘网络会向边缘服务发送请求，以便通过访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）来扩充请求。 |
| 3 | 边缘网络会使用访客ID和传递的参数将扩充的个性化请求发送到Target边缘。 |
| 4 | 配置文件脚本先执行，然后馈送到Target配置文件存储中。 配置文件存储从受众库中提取区段(例如，从Adobe Analytics、Adobe Audience Manager、Adobe Experience Platform共享的区段)。 |
| 5 | Target会根据URL请求参数和配置文件数据确定要为访客显示哪些活动和体验以用于当前页面查看和将来预取的视图。 然后，Target会将此数据发送回边缘网络。 |
| 6 | a.边缘网络会将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br><br>b.单页应用程序(SPA)中作为用户操作结果显示的视图的个性化内容会缓存以便即时渲染，而无需额外的服务器调用。<br><br>c.边缘网络发送访客ID和Cookie中的其他值（例如同意、会话ID、身份、Cookie检查、个性化等）。 |
| 7 | 边缘网络会将Analytics for Target(A4T)详细信息（活动、体验和转化元数据）转发到Analytics边缘。 |

请参阅开发人员指南，以了解有关如何 [使用适用于单页应用程序的Platform Web SDK实施Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

在您对当前的Target实施和所使用的功能有了良好的技术了解后，下一步就是执行 [初始设置](initial-setup.md).

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
