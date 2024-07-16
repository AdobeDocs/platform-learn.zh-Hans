---
title: 使用Adobe Experience Cloud Debugger切换标记环境
description: 了解如何使用Experience Cloud Debugger加载其他标记嵌入代码。 本课程是“在网站中实施Experience Cloud”教程的一部分。
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 21%

---

# 使用Experience Cloud Debugger切换标记环境

在本课程中，您将使用[Adobe Experience Platform Debugger扩展](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)将[Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html)上硬编码的标记属性替换为您自己的属性。

此技术称为环境切换，当您以后在自己的网站上使用标记时，此技术将非常有用。 您可以在浏览器中加载生产网站，但需要您的&#x200B;*开发*&#x200B;标记环境。 这使您能够放心地做出并验证标记更改，而不依赖于常规代码发布。  毕竟，将营销标记发布与常规代码发布分开是客户最初使用标记的主要原因之一！

>[!NOTE]
>
>Adobe Experience Platform Launch正在作为一套数据收集技术集成到Adobe Experience Platform中。 在使用此内容时，您应该了解的界面中推出了几项术语更改：
>
> * platform launch（客户端）现在为&#x200B;**[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch服务器端现在为&#x200B;**[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge配置现在为&#x200B;**[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

## 学习目标

在本课程结束后，您将能够：

* 使用Debugger加载替代标记环境
* 使用Debugger验证是否已加载替代标记环境

## 获取开发环境的 URL

1. 在标记属性中，打开`Environments`页面

1. 在&#x200B;**[!UICONTROL Development]**&#x200B;行中，单击“安装”图标![安装图标](images/launch-installIcon.png)以打开模式窗口

1. 单击复制图标 ![复制图标](images/launch-copyIcon.png) 以将嵌入代码复制到剪贴板

1. 单击&#x200B;**[!UICONTROL 关闭]**&#x200B;以关闭该模式窗口

   ![安装图标](images/launch-copyInstallCode.png)

## 替换Luma演示网站上的标记URL

1. 在您的 Chrome 浏览器中打开 [Luma 演示网站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 通过单击![Experience Platform器图标](images/icon-debugger.png)图标，打开[调试器扩展](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

   ![单击 Debugger 图标](images/switchEnvironments-openDebugger.png)

1. 请注意，当前实施的标记属性将显示在“摘要”选项卡中

   Debugger](images/switchEnvironments-debuggerOnWeRetail-prod.png)中显示的![标记环境

1. 转到“工具”选项卡
1. 滚动到&#x200B;**[!UICONTROL 替换Launch嵌入代码]**&#x200B;部分
1. 确保Debugger后面显示Luma网站的Chrome选项卡成为焦点（不是显示本教程的选项卡，也不是显示数据收集界面的选项卡）。  将剪贴板中的嵌入代码粘贴到输入字段中
1. 打开“跨luma.enablementadobe.com应用”功能，以便Luma网站上的所有页面都将映射到您的标记属性
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;按钮

   Debugger](images/switchEnvironments-debugger-save.png)中显示的![标记环境

1. 重新加载 Luma 网站并检查 Debugger 的“摘要”选项卡。在 Launch 部分下，现在您应会看到开发资产正在使用中。请确认该资产的名称与您的资产名称匹配，并且环境显示为“development”。

   Debugger](images/switchEnvironments-debuggerOnWeRetail.png)中显示的![标记环境

>[!NOTE]
>
>每当您返回Luma网站时，Debugger都将保存此配置并替换标记嵌入代码。 这不会影响您在其他打开的标签页中访问的其他网站。要阻止Debugger替换嵌入代码，请在Debugger的“工具”选项卡中单击嵌入代码旁边的&#x200B;**[!UICONTROL 删除]**&#x200B;按钮。

在本教程的后面部分，您将使用此技术将Luma网站映射到您自己的标记资产，以验证标记实施。 在生产网站上开始使用标记时，您可以使用该同一技术验证所做的更改。

[下一课程“添加Adobe Experience Platform Identity Service”>](id-service.md)
