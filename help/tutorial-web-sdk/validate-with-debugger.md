---
title: 使用Debugger验证Web SDK实施Experience Platform
description: 了解如何使用Adobe Experience Platform Debugger验证Platform Web SDK实施。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 5%

---

# 使用Debugger验证Web SDK实施Experience Platform

了解如何使用Adobe Experience Platform Debugger验证Platform Web SDK实施。

Experience Platform调试器是适用于Chrome和Firefox浏览器的扩展，可帮助您查看在网页中实施的Adobe技术。 下载首选浏览器的版本：

* [Firefox扩展](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome扩展](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您以前从未使用过该调试器(并且此调试器与旧版Adobe Experience Cloud Debugger不同)，则可能需要观看此五分钟的概述视频：

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

在本课程中，您将使用 [Adobe Experience Cloud Debugger扩展](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) 替换 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html) 拥有您自己的资产。

此技术称为环境切换，当您稍后在自己的网站上使用标记时，此技术将非常有用。 您可以在浏览器中加载生产网站，但使用 *开发* 标记环境。 通过此功能，您可以放心地做出并验证标记更改，而不依赖于常规代码发布。 毕竟，这种将营销标记发布与常规代码发布分离的做法是客户最初使用标记的主要原因之一！

## 学习目标

在本课程结束时，您将能够使用调试器执行以下操作：

* 加载替代标记库
* 验证XDM对象是否正在按照预期的边缘网络捕获和发送数据

## 先决条件

您熟悉数据收集标记和 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}并已完成教程中以前的以下课程：

* [配置权限](configure-permissions.md)
* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [标记属性中安装的Web SDK扩展](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)
* [创建标记规则](create-tag-rule.md)


## 使用Debugger加载替代标记库

本教程使用的是 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html). 打开主页并将其加入书签。

![Luma主页](assets/validate-luma-site.png)

Experience Platform调试器具有一项酷炫的功能，允许您将现有的标记库替换为其他的标记库。 此技术对于验证非常有用，它允许我们在本教程中跳过许多实施步骤。

1. 确保已打开Luma网站，并选择Debugger扩展图标Experience Platform
1. Debugger将打开并显示硬编码实施的一些详细信息，这些信息与本教程无关（您可能需要在打开Debugger后重新加载Luma网站）
1. 确认Debugger为“**[!UICONTROL 已连接到Luma]**“ ”，然后选择“**[!UICONTROL 锁]**“ ”图标，将Debugger锁定到Luma网站。
1. 选择 **[!UICONTROL 登录]** 按钮，然后使用您的AdobeID登录Adobe Experience Cloud。
1. 现在，转到 **[!UICONTROL Experience Platform标记]** 在左侧导航中

   ![Debugger标记屏幕](assets/validate-launch-screen.png)

1. 选择 **[!UICONTROL 配置]** 选项卡
1. 右边显示 **[!UICONTROL 页面嵌入代码]**，打开 **[!UICONTROL 操作]** 下拉菜单，然后选择 **[!UICONTROL 替换]**

   ![选择“操作”>“替换”](assets/validate-switch-environment.png)

1. 自您通过身份验证后，Debugger将提取您的可用标记属性和环境。 选择 `Web SDK Course` 属性
1. 选择 `Development` 环境
1. 选择 **[!UICONTROL 应用]** 按钮

   ![选择替代标记属性](assets/validate-switch-selection.png)

1. Luma网站现在将重新加载 _使用标记属性_.

   ![已替换标记属性](assets/validate-switch-success.png)

在您继续本教程时，您将使用此技术将Luma网站映射到您自己的标记属性，以验证您的平台Web SDK实施。 当您开始在生产网站上使用标记时，可以使用此相同技术来验证更改。

## 在Debugger中验证您的实施Experience Platform

您可以使用Debugger验证Platform Web SDK实施，并查看发送到Platform Edge Network的数据：

1. 转到 **[!UICONTROL 概要]** 在左侧导航中，查看标记属性的详细信息

   ![“摘要”选项卡](assets/validate-summary.png)

1. 现在，转到 **[!UICONTROL Experience PlatformWeb SDK]** ，以查看 **[!UICONTROL 网络请求]**
1. 打开 **[!UICONTROL 事件]** 行（如果此屏幕截图显示的请求数多于您的请求数，则无需担心，其中包含将来课程的请求数，您现在可以忽略该请求）

   ![Adobe Experience Platform Web SDK请求](assets/validate-aep-screen.png)

1. 请注意，如何查看 `web.webpagedetails.pageView` 我们在 [!UICONTROL 发送事件] 操作，以及 `AEP Web SDK ExperienceEvent Mixin` 格式

   ![事件详细信息](assets/validate-event-pageViews.png)

1. 向下滚动到 `web` 对象，选择以将其打开并检查 `webPageDetails.name`, `webPageDetails.server`和 `webPageDetails.siteSection`. 它们应与主页上相应的digitalData数据层变量相匹配

   ![“网络”选项卡](assets/validate-xdm-content.png)

您还可以验证身份映射详细信息：

1. 使用凭据 `test@adobe.com`/`test` 登录 Luma 网站

1. 返回 [Luma 主页](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 打开 **[!UICONTROL Experience PlatformWeb SDK]** 部分

   ![Debugger中的Web SDK](assets/identity-debugger-websdk-dark.png)

1. 选择 **[!UICONTROL 事件]** 行以在弹出窗口中打开详细信息

   ![Debugger中的Web SDK](assets/identity-deugger-websdk-event-dark.png)

1. 搜索 **identityMap** 在弹出窗口中。 在这里，您应该看到 `lumaCrmId` 具有authenticatedState、id和primary的三个键：
   ![Debugger中的Web SDK](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)


## 使用浏览器开发工具进行验证

浏览器的Web开发人员工具中还会显示这些类型的请求详细信息 **网络** 选项卡（假定网站正在加载您的标记库）。

1. 打开浏览器的Web开发人员工具 **网络** 选项卡，然后重新加载页面。 筛选具有 `/ee` 要找到调用，请选择它，然后查看 **标题** 选项卡，以及 **负载** 选项卡

   ![“网络”选项卡](assets/validate-dev-console.png)

1. 转到 **响应** 选项卡，并记下ECID值是如何包含在响应中的。 复制此值以在下一个练习中使用该值验证用户档案信息

   ![“网络”选项卡](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   >    您可能看不到与上述屏幕截图相同的有效负载请求数量。 这种差距是因为 [设置Target](setup-target.md) 在拍摄屏幕截图时完成。 你暂时可以忽略这一区别。

现在，XDM对象在页面上触发，并且您了解如何验证数据收集，因此您可以使用Platform Web SDK设置单个Adobe应用程序。

[下一个： ](setup-experience-platform.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
