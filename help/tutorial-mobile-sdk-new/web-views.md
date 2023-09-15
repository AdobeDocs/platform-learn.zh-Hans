---
title: 处理Web视图
description: 了解如何在移动应用程序中通过WebViews处理数据收集。
jira: KT-6987
hide: true
source-git-commit: b3cf168fc9b20ea78df0f8863a6395e9a45ed832
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# 处理Web视图

了解如何在移动应用程序中通过WebViews处理数据收集。

## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 了解为什么您必须对应用程序中的WebViews采取特殊注意事项。
* 了解防止跟踪问题所需的代码。

## 潜在的跟踪问题

如果您从应用程序的本机部分和应用程序内的WebView发送数据，则每个部分都会生成自己的Experience CloudID (ECID)，这会导致断开连接的点击量和夸大的访问/访客数据。 有关ECID的更多信息，请参阅 [ECID概述](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

要解决该不良情况，请务必将用户的ECID从应用程序的本机部分传递到您可能想要在应用程序中使用的WebView。

WebView中使用的AEP Edge Identity扩展可收集当前ECID并将其添加到URL，而不是向Adobe发送请求以获取新ID。 然后，实施将使用此ECID来请求URL。

## 实施

导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 视图]** > **[!UICONTROL 信息]** > **[!UICONTROL 服务条款表]**，然后找到 `func loadUrl()` 中的函数 `final class SwiftUIWebViewModel: ObservableObject` 类。 添加以下调用以处理Web视图：

```swift
// Handle web view
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

此 [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) API为URL设置变量以包含所有相关信息，如ECID等。 在本例中，您使用的是本地文件，但相同的概念也适用于远程页面。

您可了解有关 `Identity.getUrlVariables` 中的API [Edge Network身份扩展API参考指南](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## 验证

要执行代码，请执行以下操作：

1. 转到 **[!UICONTROL 设置]** 在应用程序中
1. 点按 **[!UICONTROL 查看……]** 按钮以显示 **[!UICONTROL 使用条款]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. 在Assurance UI中，查找 **[!UICONTROL Edge Identity响应URL变量]** 来自的事件 **[!UICONTROL com.adobe.griffon.mobile]** 供应商。
1. 选择事件并查看 **[!UICONTROL url变量]** 中的字段 **[!UICONTROL ACPExtensionEventData]** 对象，确认URL中存在以下参数： `adobe_mc`， `mcmid`、和 `mcorgid`.

   ![webview验证](assets/webview-validation.png)

   示例 `urvariables` 字段如下所示：

   * 原始（带转义字符）

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * 美化

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

>[!NOTE]
>
>Platform Web SDK（版本2.11.0或更高版本）中以及使用 `VisitorAPI.js`.


>[!SUCCESS]
>
>现在，您已经将应用程序设置为在Webview中根据URL显示内容，该URL使用与Adobe Experience Platform Mobile SDK已颁发的ECID相同的ECID。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[标识](identity.md)**
