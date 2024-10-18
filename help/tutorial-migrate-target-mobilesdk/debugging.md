---
title: Debug — 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解如何使用Adobe Experience Platform Mobile SDK调试Adobe Target实施。
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 3%

---

# 使用Platform Mobile SDK调试Target

验证Target活动并调试Mobile SDK，以排查实施、内容交付或受众资格问题。 迁移指南的此页面说明了使用at.js调试与使用Platform Web SDK调试之间的区别。

下表总结了各种功能和对测试和调试方法的支持。

| 特征或工具 | at.js支持 | 平台Web SDK支持 |
| --- | --- | --- |
| 活动QA URL | 是 | 是 |
| `mboxDisable` URL参数 | 是 | 请参阅以下信息以了解[禁用Target功能](#disable-target-functionality) |
| `mboxDebug` URL参数 | 是 | 将`alloy_debug`参数用于类似的调试信息 |
| `mboxTrace` URL参数 | 是 | 使用Experience PlatformDebugger浏览器扩展 |
| Adobe Experience Platform Debugger扩展 | 是 | 是 |
| `alloy_debug` URL参数 | 不适用 | 是 |
| Adobe Experience Platform Assurance | 不适用 | 是 |

## Adobe Experience Platform Debugger浏览器扩展

适用于Chrome和Firefox的Adobe Experience Platform Debugger扩展可检查您的网页，并帮助您验证Adobe Experience Cloud实施。

您可以在任何网页上运行Platform Debugger，并且该扩展可以访问公共数据。 若要使用扩展访问非公共数据（如Target跟踪信息），必须通过&#x200B;**[!UICONTROL 登录]**&#x200B;链接向Experience Cloud进行身份验证。


## 使用QA URL预览Target活动

at.js和Platform Web SDK都允许您使用Target QA URL预览Target活动，并且这两种实施方法都支持相同的QA功能。

通过指示at.js或Platform Web SDK将特定Cookie写入名为`at_qa_mode`的浏览器，Target QA URL可正常工作。 此Cookie用于强制对特定活动和体验进行鉴别。

>[!CAUTION]
>
>Platform Web SDK版本2.13.0或更高版本支持Target QA模式功能。 已根据`sendEvent`调用中传递的`xdm.web.webPageDetails.URL`值启用目标QA模式。 对此值所做的任何修改（例如将所有字符变为小写），都可能会妨碍Target QA模式正常工作。

有关[Target活动QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html)的详细信息，请参阅专用指南。

## 调试Target实施

下表概述了at.js与Platform Web SDK调试策略之间的差异：

| at.js功能 | Platform Web SDK等效项 |
| --- | --- |
| **Mbox禁用** — 禁用Target的提取和渲染功能，以检查页面是否损坏，而不进行Target交互<br><br>使用URL参数加载页面： `mboxDisable=true` | 没有直接等效项。 您可以使用浏览器的开发人员工具阻止所有Platform Web SDK请求。 |
| **Mbox调试** — 记录浏览器控制台中的每个at.js操作，以帮助解决渲染问题<br><br>使用URL参数`mboxDebug=true`加载页面 | **Alloy Debug** — 记录SDK的详细操作，包括但不限于Target个性化操作。<br><br>加载包含URL参数的页面： `alloy_debug=true` <br /><br />或在开发人员控制台中执行`alloy("setDebug", { "enabled": true });` |
| **目标跟踪** — 在Target UI中生成mbox跟踪令牌后，`window.___target_trace`对象下提供了包含参与决策过程的详细信息的跟踪对象。<br><br>加载包含URL参数的页面： `mboxTrace=window&authorization={TOKEN}` | 使用Adobe Experience Platform Debugger扩展或Platform Assurance。 |

>[!NOTE]
>
>上面列出的所有at.jsAdobe Experience Platform Debugger功能都可以通过Debugging中的增强功能使用。

### 禁用Target功能

Platform Web SDK当前没有选择性地禁止Target响应的功能。 但是，可以使用浏览器的开发人员工具、各种浏览器扩展或第三方应用程序阻止Platform Web SDK请求。 例如，要使用Google Chrome阻止Platform Web SDK，请执行以下操作：

1. 右键单击页面上的任意位置，然后选择&#x200B;**Inspect**
1. 选择&#x200B;**网络**&#x200B;选项卡
1. 按字符串`//ee//`筛选，以仅查看Platform Web SDK调用
1. 重新加载页面
1. 右键单击其中一个过滤的网络请求，然后选择&#x200B;**阻止请求域**
1. 重新加载页面，并注意网络请求已被阻止
1. 完成调试后，右键单击被阻止的网络请求并选择&#x200B;**取消阻止**，或关闭“开发人员工具”面板

### 查看调试日志记录

使用`mboxDebug=true` URL参数调试at.js日志记录可显示有关每个Target请求、响应以及尝试将内容呈现到页面的详细信息。 Platform Web SDK具有类似的使用`alloy_debug=true` URL参数的调试日志记录。

| 信息已记录 | at.js (`mboxDebug=true`) | 平台Web SDK (`alloy_debug=true`) |
| --- | --- | --- |
| 用于筛选的日志记录前缀 | `AT:` | `[alloy]` |
| 页面加载请求详细信息 | 是 | 是 |
| Mbox或范围请求详细信息 | 是 | 是 |
| 请求状态 | 是 | 是 |
| 响应详细信息 | 是 | 是 |
| 渲染状态 | 成功和错误 | 仅错误 |
| 呈现详细信息 | 是 | 是 |

>[!NOTE]
>
>at.js和Platform Web SDK的调试日志提供了类似级别的详细信息，但存在一个显着例外，即Web SDK仅通知由于选择器无效而出现的渲染错误。 调试日志记录当前未确认渲染成功。

### 查看Target跟踪

Target跟踪可提供有关活动资格和访客的Target配置文件的详细信息。 由于Target跟踪包含不公开的信息，因此查看这些跟踪需要授权令牌或在Adobe Experience Platform Debugger浏览器扩展窗口中进行身份验证。

| 目标跟踪方法 | at.js | 平台Web SDK |
| --- | --- | --- |
| `mboxTrace` URL参数 | 是 | 否 |
| Adobe Experience Platform Debugger浏览器扩展 | 是 | 是 |
| Adobe Experience Platform Assurance | 否 | 是 |



<!--![How to view Target traces with Adobe Experience Platform Debugger](assets/target-trace-debugger.png){zoomable="yes"}-->

选择&#x200B;**[!UICONTROL 视图]**&#x200B;后，将显示一个叠加图，允许您查看与请求相关的以下信息：

- 匹配的活动
- 不匹配的活动
- 请求详细信息
- 配置文件快照

有关Target跟踪的详细信息，请参阅有关[调试Target内容投放](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html)的专用指南。

### 使用保障进行故障排除

可以在Adobe Experience Platform Debugger浏览器扩展和Assurance应用程序（以前称为Project Griffon）中查看Target跟踪信息。 要在Assurance中查看Target跟踪，请执行以下操作：

1. 如上所述，打开Adobe Experience Platform Debugger浏览器扩展并连接远程调试会话
1. 选择带有您的会话名称的链接，该链接位于调试日志上方
1. 平台保证会加载并在数据流中为您的实施配置的所有Adobe应用程序显示详细的日志记录
1. 按`adobe.target`筛选日志
1. 选择类型为`com.adobe.target.trace`的日志条目
1. 展开有效负载的详细信息并查看`context > targetTrace`下的信息

<!--![How to view Target traces with Assurance](assets/target-trace-assurance.png){zoomable="yes"}-->

## 检查网络请求和响应

Platform Web SDK `sendEvent`调用的请求有效负载和响应与at.js不同。 使用浏览器的开发人员工具检查网络调用时，以下概要应该帮助您了解请求和响应的结构。

### 内容请求有效负荷

<!--![Target specific elements of the Platform Web SDK payload](assets/target-payload.png){zoomable="yes"}-->

- 配置文件、实体和其他非mbox参数在`data.__adobe.target`下的事件数组中传递
- 决策范围位于`query.personalization.decisionScopes`下的事件数组中
- 映射到下游mbox参数的XDM数据位于`xdm`下的事件数组中

### 内容响应正文

<!--![Target specific elements of the Platform Web SDK response body](assets/target-response.png){zoomable="yes"}-->

- Platform Web SDK返回`handle`对象下所有Adobe应用程序的操作
- `personalization:decisions`操作表示来自Target或offer decisioning的响应
- 目标建议以数组形式呈现，每个建议都具有以`AT:`为前缀的唯一建议ID
- 决策范围和活动详细信息位于建议数组中
- 选件详细信息位于`data`下的`items`数组中
- 响应令牌位于`meta`下的`items`数组中

### 建议事件有效负载

<!--![Target proposition event example](assets/target-proposition-event.png){zoomable="yes"}-->

- Target特定的SDK事件为展示的`decisioning.propositionDisplay`或交互的`decisioning.propositionInteract`，例如点击
- 建议事件的详细信息位于`xdm._experience.decisioning`下的事件数组中
- 显示或交互事件的建议ID应当与从Target返回的内容的建议ID匹配


恭喜，您已到达本教程的结尾！ 祝您顺利将Adobe Target实施迁移到Web SDK！

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
