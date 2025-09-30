---
title: at.js 2.x与Web SDK的比较 — 将Target从at.js 2.x迁移到Web SDK
description: 了解at.js 2.x与Platform Web SDK之间的差异，包括特性、功能、设置和数据流。
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 7d3c1728925e322f9313cf71f081500e0c0bac0b
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 1%

---

# at.js与Platform Web SDK的比较

独立的Adobe Target at.js库与Platform Web SDK存在显着差异。 下表可供参考，以帮助您评估在迁移过程中可能需要重点实施的各个方面。

在查看以下信息并评估您当前的技术at.js实施后，您应该能够了解以下内容：

- Platform Web SDK支持哪些目标功能
- 哪些at.js函数具有Platform Web SDK等效项
- 如何将Target设置应用于平台Web SDK
- at.js和Platform Web SDK的数据流有何不同

如果您是Platform Web SDK的新用户，请不要担心 — 本教程将更详细地介绍以下项目。

## 功能比较

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 更新Target配置文件 | 支持 | 支持 |
| SPA的触发器视图 | 支持 | 支持 |
| Target推荐 | 支持 | 支持 |
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
| 远程选件 | 支持 | 部分支持。 不支持动态远程选件。 |
| 重定向选件 | 支持 | 支持。 但是，不支持从具有Platform Web SDK的页面重定向到具有at.js的页面（并且是朝着相反的方向）。 |
| 设备上决策 | 支持 | 当前不支持 |
| 预取Mbox | 支持自定义范围和SPA VEC | 预取是Web SDK的默认模式 |
| 自定义事件 | 支持 | 不支持。 查看[公共路线图](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"})以了解当前状态。 |
| 响应令牌 | 支持 | 支持。 有关at.js与Platform Web SDK之间的代码示例和差异，请参阅[专用响应令牌文档](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans) |
| 数据提供程序 | 支持 | 不支持。 在从其他提供程序检索数据之后，可以使用自定义代码触发Platform Web SDK `sendEvent`命令。 |


## 值得注意的标注

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 减少闪烁 | 异步实施的预隐藏代码片段使用样式ID `at-body-style`。 at.js会在收到响应后查找要删除样式的元素ID。 | 默认预隐藏代码片段使用的样式ID为`alloy-prehiding`。 Web SDK与at.js预隐藏代码片段不兼容，因此必须在迁移过程中更改该代码片段。 |
| 在页面加载时自动呈现内容 | 使用Target全局设置进行控制。 当`pageLoadEnabled`设置为`true`时启用。 | 在Platform Web SDK `sendEvent`命令中指定。 通过将`renderDecisions`选项设置为`true`启用。 |
| 手动呈现内容 | `applyOffer()`和`applyOffers()`函数仅支持设置HTML | `applyPropositions`命令支持设置、替换或附加HTML以增加灵活性 |
| 跟踪自定义事件 | `trackEvent()`和`sendNotifications()`函数支持。 这些函数特定于Target，不会影响Adobe Analytics指标。 | Platform Web SDK `sendEvent`调用中的所有数据都会转发到Target。 Target特别需要的补充数据应包含在事件类型为`sendEvent`或`decisioning.propositionDisplay`的`decisioning.propositionInteract`命令中，以确保Adobe Analytics指标不受影响。 |
| 目标CNAME | 支持。 这与用于Analytics和Experience Cloud ID服务的CNAME不同。 | 不再相关。 单个CNAME可用于所有Platform Web SDK调用。 |
| 调试 | `mboxDisable`、`mboxDebug`和`mboxTrace` URL参数可用于使用浏览器的开发人员工具进行调试。<br><br>Adobe Experience Platform Debugger也是一种受支持的调试工具。 | 不支持`mboxDisable`、`mboxDebug`和`mboxTrace` URL参数。<br><br>您可以通过将`alloy_debug=true`添加到查询字符串或在开发人员控制台中执行`alloy("setDebug", { "enabled": true });`来打开Web SDK调试。<br><br>Adobe Experience Platform Debugger浏览器扩展可用于启动边缘跟踪以进行调试。<br><br>有关详细信息，请参阅[调试Platform Web SDK](debugging.md)文档。 |
| Analytics for Target (A4T) | 使用SDID值拼合Target和Analytics调用 | 本机支持，无需拼接 |

>[!NOTE]
>
>不支持在将Target迁移到Platform Web SDK的同时保留给定页面的现有AppMeasurement Adobe Analytics实施。
>
> 可以将您的at.js(和AppMeasurement.js)实施逐页迁移到Platform Web SDK。 如果采用这种方法，最好使用[`idMigrationEnabled`命令将](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hans#id-migration-enabled) [`targetMigrationEnabled`和](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hans#targetMigrationEnabled)`true`选项设置为`configure`。

## at.js函数和Platform Web SDK等效函数

许多at.js函数都具有使用Platform Web SDK的等效方法，如下表所述。 有关[at.js函数](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的更多详细信息，请参阅《Adobe Target开发人员指南》。

| at.js 2.x函数 | Platform Web SDK等效项 |
| --- | --- | 
| `getOffer()` 和 `getOffers()` | 若要请求和[自动渲染](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hans#automatically-rendering-content)基于Target VEC的体验，请使用`sendEvent`命令并将`renderDecisions`选项设置为true。<br><br>要请求基于表单的体验或[手动渲染](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hans#manually-rendering-content)内容，请使用`decisionScopes`命令指定一个由`sendEvent` (mbox)组成的数组。 |
| `applyOffer()` 和 `applyOffers()` | 使用[`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hans#applypropositions)命令应用内容。 您可以选择将HTML设置、替换或附加到特定选择器。 |
| `triggerView()` | 如果在[命令的](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=zh-Hans#how-to-trigger-a-view-change-in-a-single-page-application)选项下设置了`web.webPageDetails.viewName`属性，则Platform Web SDK会自动触发用于SPA VEC的`xdm`视图更改`sendEvent`。 |
| `trackEvent()` 和 `sendNotifications()` | 使用包含`sendEvent`特定[`eventType`集的](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=zh-Hans#how-to-track-events)命令：<br><br>`decisioning.propositionDisplay`表示呈现活动<br><br>`decisioning.propositionInteract`，表示用户与某个活动的交互，如鼠标单击。 |
| `targetGlobalSettings()` | 没有直接等效项。 有关其他详细信息，请参阅[Target设置比较](detailed-comparison.md)。 |
| `targetPageParams()` 和 `targetPageParamsAll()` | 在`xdm`命令的`sendEvent`选项中传递的所有数据都映射到Target mbox参数。 由于mbox参数使用序列化的点表示法命名，迁移到Platform Web SDK时，您可能需要更新现有受众和活动才能使用新的mbox参数名称。 <br><br>作为`data.__adobe.target`命令的`sendEvent`的一部分传递的数据映射到[目标配置文件和推荐特定参数](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=zh-Hans#single-profile-update)。 |
| at.js自定义事件 | 不支持。 查看[公共路线图](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"})以了解当前状态。 [响应令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html?lang=zh-Hans)在`propositions`调用的响应中作为`sendEvent`的一部分公开。 |

## at.js设置和平台Web SDK等效项

可以使用Target UI中的各种设置配置和下载at.js库。 也可以使用[`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/)函数更新这些设置。 下表将这些设置与Platform Web SDK中的可用设置进行了比较。

| at.js设置 | Platform Web SDK等效项 |
| --- | --- |
| `bodyHiddenStyle` | 使用[`prehidingStyle`命令设置](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hans#prehidingStyle)`configure` |
| `bodyHidingEnabled` | 如果使用`prehidingStyle`命令定义了`configure`，则会启用此功能。 如果未定义样式，则Platform Web SDK不会尝试隐藏任何内容。 |
| `clientCode` | 自动配置 |
| `cookieDomain` | 不适用 |
| `crossDomain` | 使用`thirdPartyCookiesEnabled`命令将`true`选项设置为`configure`，以便为跨域用例启用第一方和第三方Cookie |
| `cspScriptNonce` 和 `cspStyleNonce` | 请参阅有关[配置CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html?lang=zh-Hans)的文档 |
| `dataProviders` | 不受支持 |
| `decisioningMethod` | 所有Platform Web SDK `sendEvent`命令都使用服务器端决策。 不支持混合决策和设备上决策。 |
| `defaultContentHiddenStyle` 和 `defaultContentVisibleStyle` | 仅适用于at.js 1.x。与at.js 2.x类似，可以使用自定义代码缓解基于表单的体验出现的任何闪烁。 |
| `deviceIdLifetime` | 不支持。 如果使用`targetMigrationEnabled`命令将`true`设置为`configure`，则将`mbox` Cookie设置为设备生命周期设置为2年。 此值不可配置。 |
| `enabled` | 通过数据流配置启用或禁用目标功能 |
| `globalMboxAutoCreate` | 使用`renderDecisions`命令将`true`选项设置为`sendEvent`以自动获取和渲染基于VEC的体验。如果您希望手动渲染基于VEC的体验，请<br><br>为`decisionScope`请求`__view__`。 |
| `imsOrgId` | 使用`orgId`命令设置`configure` |
| `optinEnabled` 和 `optoutEnabled` | 请参阅平台Web SDK [隐私选项](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=zh-Hans)。 `defaultConsent`选项适用于平台Web SDK支持的所有Adobe解决方案。 |
| `overrideMboxEdgeServer` 和 `overrideMboxEdgeServerTimeout` | 不适用。 所有Platform Web SDK请求都使用Adobe Experience Platform Edge网络。 |
| `pageLoadEnabled` | 使用`renderDecisions`命令将`true`选项设置为`sendEvent` |
| `secureOnly` | 不支持。 Platform Web SDK使用`secure`和`sameSite="none"`属性设置所有Cookie。 |
| `selectorsPollingTimeout` | 不支持。 Platform Web SDK使用值5秒。 如果需要，可以使用自定义代码手动渲染内容。 |
| `serverDomain` | 在`edgeDomain`命令中使用`configure`设置 |
| `telemetryEnabled` | 不适用 |
| `timeout` | 不支持。 建议您确保任何闪烁缓解代码都包含适当的超时。 |
| `viewsEnabled` | 不支持。 如果将`sendEvent()`设置为`renderDecisions`或请求中包含`true` decisionScope，则始终在前`__view__`次调用中获取Target视图的内容。 |
| `visitorApiTimeout` | 不适用 |


## 系统图比较

下图应该有助于您了解使用at.js的Target实施与使用Platform Web SDK的实施之间的数据流差异。

### at.js 2.x系统图

![at.js 2.0在页面加载时的行为](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| 调用 | 详细信息 |
| --- | --- |
| 1 | 调用返回Experience Cloud ID (ECID)。 如果用户通过了身份验证，则另一调用会同步客户ID。 |
| 2 | at.js库会同步加载并隐藏文档正文（也可以选择预先隐藏页面上实施的代码段，以异步方式加载at.js）。 |
| 3 | 将会发出页面加载请求，其中包括已配置的所有参数，如ECID、SDID和客户ID。 |
| 4 | 配置文件脚本执行并进入配置文件存储区。 存储区向受众库请求符合条件的受众(例如，从Analytics、Audience Manager等共享的受众)。 客户属性会以批量过程发送到配置文件存储区。 |
| 5 | Target会根据URL、请求参数和配置文件数据，决定可为访客返回哪些当前页面和未来视图的活动和体验。 |
| 6 | 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。<br><br>当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。<br><br>单页应用程序未来视图的目标内容将缓存在浏览器中，因此当视图触发时，可以立即应用它而无需额外的服务器调用。 |
| 7 | 从页面发送到数据收集服务器的Analytics数据。 |
| 8 | Target数据会通过SDID匹配到Analytics数据，并且会进行相应处理以保存到Analytics报表存储中。 之后，便可以在Analytics和Target中通过A4T报表查看Analytics数据。 |

请参阅开发人员指南以了解如何[使用单页应用程序的at.js实施Target](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/)的更多信息。

### Platform Web SDK系统图

![使用Platform Web SDK的Adobe Target Edge Decisioning图表](assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载Platform Web SDK。 Platform Web SDK向边缘网络发送请求，请求中包含XDM数据、数据流环境ID、传入参数和客户ID（可选）。 页面（或容器）为预隐藏。 |
| 2 | 边缘网络将请求发送到边缘服务，以使用访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）扩充其内容。 |
| 3 | 边缘网络使用访客ID和传入的参数将扩充的个性化请求发送到Target边缘。 |
| 4 | 配置文件脚本在执行后进入到Target配置文件存储中。 配置文件存储从受众库中获取区段(例如，从Adobe Analytics、Adobe Audience Manager、Adobe Experience Platform共享的区段)。 |
| 5 | 根据URL请求参数和配置文件数据，Target可确定将为访客显示的当前页面视图和未来预取视图的活动和体验。 然后，Target将此数据发送回边缘网络。 |
| 6 | a.边缘网络将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br><br>b。作为用户在单页应用程序(SPA)中的操作结果而显示的视图的个性化内容将缓存以供即时渲染，而无需额外的服务器调用。<br><br>c。边缘网络发送访客ID和Cookie中的其他值（例如同意、会话ID、身份、Cookie检查、个性化等等）。 |
| 7 | 边缘网络将Analytics for Target (A4T)详细信息（活动、体验和转化元数据）转发到Analytics边缘。 |

请参阅开发人员指南，了解如何[使用适用于单页应用程序的Platform Web SDK实施Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=zh-Hans)的更多信息。

在您对当前Target实施和您使用的功能有了充分的技术了解后，下一步是执行[初始设置](initial-setup.md)。

>[!NOTE]
>
>我们致力于帮助您成功从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
