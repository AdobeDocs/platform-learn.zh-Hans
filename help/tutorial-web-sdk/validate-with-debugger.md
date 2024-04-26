---
title: 使用Experience Platform调试器验证Web SDK实施
description: 了解如何使用Adobe Experience Platform Debugger验证您的Platform Web SDK实施。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Web SDK,Tags,Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: 78df0fb4e2f2b56b829c54c08a16f860192592d1
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 使用Experience Platform调试器验证Web SDK实施

了解如何使用Adobe Experience Platform Debugger验证您的Platform Web SDK实施。

Experience Platform调试器是一个适用于Chrome和Firefox浏览器的扩展，可帮助您查看在网页中实现的Adobe技术。 下载首选浏览器的版本：

* [Firefox扩展](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome扩展](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您以前从未使用过该调试器，则可能需要观看以下时长为5分钟的概述视频：

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

在本课程中，您将使用 [Adobe Experience Cloud Debugger扩展](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) 替换 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html) 拥有自己的财产。

此技术称为环境切换，当您以后在自己的网站上使用标记时，此技术将非常有用。 它允许您在浏览器中加载生产网站，但需使用 *开发* 标记库。 此功能使您能够放心地做出并验证标记更改，而不依赖于常规代码发布。 毕竟，将营销标记发布与常规代码发布分开是客户最初使用标记的主要原因之一！

## 学习目标

在本课程结束时，您将能够使用调试器执行以下操作：

* 加载备用标记库
* 验证客户端XDM事件是否按预期捕获数据并将数据发送到PlatformEdge Network
* 启用边缘跟踪以查看由平台Edge Network发送的服务器端请求

## 先决条件

您熟悉数据收集标记和 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 并完成了本教程中以前的课程：

* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)
* [创建身份](create-identities.md)
* [创建标记规则](create-tag-rule.md)

## 使用Debugger加载备用标记库

Experience PlatformDebugger具有一项酷炫功能，允许您使用其他标记库替换现有标记库。 此技术对验证非常有用，允许我们跳过本教程中的许多实施步骤。

1. 确保您拥有 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 打开并选择Experience PlatformDebugger扩展图标
1. 调试器将打开并显示硬编码实施的一些详细信息（您可能需要在打开调试器后重新加载Luma网站）
1. 确认调试器为“**[!UICONTROL 已连接到Luma]**&quot;，如下图所示，然后选择&quot;**[!UICONTROL 锁定]**”图标将Debugger锁定到Luma网站。
1. 选择 **[!UICONTROL 登录]** 按钮并使用您的AdobeID登录Adobe Experience Cloud。
1. 现在转到 **[!UICONTROL Experience Platform标记]** 在左侧导航中

   ![Debugger标记屏幕](assets/validate-launch-screen.png)

1. 选择 **[!UICONTROL 配置]** 选项卡
1. 右边显示了 **[!UICONTROL 页面嵌入代码]**，打开 **[!UICONTROL 操作]** 下拉列表，然后选择 **[!UICONTROL 替换]**

   ![选择操作>替换](assets/validate-switch-environment.png)

1. 由于您已经过身份验证，调试器将会拉入您的可用标记属性和环境。 选择您的资产
1. 选择您的 `Development` 环境
1. 选择 **[!UICONTROL 应用]** 按钮

   ![选择备用标记属性](assets/validate-switch-selection.png)

1. Luma网站现在将重新加载 _使用您自己的标记属性_.

   ![已替换标记属性](assets/validate-switch-success.png)

在本教程的后面部分，您将使用此技术将Luma网站映射到您自己的标记资产，以验证您的Platform Web SDK实施。 在生产网站上开始使用标记时，您可以在标记的开发环境中使用同一技术来验证所做的更改。

## 使用Experience Platform调试器验证客户端网络请求

您可以使用Debugger验证从Platform Web SDK实施触发的客户端信标，以查看发送到PlatformEdge Network的数据：

1. 转到 **[!UICONTROL 摘要]** 在左侧导航中，查看标记属性的详细信息

   ![“摘要”选项卡](assets/validate-summary.png)

