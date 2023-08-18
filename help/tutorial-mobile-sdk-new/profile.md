---
title: 配置文件
description: 了解如何在移动应用程序中收集用户档案数据。
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# 配置文件

了解如何在移动应用程序中收集用户档案数据。

您可以使用Profile扩展在客户端存储有关用户的属性。 此信息以后可用于在线或离线情景中定位和个性化消息，而无需连接到服务器以获得最佳性能。 配置文件扩展管理客户端操作配置文件(CSOP)，提供对API做出反应的方式，更新用户配置文件属性，并将用户配置文件属性作为已生成事件与系统的其他部分共享。

配置文件数据由其他扩展用于执行与配置文件相关的操作。 规则引擎扩展就是一个示例，该扩展会使用用户档案数据并根据用户档案数据运行规则。 了解关于 [配置文件扩展](https://developer.adobe.com/client-sdks/documentation/profile/) 在文档中

>[!IMPORTANT]
>
>本课程中介绍的配置文件功能与Adobe Experience Platform中的实时客户配置文件功能以及基于平台的应用程序不同。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 已导入配置文件SDK。

  ```swift
  import AEPUserProfile
  ```

## 学习目标

在本课程中，您将执行以下操作：

* 设置或更新用户属性。
* 检索用户属性。


## 设置和更新

快速了解用户以前是否曾在应用程序中购买过产品，这对定位和/或个性化会很有帮助。 让我们在Luma应用程序中设置它。

1. 导航到 **[!UICONTROL 产品视图]** (in **[!UICONTROL 视图]** > **[!UICONTROL 产品]**)并找到对的调用 `updateUserAttributes` （在“购买”按钮内）：

   ```swift {highlight="8-9"}
   Button {
       Task {
           if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send purchase commerce experience event
               MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
               // Update attributes
               MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
           }
       }
       showPurchaseDialog.toggle()
   } label: {
       Label("", systemImage: "creditcard")
   }
   .alert(isPresented: $showPurchaseDialog, content: {
       Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
   })
   ```

2. 导航到 **[!UICONTROL MobileSDK]** 并查找 `updateUserAttributes` 函数。 添加以下高亮显示的代码：

   ```swift {highlight="2-4"}
   func updateUserAttributes(attributeName: String, attributeValue: String) {
       var profileMap = [String: Any]()
       profileMap[attributeName] = attributeValue
       UserProfile.updateUserAttributes(attributeDict: profileMap)
   }
   ```

   此代码：

   1. 设置空的词典，名为 `profileMap`.

   1. 使用以下方式将元素添加到词典 `attributeName` (例如 `isPaidUser`)，和 `attributeValue` (例如 `yes`)。

   1. 使用 `profileMap` 词典作为值 `attributeDict` 的参数 `UserProfile.updateUserAttributes` API调用。


其他 `updateUserAttributes` 可找到文档 [此处](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Get

更新用户的属性后，该属性便可用于其他AdobeSDK，但您也可以显式检索属性。

1. 导航到 **[!UICONTROL 主页视图]** (in **[!UICONTROL 视图]** > **[!UICONTROL 常规]**)并查找 `.onAppear` 修饰符。 添加以下代码：

   ```swift {highlight="3-11"}
   .onAppear {
       // Track view screen
       MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: home")
       // Get attributes
       UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
           if attributes?["isPaidUser"] as! String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   此代码：

   1. 调用 `UserProfile.getUserAttributes` 关闭 `iPaidUser` 属性名称作为 `attributeNames` 数组。
   1. 然后检查的值 `isPaidUser` 属性和时间 `yes`，会在右上角的“人员”图标上放置一个徽章。

其他 `getUserAttributes` 可找到文档 [此处](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## 使用保障进行验证

1. 查看 [设置说明](assurance.md) 部分。
1. 安装应用程序。
1. 使用保障生成的URL启动应用程序。
1. 运行应用程序以登录并与产品交互。

   1. 将“Assurance（保证）”图标向左移动。
   1. 选择 **[!UICONTROL 主页]** 在选项卡栏中。
   1. 要打开“登录”工作表，请选择 **[!UICONTROL 登录]** 按钮。
   1. 要插入随机电子邮件和客户ID，请选择 **[!UICONTROL A|]** 按钮。
   1. 选择 **[!UICONTROL 登录]**.
   1. 选择 **[!UICONTROL 产品]** 在选项卡栏中。
   1. 选择一个产品。
   1. 选择 **[!UICONTROL 保存供以后使用]**.
   1. 选择 **[!UICONTROL 添加到购物车]**.
   1. 选择 **[!UICONTROL 购买]**.
   1. 返回至 **[!UICONTROL 主页]** 屏幕。 您应会看到已更新的登录按钮。

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200"> <img src="./assets/personbadges.png" width="200">

1. 您应该会看到 **[!UICONTROL UserProfileUpdate]** 和 **[!UICONTROL getuserattributes]** 具有更新的Assurance UI中的事件 `profileMap` 值。
   ![验证配置文件](assets/profile-validate.png)

>[!SUCCESS]
>
>您现在已设置应用程序，以更新Edge Network和（设置后）Adobe Experience Platform中用户档案的属性。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[将数据映射到Adobe Analytics](analytics.md)**
