---
title: 考虑将供应商标记移动到事件转发
description: 了解如何评估服务器端数据分发的客户端供应商标记。
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
jira: KT-9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# 考虑将客户端供应商标记移动到事件转发

考虑将客户端供应商标记从浏览器和设备移动到服务器有几个令人信服的原因。 在本文中，我们将讨论如何评估客户端供应商标记是否可能将其移动到事件转发属性。

仅当您考虑删除客户端供应商标记并在事件转发属性中将其替换为服务器端数据分发时，才需要此评估。 本文假设您熟悉 [数据收集](https://experienceleague.adobe.com/docs/data-collection.html)、和 [事件转发](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

浏览器供应商正在改变他们对待第三方Cookie的方式。 广告和营销供应商和技术通常需要使用许多客户端标记。 这些挑战只是我们的客户增加服务器端数据分发的两个令人信服的原因。

>[!NOTE]
>
>`Tag` 在本文中，是指当访客与网站或应用程序进行交互时，在浏览器或设备中用于收集数据的客户端代码，通常是来自供应商的JavaScript。 `Website` 或 `site` 此处是指适用于移动设备的网站、Web应用程序或应用程序。 用于这些目的的“标记”通常也称为像素。

## 用例和数据 {#use-cases-data}

第一步是定义使用客户端供应商标记实施的用例。 例如，以Facebook (Meta)像素为例。 将其从我们的站点移至 [facebook转化API](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) 使用事件转发扩展意味着首先记录特定用例。

对于当前客户端供应商代码：

- 哪些特定事件和其他数据点会公开并传递到客户端标记？
- 数据传输何时发生、在何处发生？

创建数据和事件序列的列表、电子表格、图表或其他记录以记录此评估很有帮助 — 即使它仅供您自己使用。 确保包含数据源标签 — 数据源来自何处？ 目标 — 它去哪里？ 以及转换 — 在源和目标之间会发生什么情况？

在我们的示例中，当访客在查看Facebook广告后与我们的网站进行交互时，我们使用Facebook像素跟踪转化。 他们亦可在其他社交平台上观看相关广告后与我们的网站互动。 要在Facebook广告工具和报表中查看这些转化，必须将数据发送到Facebook。 此数据可能包括下载、注册、点赞或购买等转化事件。

### 数据 {#data}

对于现有的客户端标记，当它在我们的网站上运行或执行时，用例中的数据会发生什么情况？ 我们是否可以在客户端捕获所需的数据，而无需供应商标记，以便将其发送到事件转发？ 使用时 [标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 标记管理系统或其他标记管理系统中，大多数访客交互数据可用于收集和分发。 但是，在我们的用例中需要的数据是否可以在需要时、在需要的地方、以需要的格式提供 — 而不需要客户端供应商标记？ 下面是一些需要考虑的其他数据问题：

- 每个事件是否需要供应商用户ID？
- 如果是这样，如何在不使用客户端标记的情况下收集或生成它？
- 供应商是否在运行时明确要求客户端代码？
- 还需要哪些其他数据？ 这些数据将来自何处？

对于任何特定用例，大多数客户端供应商标记不需要许多数据点，但在这些评估期间记下用例和所需数据会很有帮助。

## 供应商API {#vendor-apis}

现在，我们知道了要实施的特定用例、所需的数据以及从源到目标的事件顺序。 为了确定用例是否适合事件转发，我们现在可以调查供应商API详细信息。

>[!IMPORTANT]
>
>虽然许多供应商正在启用API以进行服务器到服务器传输，但也有许多供应商当前没有适合这些用途的API。

### 调查API {#investigate-apis}

以下是调查供应商API端点可以执行的一些步骤。

供应商是否有专为事件数据的服务器到服务器传输而设计的API？ 首先，找出这些特定API端点的要求：

- 是否存在API端点以发送所需数据？ 要查找支持您的用例的端点，请查看供应商的开发人员或API文档。
- 是允许流式传输事件数据，还是仅允许批处理数据？
- 它们支持哪些身份验证方法？ 令牌、HTTP、OAuth客户端凭据版本还是其他？ 参见 [此处](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) 用于事件转发支持的方法。
- 其API的刷新偏移量是多少？ 此限制是否与事件转发最小值兼容？ 详细信息 [此处](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- 它们需要相关端点的哪些数据？
- 他们是否需要每次调用端点时都使用特定于供应商的用户标识符？
- 如果它们需要该标识符，可在何处以及如何生成或捕获该标识符，而无需客户端代码？

换句话说：

- 供应商是否提供用例所需的API端点？
- 它们是否有兼容的事件转发身份验证方法？
- 我们是否可以访问事件转发实施所需的所有数据（从客户端或从其他API调用）？

如果我们可以对这些问题回答“是”，则标记可能是很好的候选项，可以在事件转发属性中从客户端移动到我们的服务器。

如果供应商没有支持用例的API端点，那么很显然，供应商标记不适合使用事件转发来代替客户端供应商标记。

如果他们具有API，但同时要求在每个API调用中具有一些独特访客或用户ID，该怎么办？ 如果网站上未运行供应商客户端代码（标记），我们如何访问该ID？

一些供应商在没有第三方Cookie的情况下正在针对新世界更改其系统。 这些更改包括使用替代唯一标识符，如 [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) 或其他 [客户生成的Id](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). 如果供应商允许客户生成的ID，我们既可以使用Web或Mobile SDK将其从客户端发送到Platform Edge Network，也可以通过事件转发中的API调用获取该ID。 当我们在事件转发规则中向供应商发送数据时，我们只是根据需要包含该标识符。

如果供应商需要只能由其自己的客户端标记生成或访问的数据（例如，特定于供应商的唯一ID），则该供应商标记可能不是一个合适的候选移动对象。 _建议不要尝试对客户端标记进行逆向工程，不要考虑在不使用适当API的情况下将该数据收集移动到事件转发。_

此 [Adobe Experience Platform Cloud连接器](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) 扩展可以根据需要向具有用于服务器到服务器事件数据传输的适当API的供应商发出HTTP请求。 虽然供应商特定的扩展很好，并且更多扩展正在积极开发，但我们现在可以使用Cloud Connector扩展实施事件转发规则，而无需等待其他供应商扩展。

## 工具 {#tools}

借助以下工具，更容易调查和测试供应商API端点 [Postman](https://www.postman.com/)或文本编辑器扩展，如Visual Studio Code [Thunder客户端](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)，或 [HTTP客户端](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## 后续步骤 {#next-steps}

本文提供了一系列步骤来评估供应商客户端标记，并可能将其移动到事件转发属性的服务器端。 有关相关主题的更多信息，请参阅以下链接：

- [标记管理](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 在Adobe Experience Platform中
- [事件转发](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) 用于服务器端处理
- [术语更新](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) 在数据收集中