1. 现在转到 **[!UICONTROL Experience PlatformWeb SDK]** 在左侧导航中查看 **[!UICONTROL 网络请求]**
1. 打开 **[!UICONTROL 事件]** 行

   ![Adobe Experience Platform Web SDK请求](assets/validate-aep-screen.png)

1. 请注意您能看到的 `web.webpagedetails.pageView` 您指定的事件类型 [!UICONTROL 更新变量] 操作以及其他遵循的开箱即用变量 `AEP Web SDK ExperienceEvent` 字段组

   ![事件详细信息](assets/validate-event-pageViews.png)

1. 向下滚动到 `web` 对象，选择以将其打开并检查 `webPageDetails.name`， `webPageDetails.server`、和 `webPageDetails.siteSection`. 它们应该与对应的 `digitalData` 主页上的数据层变量

>[!TIP]
>
> 要查看和比较 `digitalData` 数据层：
>
> 1. 在Luma主页上，打开浏览器开发人员工具。 对于Chrome，选择button `F12` 在键盘上
> 1. 选择 **[!UICONTROL 控制台]** 选项卡
> 1. 输入 `digitalData` 并选择 `Enter` 以调出数据层值

![“网络”选项卡](assets/validate-xdm-content.png)

您还可以验证身份映射详细信息：

1. 使用凭据登录Luma网站 `test@adobe.com`/`test`

1. 返回 [Luma 主页](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 打开 **[!UICONTROL Experience PlatformWeb SDK]** 左侧导航中的部分

   ![Debugger中的Web SDK](assets/identity-debugger-websdk-dark.png)

1. 选择 **[!UICONTROL 事件]** 在弹出窗口中打开详细信息的行

   ![Debugger中的Web SDK](assets/identity-deugger-websdk-event-dark.png)

1. 搜索 **identityMap** 在弹出窗口中。 您应该看到 `lumaCrmId` 包含authenticatedState、id和primary的三个键：
   ![Debugger中的Web SDK](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### 使用浏览器开发工具验证客户端请求

这些类型的请求详细信息还可在浏览器的Web开发人员工具中查看 **网络** 选项卡（假设网站正在加载您的标记库）。

1. 打开浏览器的Web开发人员工具 **网络** 制表符并重新加载页面。 过滤调用 `/ee` 要查找该调用，请选择它，然后查看 **标题** 制表符，和 **有效负荷** 选项卡

   ![“网络”选项卡](assets/validate-dev-console.png)

1. 转到 **响应** 选项卡，并记下ECID值在响应中的包含方式。 复制此值，因为您将在下一个练习中使用它来验证用户档案信息

   ![“网络”选项卡](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > ECID值在网络响应中可见。 它不包括在 `identityMap` 请求的一部分，也不会以此格式存储在Cookie中。

## 使用Experience Platform调试器验证服务器端网络请求

正如您在 [配置数据流](configure-datastream.md) 课程， Platform Web SDK首先会将您的数字财产中的数据发送到PlatformEdge Network。 然后，平台Edge Network会向数据流中启用的相应服务发出其他服务器端请求。 您可以在Debugger中使用Edge Trace验证PlatformEdge Network发出的服务器端请求。

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home). -->


### 启用边缘跟踪

要启用边缘跟踪，请执行以下操作：

1. 在左侧导航中 **[!UICONTROL Experience Platform调试程序]** 选择 **[!UICONTROL 日志]**
1. 选择 **[!UICONTROL Edge]** 选项卡，然后选择 **[!UICONTROL 连接]**

   ![连接边缘跟踪](assets/analytics-debugger-edgeTrace.png)

1. 目前为空

   ![连接的边缘跟踪](assets/analytics-debugger-edge-connected.png)

1. 刷新 [Luma主页](https://luma.enablementadobe.com/) 并选中 **[!UICONTROL Experience Platform调试程序]** 同样，查看数据输入。

   ![Analytics信标边缘跟踪](assets/validate-edge-trace.png)

此时，您无法查看任何发送到Adobe应用程序的平台Edge Network请求，因为您未在数据流中启用任何请求。 在将来的课程中，您将使用Edge Trace查看用于Adobe应用程序和事件转发的传出服务器端请求。 但首先，了解用于验证平台Edge Network发出的服务器端请求的另一个工具 — Adobe Experience Platform Assurance！

[下一步： ](validate-with-assurance.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
