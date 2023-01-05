---
title: 调试 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Adobe Experience Platform Web SDK调试Adobe Target实施。 主题包括调试选项、浏览器扩展，以及at.js和Platform Web SDK之间的差异。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 3%

---

# 使用平台Web SDK调试Target

验证Target活动并调试Web SDK以解决实施、内容交付或受众鉴别问题。 迁移指南的本页介绍了使用at.js进行调试与使用Platform Web SDK进行调试之间的差异。

下表概述了测试和调试方法的功能和支持。

| 功能或工具 | at.js支持 | 平台Web SDK支持 |
| --- | --- | --- |
| 活动QA URL | 是 | 是 |
| `mboxDisable` URL parameter | 是 | 请参阅下面的信息以 [禁用Target功能](#disable-target-functionality) |
| `mboxDebug` URL parameter | 是 | 使用 `alloy_debug` 类似调试信息的参数 |
| `mboxTrace` URL parameter | 是 | 使用Experience Platform调试器浏览器扩展 |
| Adobe Experience Platform Debugger扩展 | 是 | 是 |
| `alloy_debug` URL parameter | 不适用 | 是 |
| Adobe Experience Platform保障 | 不适用 | 是 |

## Adobe Experience Platform Debugger浏览器扩展

适用于Chrome和Firefox的Adobe Experience Platform Debugger扩展可检查您的网页，并帮助您验证Adobe Experience Cloud实施。

您可以在任何网页上运行Platform Debugger，并且该扩展有权访问公共数据。 要使用扩展（如Target跟踪信息）访问非公共数据，您必须通过验证以Experience Cloud **[!UICONTROL 登录]** 链接。

### 获取并安装Adobe Experience Platform Debugger

可以在Google Chrome或Mozilla Firefox浏览器中安装Adobe Experience Platform Debugger。 请按照以下相应链接在首选浏览器上安装扩展：

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
- [Firefox](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/)

安装Chrome扩展程序或Firefox加载项后，会显示一个图标(![](assets/start-icon.jpg))。 选择此图标以打开扩展。

有关 [Adobe Experience Platform Debugger扩展](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) 以及如何调试所有AdobeWeb应用程序。

## 使用QA URL预览Target活动

at.js和Platform Web SDK都允许您使用Target QA URL预览Target活动，并且两种实施方法都支持相同的QA功能。

Target QA URL的工作方式是指示at.js或Platform Web SDK向名为 `at_qa_mode`. 此Cookie用于强制对特定活动和体验进行鉴别。

>[!CAUTION]
>
>Platform Web SDK版本2.13.0或更高版本支持Target QA模式功能。 Target QA模式基于 `xdm.web.webPageDetails.URL` 传递的值 `sendEvent` 呼叫。 对此值所做的任何修改（如将所有字符都小写）都可能会阻止Target QA模式正常工作。

有关 [Target活动QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## 调试Target实施

下表概述了at.js和Platform Web SDK调试策略之间的差异：

| at.js功能 | 平台Web SDK等效项 |
| --- | --- |
| **Mbox禁用**  — 禁用Target的获取和渲染功能，以检查在没有Target交互的情况下页面是否已损坏<br><br>加载包含URL参数的页面： `mboxDisable=true` | 没有直接对等项。 您可以使用浏览器的开发人员工具阻止所有平台Web SDK请求。 |
| **Mbox调试**  — 在浏览器控制台中记录每个at.js操作，以帮助解决渲染问题<br><br>加载包含URL参数的页面： `mboxDebug=true` | **Alloy调试**  — 记录SDK的详细操作，包括但不限于Target个性化操作。<br><br>加载包含URL参数的页面： `alloy_debug=true`  <br /><br />或执行 `alloy("setDebug", { "enabled": true });` 在开发人员控制台中 |
| **目标跟踪**  — 通过在Target UI中生成的mbox跟踪令牌，可在 `window.___target_trace` 对象。<br><br>加载包含URL参数的页面： `mboxTrace=window&authorization={TOKEN}` | 使用Adobe Experience Platform Debugger扩展或平台保证。 |

>[!NOTE]
>
>上面列出的所有at.js调试功能均可在Adobe Experience Platform Debugger中通过增强功能使用。

### 禁用Target功能

Platform Web SDK当前没有可选择性禁止Target响应的功能。 但是，您可以使用浏览器的开发人员工具、各种浏览器扩展或第三方应用程序来禁止Platform Web SDK请求。 例如，要使用Google Chrome阻止Platform Web SDK，请执行以下操作：

1. 右键单击页面上的任意位置，然后选择 **Inspect**
1. 选择 **网络** 选项卡
1. 按字符串过滤 `//ee//` 以仅查看平台Web SDK调用
1. 重新加载页面
1. 右键单击其中一个过滤的网络请求，然后选择 **阻止请求域**
1. 重新加载页面，并注意到网络请求被阻止
1. 调试完成后，右键单击被阻止的网络请求并选择 **取消阻止**，或关闭“开发人员工具”面板

### 查看调试日志记录

使用 `mboxDebug=true` URL参数显示有关每个Target请求、响应和尝试向页面渲染内容的详细信息。 Platform Web SDK具有类似的调试日志记录(使用 `alloy_debug=true` URL参数。

| 已记录的信息 | at.js (`mboxDebug=true`) | 平台Web SDK(`alloy_debug=true`) |
| --- | --- | --- |
| 用于筛选的日志记录前缀 | `AT:` | `[alloy]` |
| 页面加载请求详细信息 | 是 | 是 |
| Mbox或范围请求详细信息 | 是 | 是 |
| 请求状态 | 是 | 是 |
| 响应详细信息 | 是 | 是 |
| 呈现状态 | 成功和错误 | 仅错误 |
| 渲染详细信息 | 是 | 是 |

>[!NOTE]
>
>at.js和Platform Web SDK的调试日志提供类似级别的详细信息，但有一个显着的例外是，Web SDK仅会通知由于无效选择器而出现渲染错误。 调试日志记录当前不确认渲染成功。

### 查看Target跟踪

Target跟踪提供有关活动资格和访客Target配置文件的详细信息。 由于Target跟踪包含的信息不是公开的，因此查看这些跟踪需要授权令牌或在Adobe Experience Platform Debugger浏览器扩展窗口中进行身份验证。

| 目标跟踪方法 | at.js | 平台Web SDK |
| --- | --- | --- |
| `mboxTrace` URL parameter | 是 | 否 |
| Adobe Experience Platform Debugger浏览器扩展 | 是 | 是 |
| Adobe Experience Platform保障 | 否 | 是 |


要使用Adobe Experience Platform Debugger查看Platform Web SDK Target跟踪，请执行以下操作：

1. 导航到您网站上已通过Platform Web SDK实施Target的页面
1. 选择图标(![](assets/start-icon.jpg))
1. 选择 **[!UICONTROL 登录]** 链接
1. 使用Adobe Experience Cloud登录名进行身份验证
1. 选择 **[!UICONTROL 日志]** 选项卡
1. 选择 **[!UICONTROL Edge]** 选项卡
1. （可选）为调试会话提供一个名称并单击 **[!UICONTROL 连接]** 按钮
1. 重新加载页面，日志中应填充有关边缘网络交互的详细信息
1. 在描述中重点关注以“目标跟踪”开头的日志条目，然后选择 **[!UICONTROL 查看]** 查看Target跟踪详细信息

![如何使用Adobe Experience Platform Debugger查看Target跟踪](assets/target-trace-debugger.png)

选择后 **[!UICONTROL 查看]**，将显示一个叠加图，允许您查看与请求相关的以下信息：

- 匹配的活动
- 无与伦比的活动
- 请求详细信息
- 配置文件快照

请参阅有关 [调试Target内容交付](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html) 以了解有关Target跟踪的更多信息。

### 疑难解答和保证

可以在Adobe Experience Platform Debugger浏览器扩展和Assurance应用程序（以前称为Project Griffon）中查看Target跟踪信息。 要在“保证”中查看Target跟踪，请执行以下操作：

1. 如上所述，打开Adobe Experience Platform Debugger浏览器扩展并连接远程调试会话
1. 在调试日志上方选择会话名称的链接
1. 平台保障加载并显示在您的实施的数据流中配置的所有Adobe应用程序的详细日志记录
1. 日志过滤依据 `adobe.target`
1. 选择类型为的日志条目 `com.adobe.target.trace`
1. 展开有效负载的详细信息，并查看 `context > targetTrace`

![如何确保查看Target跟踪](assets/target-trace-assurance.png)

## 检查网络请求和响应

Platform Web SDK的请求负载和响应 `sendEvent` 调用与at.js有所不同。 以下大纲应有助于您在使用浏览器的开发人员工具检查网络调用时了解请求和响应的结构。

### 内容请求负载

![定位平台Web SDK有效负载的特定元素](assets/target-payload.png)

- 配置文件、实体和其他非mbox参数将在事件数组中的 `data.__adobe.target`
- 决策范围位于事件数组下 `query.personalization.decisionScopes`
- 映射到下游mbox参数的XDM数据位于事件数组中的 `xdm`

### 内容响应正文

![定位平台Web SDK响应正文的特定元素](assets/target-response.png)

- Platform Web SDK会返回 `handle` 对象
- 的 `personalization:decisions` 操作表示来自Target或offer decisioning的响应
- 目标命题以数组形式呈现，每个命题ID带有前缀的唯一命题ID `AT:`
- 决策范围和活动详细信息位于命题数组内
- 选件详细信息位于 `items` 数组 `data`
- 响应令牌位于 `items` 数组 `meta`

### 建议事件有效负载

![Target建议事件示例](assets/target-proposition-event.png)

- Target特定SDK事件包括 `decisioning.propositionDisplay` 展示或 `decisioning.propositionInteract` ，例如点击
- 建议事件的详细信息位于 `xdm._experience.decisioning`
- 展示或交互事件的命题ID应与从Target返回的内容的命题ID匹配


恭喜，您已到教程的结尾！ 祝您将Adobe Target实施迁移到Web SDK!

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
