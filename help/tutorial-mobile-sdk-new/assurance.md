---
title: 设置保证
description: 了解如何在移动应用程序中实施Assurance扩展。
feature: Mobile SDK,Assurance
hide: true
source-git-commit: b3cf168fc9b20ea78df0f8863a6395e9a45ed832
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 8%

---

# Assurance

了解如何在移动应用程序中设置Adobe Experience Platform保障。

Assurance（正式称为Project Griffon）旨在帮助您检查、证明、模拟和验证在移动应用程序中收集数据或提供体验的方式。

Assurance 可帮助您检查 Adobe Experience Platform Mobile SDK 生成的原始 SDK 事件。SDK 收集的所有事件都可供检查。SDK 事件加载在列表视图中，按时间排序。每个事件都有一个详细视图，可提供更多详细信息。还提供了用于浏览SDK配置、数据元素、共享状态和SDK扩展版本的其他视图。 了解关于 [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) 在产品文档中。


## 先决条件

* 成功设置已安装并配置SDK的应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 确认您的组织具有访问权限（如果您没有访问权限，请进行请求）。
* 设置您的基本URL。
* 添加所需的iOS特定代码。
* 连接到会话.

## 确认访问

确认您的组织有权访问Assurance。 您作为用户，应该被添加到Adobe Experience Platform的配置文件。 请参阅 [用户访问权限](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) ，以了解详细信息。

## 实施

除了一般 [SDK安装](install-sdks.md)（已在之前的课程中完成），iOS还需要添加以下内容才能启动应用程序的保障会话。

1. 导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL SceneDelegate]** 在Xcode的项目导航器中。

1. 将以下代码添加到 `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`：

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   当应用程序处于后台并使用深层链接打开时，此代码会启动保证会话。

可以找到更多信息 [此处](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## 签名

在Xcode中首次运行应用程序之前，请确保更新签名。

1. 在Xcode中打开项目。
1. 选择 **[!UICONTROL Luma]** 在项目导航器中。
1. 选择 **[!UICONTROL Luma]** 目标。
1. 选择 **签名和功能** 选项卡。
1. 配置 **[!UICONTROL 自动管理签名]**， **[!UICONTROL 团队]**、和 **[!UICONTROL 捆绑标识符]**，或使用您的特定Apple开发配置详细信息。

   ![Xcode签名功能](assets/xcode-signing-capabilities.png){zoomable=&quot;yes&quot;}

## 设置基本URL

1. 转到Xcode中的项目。
1. 选择 **[!UICONTROL Luma]** 在项目导航器中。
1. 选择 **[!UICONTROL Luma]** 目标。
1. 选择 **信息** 选项卡。
1. 要添加基本URL，请向下滚动到 **URL类型** 并选择 **+** 按钮。
1. 设置 **标识符** 到您在中配置的捆绑包标识符 [签名](#signing) (例如 `com.adobe.luma.tutorial.swiftui`)并设置 **URL方案**&#x200B;例如 `lumatutorialswiftui`.

   ![保证url](assets/assurance-url-type.png)

要了解有关iOS中URL方案的更多信息，请查看 [Apple的文档](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

Assurance的工作方式是通过浏览器或二维码打开URL。 该URL以基本URL开头，该URL可打开应用程序并包含其他参数。 这些唯一参数用于连接会话。


## 连接到会话

1. 在模拟器中或在连接的物理设备上运行应用程序。
1. 选择 **[!UICONTROL Assurance]** 从数据收集UI的左边栏中。
1. 选择 **[!UICONTROL 创建会话]**.
1. 选择 **[!UICONTROL 开始]**.
1. 提供 **[!UICONTROL 会话名称]** 例如 `Luma Mobile App Session` 和 **[!UICONTROL 基本URL]**，这是您在Xcode中输入的URL方案，后面接着 `://`. 例如：`lumatutorialswiftui://`。
1. 选择&#x200B;**[!UICONTROL 下一步]**。
   ![保证创建会话](assets/assurance-create-session.png)
1. 在 **[!UICONTROL 创建新会话]** 模式对话框：

   如果您使用的是物理设备：

   * 选择 **[!UICONTROL 扫描二维码]**. 使用物理设备上的摄像头扫描二维码并点击链接以打开应用程序。

     ![保证qa代码](assets/assurance-qr-code.png)

   如果您使用模拟器：

   1. 选择 **[!UICONTROL 复制链接]**.
   1. 使用以下方式复制深层链接 ![复制](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  并在模拟器中使用深层链接通过Safari打开应用程序。
      ![保证副本链接](assets/assurance-copy-link.png)

1. 应用程序加载时，系统会显示一个模式对话框，要求您输入步骤7中显示的PIN。

   <img src="assets/assurance-enter-pin.png" width="300">

   输入PIN并选择 **[!UICONTROL 连接]**.


1. 如果连接成功，您会看到：
   * “保证”图标浮动在应用程序顶部。

     <img src="assets/assurance-modal.png" width="300">

   * 在Assurance UI中执行的Experience Cloud更新显示：

      1. 来自应用程序的体验事件。
      1. 选定事件的详细信息。
      1. 设备和时间轴。

         ![保证事件](assets/assurance-events.png)

如果您遇到任何挑战，请查看 [技术](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.

>[!SUCCESS]
>
>您现在已将应用程序设置为在教程的其余部分使用Assurance 。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


下一步： **[同意](consent.md)**
