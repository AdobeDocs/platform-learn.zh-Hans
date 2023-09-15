---
title: 安装Adobe Experience Platform Mobile SDK
description: 了解如何在移动应用程序中实施Adobe Experience Platform Mobile SDK。
hide: true
source-git-commit: b3cf168fc9b20ea78df0f8863a6395e9a45ed832
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# 安装Adobe Experience Platform Mobile SDK

了解如何在移动应用程序中实施Adobe Experience Platform Mobile SDK。

## 先决条件

* 使用中所述的扩展成功构建标记库 [上一课程](configure-tags.md).
* 来自的开发环境文件ID [移动设备安装说明](configure-tags.md#generate-sdk-install-instructions).
* 已下载空的 [示例应用程序](https://git.corp.adobe.com/rmaur/Luma){target="_blank"}.
* 体验 [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## 学习目标

在本课程中，您将执行以下操作：

* 使用Swift包管理器将所需的SDK添加到您的项目中。
* 注册扩展。

>[!NOTE]
>
>在移动应用程序实施中，“扩展”和“SDK”这两个术语几乎可以互换。

## Swift包管理器

不要使用CocoaPods和Pod文件（如移动设备安装说明中所述），请参阅 [生成SDK安装说明](./configure-tags.md#generate-sdk-install-instructions))，您可使用Xcode的本机Swift包管理器添加单个包。

在Xcode中，使用 **[!UICONTROL 文件]** > **[!UICONTROL 添加包……]** 并安装下表中列出的所有软件包。 选择表中包的链接以获取特定包的完整URL。

| 包 | 描述 |
|---|---|
| [AEP核心](https://github.com/adobe/aepsdk-core-ios.git) | 此 `AEPCore`， `AEPServices`、和 `AEPIdentity` 扩展是Adobe Experience Platform SDK的基础 — 使用SDK的每个应用程序都必须包含这些扩展。 这些模块包含所有SDK扩展所需的一组通用功能和服务。<br/><ul><li>`AEPCore` 包含事件中心的实施。 事件中心是在应用程序和SDK之间交付事件的机制。 事件中心还用于在扩展之间共享数据。</li><li>`AEPServices` 提供平台支持所需的多种可重用的实现，包括网络、磁盘访问和数据库管理。</li><li>`AEPIdentity` 实施与Adobe Experience Platform Identity服务的集成。</li><li>`AEPSignal` 表示Adobe Experience Platform SDK Signal扩展，该扩展允许营销人员向其应用程序发送“信号”，以将数据发送到外部目标或打开URL。</li><li>`AEPLifecycle` 表示Adobe Experience Platform SDK生命周期扩展，该扩展可帮助收集应用程序生命周期量度，例如应用程序安装或升级信息、应用程序启动和会话信息、设备信息以及应用程序开发人员提供的任何其他上下文数据。</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | Adobe Experience Platform Edge Network移动扩展(`AEPEdge`)允许您从移动应用程序向Adobe Edge Network发送数据。 通过此扩展，您可以更稳健地实施Adobe Experience Cloud功能，通过一个网络调用提供多个Adobe解决方案，并同时将此信息转发到Adobe Experience Platform。<br/>Edge Network移动扩展是Adobe Experience Platform SDK的扩展，它需要 `AEPCore` 和 `AEPServices` 事件处理的扩展，以及 `AEPEdgeIdentity` 用于检索身份（如ECID）的扩展。 |
| [AEP Edge标识](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | AEP Edge Identity Mobile扩展(`AEPEdgeIdentity`)在使用Adobe Experience Platform SDK和Edge Network扩展时，支持处理来自移动应用程序的用户身份数据。 |
| [AEP Edge同意](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | AEP同意收集移动扩展(`AEPConsent`)在使用Adobe Experience Platform SDK和Edge Network扩展时，支持从移动应用程序收集同意首选项。 |
| [AEP用户配置文件](https://github.com/adobe/aepsdk-userprofile-ios.git) | Adobe Experience Platform用户配置文件移动扩展(`AEPUserProfile`)是一个扩展，用于管理Adobe Experience Platform SDK的用户配置文件。 |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | AEP Places扩展(`AEPPlaces`)允许您跟踪Adobe位置界面和Adobe数据收集标记规则中定义的地理位置事件。 |
| [AEP消息](https://github.com/adobe/aepsdk-messaging-ios.git) | AEP消息传送扩展(`AEPMessaging`)允许您将推送通知令牌和推送通知点进反馈发送到Adobe Experience Platform。 |
| [AEP优化](https://github.com/adobe/aepsdk-optimize-ios) | AEP优化扩展(`AEPOptimize`)提供一些API，以便使用Adobe Target或Adobe Journey OptimizerOffer decisioning在Adobe Experience Platform Mobile SDK中启用实时个性化工作流。 它需要 `AEPCore` 和 `AEPEdge` 用于将个性化查询事件发送到Experience Edge网络的扩展。 |
| [AEP保证](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance（又称Griffon项目）是一种新颖的扩展(`AEPAssurance`)，以帮助您检查、验证、模拟和验证在移动设备应用程序中收集数据或提供体验的方式。 此扩展可为您的应用程序启用保证。 |


安装所有软件包后，您的Xcode **[!UICONTROL 程序包依赖项]** 屏幕应如下所示：

![Xcode包依赖项](assets/xcode-package-dependencies.png){zoomable=&quot;yes&quot;}


## 导入扩展

在Xcode中，导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** 并确保以下导入是此源文件的一部分。

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

对执行相同操作 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 实用工具]** > **[!UICONTROL MobileSDK]**.

## 更新AppDelegate

导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **AppDelegate** 在Xcode项目导航器中。

1. 设置 `@AppStorage` 值 `environmentFileId` ，作为开发环境文件ID值，该值是在的步骤6中检索的。 [生成SDK安装说明](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. 将以下代码添加到 `application(_, didFinishLaunchingWithOptions)` 函数。

   ```swift
   // Define extensions
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

上述代码执行以下操作：

1. 注册所需的扩展。
1. 配置MobileCore和其他扩展以使用标记属性配置。
1. 启用调试日志记录。 欲知更多详情和选项，请参见 [Adobe Experience Platform移动SDK文档](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. 启动生命周期监控。 请参阅 [生命周期](lifecycle-data.md) 有关更多详细信息，请参阅教程中的步骤。
1. 将默认同意设置为“未知”。 请参阅 [同意](consent.md) 有关更多详细信息，请参阅教程中的步骤。

>[!IMPORTANT]
>
>确保更新 `MobileCore.configureWith(appId: self.environmentFileId)` 使用 `appId` 基于 `environmentFileId` 从您为（开发、暂存或生产）构建的标记环境中。
>

>[!SUCCESS]
>
>您现在已安装必要的包并更新了项目，以正确注册您将在本教程的其余部分使用的所需Adobe Experience Platform Mobile SDK扩展。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[设置保证](assurance.md)**
