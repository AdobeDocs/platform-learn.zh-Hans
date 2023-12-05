---
title: 为Platform Mobile SDK实施实施同意
description: 了解如何在移动应用程序中实施同意。
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 实施同意

了解如何在移动应用程序中实施同意。

使用Adobe Experience Platform Mobile SDK和Edge Network扩展时，Adobe Experience Platform Consent移动扩展支持从移动应用程序收集同意首选项。 了解关于 [同意扩展](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) 在文档中。

## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 提示用户同意。
* 根据用户响应更新扩展。
* 了解如何获取当前的同意状态。

## 征求同意

如果您从一开始就学习了本教程，则可能会记得您已将同意扩展中的默认同意设置为 **[!UICONTROL 待处理 — 在用户提供同意首选项之前发生的队列事件。]**

要开始收集数据，您必须获得用户的同意。 在真实世界应用程序中，您将需要咨询所在地区的同意最佳实践。 在本教程中，您只需通过询问并发出警报即可获得用户的同意：

1. 您只需请求用户一次同意即可。 为此，您可以使用Apple的Mobile SDK同意与跟踪所需的授权相结合 [应用程序跟踪透明度框架](https://developer.apple.com/documentation/apptrackingtransparency). 在此应用程序中，您假设当用户授权跟踪时，他们同意收集事件。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode项目导航器中。

   将此代码添加到 `updateConsent` 函数。

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 免责声明视图]** 在Xcode的项目导航器中，该视图是在安装或重新安装应用程序并首次启动应用程序后显示的视图。 系统会根据Apple提示用户授权跟踪 [应用程序跟踪透明度框架](https://developer.apple.com/documentation/apptrackingtransparency). 如果用户授权，则还需要更新同意。

   将以下代码添加到 `ATTrackingManager.requestTrackingAuthorization { status in` 结束。

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## 获取当前同意状态

同意移动扩展会根据当前同意值自动禁止/挂起/允许跟踪。 您还可以自行访问当前同意状态：

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode的项目导航器中。

   将以下代码添加到 `getConsents` 函数：

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 主页视图]** 在Xcode的项目导航器中。

   将以下代码添加到 `.task` 修饰符：

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

在上例中，您只是将同意状态记录到Xcode中的控制台。 在真实场景中，您可以使用该场景来修改向用户显示的菜单或选项。

## 使用保障进行验证

1. 从设备或模拟器中删除应用程序，以正确重置和初始化跟踪并获取同意。
1. 要将模拟器或设备连接到Assurance，请查看 [设置说明](assurance.md#connecting-to-a-session) 部分。
1. 从移动应用程序时 **[!UICONTROL 主页]** 屏幕至 **[!UICONTROL 产品]** 屏幕并返回至 **[!UICONTROL 主页]** 屏幕，您应该会看到 **[!UICONTROL 获取同意响应]** Assurance UI中的事件。
   ![验证同意](assets/consent-update.png)


>[!SUCCESS]
>
>现在，您已启用应用程序，使其在安装（或重新安装）后初始启动时提示用户同意使用Adobe Experience Platform Mobile SDK。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[收集生命周期数据](lifecycle-data.md)**
