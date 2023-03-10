---
title: 同意
description: 了解如何在移动设备应用程序中实施同意。
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# 同意

了解如何在移动设备应用程序中实施同意。

使用Adobe Experience Platform Mobile SDK和Edge Network扩展时，Adobe Experience Platform同意移动扩展允许从移动设备应用程序收集同意首选项。 进一步了解 [同意扩展](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network)，在文档中。

## 先决条件

* 已成功构建并运行安装并配置了SDK的应用程序。

## 学习目标

在本课程中，您将：

* 提示用户同意。
* 根据用户响应更新扩展。
* 了解如何获取当前同意状态。

## 请求同意

如果您从头开始学习教程，您将记得在 **[!UICONTROL 默认同意级别]** “待定”。 要开始收集数据，您必须获得用户的同意。 在本教程中，您只需在真实应用程序中通过提示获取同意，然后方法是咨询您所在地区的同意最佳实践。

1. 您只想询问用户一次。 一种简单的方法就是使用 `UserDefaults`.
1. 导航到 `Home.swift`。
1. 将以下代码添加到 `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. 如果用户以前没有看到警报，则显示警报并根据其响应更新同意。 将以下代码添加到 `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## 获取当前同意状态

同意移动扩展将根据当前同意值自动禁止/附加/允许跟踪。 您还可以自行访问当前同意状态：

1. 导航到 `Home.swift`。
1. 将以下代码添加到 `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

在上例中，您只需将同意状态打印到控制台即可。 在现实场景中，您可以使用它来修改向用户显示的菜单或选项。

## 通过保证进行验证

1. 查看 [保证](assurance.md) 课程。
1. 安装应用程序。
1. 使用保证生成的URL启动应用程序。
1. 如果您正确添加了上述代码，系统将提示您提供同意。 选择 **是**.
   ![同意弹出窗口](assets/mobile-consent-validate.png)
1. 您应会看到 **[!UICONTROL 同意首选项已更新]** 事件。
   ![验证同意](assets/mobile-consent-update.png)

下一个： **[收集生命周期数据](lifecycle-data.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)