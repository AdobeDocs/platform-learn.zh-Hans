---
title: 处理Web视图
description: 了解如何在移动应用程序中通过WebViews处理数据收集。
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 处理Web视图

了解如何在移动应用程序中通过WebViews处理数据收集。

>[!INFO]
>
> 2023年11月下旬，本教程将替换为使用新示例移动应用程序的新教程

## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 了解为什么您必须针对WebViews采取特殊注意事项。
* 了解防止跟踪问题所需的代码。

## 潜在的跟踪问题

如果您从应用程序的本机部分和WebView发送数据，则每个部分都会生成自己的Experience CloudID (ECID)。 这会导致断开连接的点击和夸大的访问/访客数据。 有关ECID的更多信息，请参阅 [ECID概述](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

要解决此不良情况，必须将用户的ECID从本机部分传递到WebView。

WebView中的Experience CloudID服务JavaScript扩展会从URL中提取ECID，而不是向Adobe发送请求以获取新ID。 ID服务使用此ECID来跟踪访客。

## 实施

在Luma示例应用程序中，找到 `TermsOfService.swift` 文件(在 `Intro-Login_SignUp` 文件夹)，并找到以下代码：

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

这是加载WebView的简单方法。 在本例中，它是一个本地文件，但同样的概念也适用于远程页面。

重构Webview代码，如下所示：

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

您可了解有关 `Identity.getUrlVariables` 中的API [Edge Network身份扩展API参考指南](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## 验证

在查看 [设置说明](assurance.md) 将您的模拟器或设备连接到Assurance，加载WebView并查找 `Edge Identity Response URL Variables` 来自的事件 `com.adobe.griffon.mobile` 供应商。

要加载WebView，请转到Luma应用程序的主屏幕，选择“帐户”图标，然后在页脚中选择“使用条款”。

加载WebView后，选择事件并查看 `urlvariables` 中的字段 `ACPExtensionEventData` 对象，确认URL中存在以下参数： `adobe_mc`， `mcmid`、和 `mcorgid`.

![webview验证](assets/mobile-webview-validation.png)

示例 `urvariables` 字段如下所示：

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>Platform Web SDK（版本2.11.0或更高版本）当前支持通过这些URL参数拼接访客，并且 `VisitorAPI.js`.


下一步： **[标识](identity.md)**

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)