---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 客户端Web数据收集
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 客户端Web数据收集
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: c4ebca8d-93e0-4056-8553-c0d7e342beca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# 1.4客户端Web数据收集

## 1.4.1验证请求中的数据

### 安装Adobe Experience Platform Debugger

Experience Platform调试器是适用于Chrome和Firefox浏览器的扩展，可帮助您查看在网页中实施的Adobe技术。 下载首选浏览器的版本：

- [Firefox扩展](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/)

- [Chrome扩展](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您以前从未使用过Debugger — 此调试器与之前的Adobe Experience Cloud Debugger不同 — 您可能需要观看此五分钟概述视频：

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

鉴于您将以隐身模式加载演示网站，因此需要确保Experience Platform调试器也可以以隐身模式使用。 要执行此操作，请转到 **chrome://extensions** 在浏览器中，打开Experience Platform调试器扩展。

确认已启用以下2个设置：

- 开发人员模式
- 允许隐身

![EXP新闻主页](./images/ext1.png)

### 打开演示网站

转到 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](../module0/images/web8.png)

在 **Screens** 页面，单击 **运行**.

![DSN](./images/web2.png)

然后，您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../module0/images/web3.png)

打开新的隐身浏览器窗口。

![DSN](../module0/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../module0/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../module0/images/web6.png)

然后，您将在无痕浏览器窗口中看到您的网站已加载。 对于每个演示，您需要使用全新的、隐身的浏览器窗口来加载演示网站URL。

![DSN](../module0/images/web7.png)

### 使用Experience Platform调试器查看转到Edge的调用

确保您打开了演示网站，然后单击Debugger扩展图标Experience Platform。

![EXP新闻主页](./images/ext2.png)

此时将打开Debugger，并显示在您的Adobe Experience Platform数据收集资产中创建的实施的详细信息。 请记住，您正在调试刚刚编辑的扩展和规则。

单击 **[!UICONTROL 登录]** 按钮进行身份验证。 如果已在Adobe Experience Platform数据收集界面中打开浏览器选项卡，则身份验证步骤将自动执行，您无需再次输入用户名和密码。

![AEP Debugger](./images/validate2.png)

点击演示网站上的重新加载按钮，将调试器连接到该特定选项卡。

![AEP Debugger](./images/validate2a.png)

确认Debugger为 **[!UICONTROL 已连接到主页]** 如上图所示，然后单击 **[!UICONTROL 锁]** 图标将Debugger锁定到演示网站。 如果您不这样做，Debugger将不断切换以显示所关注的任何浏览器选项卡的实施详细信息，这可能会造成混淆。

![AEP Debugger](./images/validate3.png)

接下来，转到演示网站上的任何页面，例如 **男** 类别页面。

![AEP Debugger AEP Web SDK扩展](./images/validate4.png)

现在，单击 **[!UICONTROL Experience PlatformWeb SDK]** 在左侧导航中，要查看 **[!UICONTROL 网络请求]**.

每个请求都包含一个 **[!UICONTROL 事件]** 行。

![AEP Debugger AEP Web SDK扩展](./images/validate5.png)

单击以打开 **[!UICONTROL 事件]** 行。 请注意如何查看 **web.webpagedetails.pageViews** 事件，以及其他开箱即用的变量， **Web SDK ExperienceEvent XDM** 格式。

![事件值](./images/validate8.png)

这些类型的请求详细信息也显示在“网络”选项卡中。 筛选具有 **交互** 来查找由Web SDK发送的请求。 您可以在请求有效负载标头中找到XDM有效负载的所有详细信息：

![“网络”选项卡](./images/validate9.png)

下一步： [1.5实施Adobe Analytics和Adobe Audience Manager](./ex5.md)

[返回到模块1](./data-ingestion-launch-web-sdk.md)

[返回到所有模块](./../../overview.md)
