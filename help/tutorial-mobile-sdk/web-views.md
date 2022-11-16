---
title: 处理WebViews
description: 了解如何在移动设备应用程序中使用WebViews处理数据收集。
kt: 6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 处理WebViews

了解如何在移动设备应用程序中使用WebViews处理数据收集。

## 先决条件

* 已成功构建并运行安装并配置了SDK的应用程序。

## 学习目标

在本课程中，您将：

* 了解为什么必须对WebViews进行特殊考虑。
* 了解防止跟踪问题所需的代码。

## 潜在的跟踪问题

如果您从应用程序的本机部分和WebView发送数据，则每个应用程序都会生成自己的Experience CloudID(ECID)。 这会导致点击断开连接并夸大访问/访客数据。 有关ECID的更多信息，请参阅 [ECID概述](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

要解决这种不良情况，必须将用户的ECID从本机部分传递到WebView。

WebView中的Experience CloudID服务JavaScript扩展会从URL中提取ECID，而不是向Adobe发送请求以获取新ID。 ID服务使用此ECID来跟踪访客。

## 实施

在Luma示例应用程序中，找到 `TermsOfService.swift` 文件(在 `Intro-Login_SignUp` ，并找到以下代码：

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

这是加载WebView的简单方法。 在这种情况下，它是本地文件，但远程页面也有相同的概念。

重构Web视图代码，如下所示：

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

您可以进一步了解 `Identity.getUrlVariables` 中的API [边缘网络扩展API参考指南](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables).

## 验证

在查看 [设置说明](assurance.md) 将您的模拟器或设备连接到Assurance，加载WebView并查找 `Edge Identity Response URL Variables` 事件 `com.adobe.griffon.mobile` 供应商。

要加载WebView，请转到Luma应用程序的主屏幕，选择“account”图标，然后在页脚中选择“Terms of Use”。

加载WebView后，选择事件并查看 `urlvariables` 字段 `ACPExtensionEventData` 对象，则确认URL中存在以下参数： `adobe_mc`, `mcmid`和 `mcorgid`.

![Web视图验证](assets/mobile-webview-validation.png)

示例 `urvariables` 字段，请参阅下文：

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>Platform Web SDK(版本2.11.0或更高版本)当前支持通过这些URL参数进行访客拼合，并且 `VisitorAPI.js`.


下一个： **[身份](identity.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)