---
title: 设置保证
description: 了解如何在移动设备应用程序中实施保证扩展。
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---

# Assurance

了解如何在移动设备应用程序中设置Adobe Experience Platform Assurance。

Assurance（正式称为Project Griffon）旨在帮助您在移动设备应用程序中检查、校样、模拟和验证如何收集数据或提供体验。

保证功能可帮助您检查由Adobe Experience Platform Mobile SDK生成的原始SDK事件。 SDK收集的所有事件都可供检查。 SDK事件在列表视图中加载，按时间排序。 每个事件都有一个详细视图，其中提供了更多详细信息。 还提供了用于浏览SDK配置、数据元素、共享状态和SDK扩展版本的其他视图。 进一步了解 [保证](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance) （在产品文档中）。


## 先决条件

* 已成功构建并运行安装并配置了SDK的示例应用程序。

## 学习目标

在本课程中，您将：

* 确认贵组织拥有访问权限（如果您没有权限，请求）。
* 设置基本URL。
* 添加所需的iOS特定代码。
* 连接到会话。

## 确认访问

通过完成以下步骤，确认贵组织有权访问“保证”：

1. 访问 [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon){target=&quot;_blank&quot;}
1. 使用您的Adobe ID凭据登录Experience Cloud。
1. 如果您被带到 **[!UICONTROL 会话]** ，则您拥有访问权限。 如果您被带到测试版访问页面，请选择 **[!UICONTROL 注册]**.

## 实施

除了 [SDK安装](install-sdks.md) 您在前面的课程中已完成，iOS还需要添加以下内容。 将以下代码添加到 `AppDelegate.swift` 文件：

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

本教程提供的示例Luma使用iOS 12.0。如果您要与您自己的使用iOS 13及更高版本的基于场景的应用程序一起使用 `UISceneDelegate's scene(_:openURLContexts:)` 方法如下：

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

可以找到更多信息 [此处](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance#implement-aep-assurance-session-start-apis-ios-only){target=&quot;_blank&quot;}。

## 设置基本URL

1. 打开Xcode并选择项目名称。
1. 导航到 **信息** 选项卡。
1. 向下滚动到 **URL类型** ，然后选择 **+** 按钮以添加新受众。
1. 已设置 **标识符** 和 **URL方案** “lumadeeplink”。
1. 构建并运行应用程序。

![保证url](assets/mobile-assurance-url-type.png)

要进一步了解iOS中的URL方案，请查阅 [Apple文档](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=&quot;_blank&quot;}。

通过浏览器或二维码打开URL，可确保该URL以基本URL开头，该基本URL可打开应用程序并包含其他参数。 这些唯一参数用于连接会话。

## 连接到会话

1. 导航到 [保证UI](https://experience.adobe.com/griffon){target=&quot;_blank&quot;}。
1. 选择 **[!UICONTROL 创建会话]**.
1. 提供 **[!UICONTROL 会话名称]** 例如 `Luma App QA` 和 **[!UICONTROL 基本URL]** `lumadeeplink://default`
1. 选择&#x200B;**[!UICONTROL 下一步]**。
   ![保证创建会话](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL 扫描QR代码]** 如果您使用的是物理设备。 如果您使用的是模拟器，则 **[!UICONTROL 复制链接]** 然后在模拟器中使用Safari打开它。
   ![保证质量保证代码](assets/mobile-assurance-qr-code.png)
1. 当应用程序加载时，会显示一个模式窗口，要求您从上一步输入PIN。
   ![保证输入PIN](assets/mobile-assurance-enter-pin.png)
1. 如果连接成功，您将在Assurance Web UI中看到事件，并在应用程序中看到一个浮动的Assurance图标。
   * 保障图标浮动。
      ![保证模式](assets/mobile-assurance-modal.png)
   * Experience Cloud事件在Web UI中传入。
      ![保证事件](assets/mobile-assurance-events.png)

如果您遇到任何挑战，请查看 [技术](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance){target=&quot;_blank&quot;}和 [常规文档](https://aep-sdks.gitbook.io/docs/beta/project-griffon){target=&quot;_blank&quot;}。

下一个： **[同意](consent.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)