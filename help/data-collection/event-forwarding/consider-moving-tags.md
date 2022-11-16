---
title: 考虑将供应商标记移动到事件转发
description: 了解如何评估客户端供应商标记以进行服务器端数据分发。
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
kt: 9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# 考虑将客户端供应商标记移动到事件转发

考虑将客户端供应商标签从浏览器和设备中移出并移到服务器上，有几个令人信服的理由。 在本文中，我们将讨论如何评估客户端供应商标记是否可能将其移动到事件转发属性。

仅当您考虑删除客户端供应商标记并将其替换为事件转发属性中的服务器端数据分发时，才需要进行此评估。 本文假定您熟悉 [数据收集](https://experienceleague.adobe.com/docs/data-collection.html)和 [事件转发](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

浏览器供应商正在改变对待第三方Cookie的方式。 广告和营销供应商和技术通常需要使用许多客户端标记。 这些难题只是我们的客户添加服务器端数据分发的两个迫切原因。

>[!NOTE]
>
>`Tag` 本文中指客户端代码，通常是来自供应商的JavaScript，该供应商用于在浏览器或设备中收集数据，而访客与网站或应用程序进行交互。 `Website` 或 `site` 此处指网站、Web应用程序或移动设备应用程序。 用于这些目的的“标记”通常也称为像素。

## 用例和数据 {#use-cases-data}

第一步是定义通过客户端供应商标记实施的用例。 例如，考虑Facebook(Meta)像素。 将其从我们的网站移动到 [Facebook转化API](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) 使用事件转发扩展意味着首先记录特定用例。

对于当前客户端供应商代码：

- 哪些特定事件和其他数据点会公开并传递到客户端标记？
- 数据传输何时以及何处发生？

创建数据和事件序列的列表、电子表格、图表或其他记录以记录此评估非常有用，即使这仅供您自己使用。 确保包含数据源的标签 — 数据源来自何处？ 目标 — 它会去哪里？ 和转换 — 在源和目标之间会发生什么情况？

在我们的示例中，我们正在跟踪访客在查看Facebook广告后与我们的网站进行交互时，与Facebook像素的转化。 在其他社交平台上查看相关广告后，用户也可以与我们的网站进行交互。 要在Facebook广告工具和报表中查看这些转化，必需数据必须到达Facebook。 此数据可能包括下载、注册、称赞或购买等转化事件。

### 数据 {#data}

使用现有的客户端标记，当该标记在我们的网站上运行或执行时，用于我们用例的数据会发生什么情况？ 我们是否可以在客户端中捕获所需的数据（不带供应商标记），以便将其发送到事件转发？ 使用 [标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 或其他标签管理系统中，大多数访客交互数据都可用于收集和分发。 但是，在我们需要时，我们需要的用例数据是否可用，在我们需要时，在我们需要它的位置，以我们需要的格式提供？ 以下是一些需要考虑的进一步数据问题：

- 每个事件是否需要供应商用户ID?
- 如果是，则如何在没有客户端标记的情况下收集或生成该标记？
- 供应商在运行时是否特别要求其客户端代码？
- 需要哪些其他数据？ 这些数据将从何而来？

大多数客户端供应商标记对于任何特定用例不需要多个数据点，但在这些评估期间记录用例和所需数据会很有帮助。

## 供应商API {#vendor-apis}

现在，我们知道要实施的具体用例、所需数据以及从源到目标的事件序列。 为了确定用例是否适合事件转发，我们现在可以调查供应商API详细信息。

>[!IMPORTANT]
>
>虽然许多供应商都在为服务器到服务器传输启用API，但还有许多供应商当前没有适合这些目的的API。

### 调查API {#investigate-apis}

以下是我们可以采取的一些步骤来调查供应商API端点。

供应商是否有专为事件数据的服务器到服务器传输而设计的API? 首先，找到这些特定API端点的要求：

- API端点是否存在以发送所需数据？ 要查找支持您的用例的端点，请参阅供应商的开发人员或API文档。
- 它们是允许流事件数据，还是仅允许批量数据？
- 它们支持哪些身份验证方法？ 令牌、HTTP、OAuth客户端凭据版本，还是其他？ 请参阅 [此处](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) 用于事件转发支持的方法。
- 其API的刷新偏移是多少？ 该限制是否与事件转发最小值兼容？ 详细信息 [此处](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- 他们需要哪些数据来获取相关端点？
- 每次调用端点时，是否需要特定于供应商的用户标识符？
- 如果他们需要该标识符，在何处以及如何生成或捕获该标识符，则无需客户端代码？

换句话说：

- 供应商是否提供我们的用例所需的API端点？
- 他们是否具有用于事件转发的兼容身份验证方法？
- 我们是否可以访问事件转发实施所需的所有数据（从客户端或其他API调用）？

如果我们能够回答这些问题，则标记可能是事件转发属性中从客户端移动到服务器的好候选项。

如果供应商没有支持我们用例的API端点，则显然该供应商标记不是使用事件转发代替客户端供应商标记的好候选者。

如果他们具有API，但同时在每次API调用中都需要一些独特访客或用户ID，该怎么办？ 如果网站上未运行供应商客户端代码（标记），我们如何访问该ID?

一些供应商正在在没有第三方Cookie的情况下为新世界更改其系统。 这些更改包括使用替代的唯一标识符，如 [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) 或其他 [客户生成的ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). 如果供应商允许客户生成的ID，我们可以通过Web SDK或Mobile SDK将其从客户端发送到Platform Edge Network，或者在事件转发中通过API调用获取该ID。 在事件转发规则中向该供应商发送数据时，我们只需根据需要包含该标识符即可。

如果供应商需要只能由其自己的客户端标记生成或访问的数据（例如，与供应商特定的唯一ID一样），则该供应商标记可能不是移动的好候选项。 _不鼓励尝试通过在没有适当API的情况下将数据收集移动到事件转发的想法来逆向设计客户端标记。_

的 [Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) 扩展可以根据需要与拥有适当API的供应商一起发出HTTP请求，以进行服务器到服务器事件数据传输。 虽然特定于供应商的扩展非常好，并且更多扩展当前处于活动开发状态，但我们现在可以使用Cloud Connector扩展实施事件转发规则，而无需等待其他供应商扩展。

## 工具 {#tools}

使用诸如 [Postman](https://www.postman.com/)，或文本编辑器扩展（如Visual Studio Code） [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)或 [HTTP客户端](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## 后续步骤 {#next-steps}

本文提供了一系列步骤来评估供应商客户端标记，并可能在事件转发属性中将其移至服务器端。 有关相关主题的更多信息，请参阅以下链接：

- [标签管理](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 在Adobe Experience Platform
- [事件转发](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) 用于服务器端处理
- [术语更新](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) 在数据收集中
