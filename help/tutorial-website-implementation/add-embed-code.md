---
title: 添加嵌入代码
description: 了解如何获取标记资产的嵌入代码并在您的网站中实施它们。 本课程是“在网站中实施Experience Cloud”教程的一部分。
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 42%

---

# 添加嵌入代码

在本课程中，您将实施标记资产的开发环境的异步嵌入代码。 在此过程中，您将了解标记的两个主要概念：环境和嵌入代码。


>[!WARNING]
>
> 本教程中使用的Luma网站预计将在2026年2月16日这一周内被替换。 作为本教程的一部分完成的工作可能不适用于新网站。

>[!NOTE]
>
>Adobe Experience Platform Launch正在作为一套数据收集技术集成到Adobe Experience Platform中。 在使用此内容时，您应该了解的界面中推出了几项术语更改：
>
> * Platform Launch（客户端）现在为&#x200B;**[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans)**
> * Platform Launch服务器端现在为&#x200B;**[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=zh-Hans)**
> * Edge配置现在为&#x200B;**[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=zh-Hans)**

## 学习目标

在本课程结束后，您将能够：

* 获取标记属性的嵌入代码
* 了解开发、暂存和生产环境之间的差异
* 将标记嵌入代码添加到HTML文档
* 解释在html文档的`<head>`中标记嵌入代码相对于其他代码的最佳位置

## 复制嵌入代码

嵌入代码是您放置在网页上的`<script>`标记，用于加载和执行您在标记中构建的逻辑。 如果异步加载库，则浏览器将继续加载页面，检索标记库，然后并行执行该库。 在这种情况下，将只有一个嵌入代码，即放置在 `<head>` 中的代码。（如果同步部署标记，则将有两个嵌入代码，一个是放置在`<head>`中的代码，另一个是放置在`</body>`之前的代码）。

在属性Overview屏幕中，单击左侧导航栏中的&#x200B;**[!UICONTROL Environments]**&#x200B;以转到环境页面。 请注意，已经为您预先创建了开发、暂存和生产环境。

![单击顶部导航中的 Environments](images/launch-environments.png)

开发、暂存和生产环境对应于代码开发和发布过程中的典型环境。首先，由开发人员在开发环境中编写代码。完成工作后，开发人员会将代码发送到暂存环境，供 QA 和其他团队审查。QA 和其他团队对代码满意后，代码会被发布到生产环境，这是面向公众的环境，即访客在访问您的网站时所体验的环境。

标记允许添加其他开发环境，对于有多位开发人员同时处理不同项目的大型组织而言，通常需要这样做。

要完成本教程，只需要这三个环境。通过这些环境，您可以将标记库的不同工作版本托管在不同的URL，这样您便可以安全地添加新功能，并在适当的时间将这些功能提供给适当的用户（例如，开发人员、QA工程师、公众等）。

现在，让我们复制嵌入代码：

1. 在&#x200B;**[!UICONTROL Development]**&#x200B;行中，单击“安装”图标![安装图标](images/launch-installIcon.png)以打开模式窗口。

1. 请注意，标记将默认使用异步嵌入代码

1. 单击复制图标 ![复制图标](images/launch-copyIcon.png) 以将嵌入代码复制到剪贴板。

1. 单击&#x200B;**[!UICONTROL 关闭]**&#x200B;以关闭该模式窗口。

   ![安装图标](images/launch-copyInstallCode.png)

## 在示例 HTML 页面的 `<head>` 中实施嵌入代码

嵌入代码应在将共享资产的所有 HTML 页面的 `<head>` 元素中实施。您可能有一个或多个可在网站全局范围内控制`<head>`的模板文件，以便简化添加标记的过程。

如果没有模板文件，请复制示例的html页面代码并将其粘贴到代码编辑器中。 [Brackets](https://brackets.io/) 是一个免费的开源编辑器（如果需要）。

+++html页面代码示例

```html
<!doctype html>
<html lang="en">
<head>
    <title>Tags: Sample HTML Page</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags: Sample HTML Page</h1>
    <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
    <p>See <a href="https://docs.adobe.com/content/help/zh-Hans/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
</body>
</html>
```

+++

将位于第 34 行或附近的现有嵌入代码替换为剪贴板中的代码，并保存该页面。接下来，在 Web 浏览器中打开该页面。如果您使用 `file://` 协议加载该页面，则需要在代码编辑器中在嵌入代码 URL 的开头添加“https:”。示例页面的第 33-36 行可能如下所示：

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

打开 Web 浏览器的开发人员工具，然后转到“网络”选项卡。此时，您应会看到与标记环境URL有关的404错误：
![404错误](images/samplepage-404.png)

出现404错误属于预期结果，因为您尚未在此标记环境中构建库。 您将在下一个课程中学习如何构建库。如果您看到“失败”消息而不是 404 错误，则您可能忘记在嵌入代码中添加 `https://` 协议。再次重申，仅当使用 `file://` 协议加载示例页面时，才需要指定 `https://` 协议。做出相应更改，然后重新加载页面，直到出现 404 错误。

## 标记实施最佳实践

让我们花些时间查看一下示例页面中演示的一些标记实施最佳实践：

* **数据层**：

   * 我们&#x200B;*强烈*&#x200B;建议在您的网站上创建一个数据层，该数据层包含在Analytics、Target和其他营销解决方案中填充变量所需的全部属性。 此示例页面仅包含一个非常简单的数据层，但实际的数据层可能包含更多与页面、访客、访客购物车详情及其他内容相关的详细信息。有关数据层的更多信息，请参阅[客户体验数字数据层 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * 先定义数据层，然后再定义标签嵌入代码，以便最大化您可使用Experience Cloud解决方案执行的操作。

* **JavaScript帮助程序库**：如果您已在页面的`<head>`中实施诸如JQuery之类的库，请在标记之前加载该库，以便在标记和Target中使用该库的语法

* **HTML5 doctype**：Target 要求使用 HTML5 doctype

* **preconnect 和 dns-prefetch**：可使用 preconnect 和 dns-prefetch 缩短页面加载时间。另请参阅：[https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **异步Target实施的预隐藏代码片段**：您将在Target课程中了解更多相关信息，但是当通过异步标记嵌入代码部署Target时，您应在页面上的标记嵌入代码之前对预隐藏代码片段进行硬编码，以便管理内容闪烁

下面按建议顺序总结了上述最佳实践。请注意，对于特定于帐户的详细信息，使用了一些占位符：

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

现在，您已了解如何将标记嵌入代码添加到您的网站！

[下一课程“添加数据元素、规则和库”>](add-data-elements-rules.md)
