---
title: 配置文件
description: 了解如何在移动应用程序中收集用户档案数据。
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# 配置文件

了解如何在移动应用程序中收集用户档案数据。

您可以使用Profile扩展在客户端上存储有关用户的属性。 此信息以后可用于在线或离线情景中定位和个性化消息，而无需连接到服务器以获得最佳性能。 配置文件扩展管理客户端操作配置文件(CSOP)，提供对API做出反应的方式，更新用户配置文件属性，并将用户配置文件属性作为生成事件与系统的其他部分共享。

配置文件数据由其他扩展用来执行与配置文件相关的操作。 例如，规则引擎扩展会使用用户档案数据并基于用户档案数据运行规则。 进一步了解 [配置文件扩展](https://developer.adobe.com/client-sdks/documentation/profile/) 在文档中

>[!IMPORTANT]
>
>本课程中介绍的配置文件功能与Adobe Experience Platform和基于Platform的应用程序中的实时客户配置文件功能不同。


## 先决条件

* 成功构建并运行安装并配置了SDK的应用程序。
* 已导入配置文件SDK。

   ```swift
   import AEPUserProfile
   ```

## 学习目标

在本课程中，您将执行以下操作：

* 设置或更新用户属性。
* 检索用户属性。


## 设置并更新

快速了解用户以前是否曾在应用程序中购买过产品，这对于定位和/或个性化很有帮助。 让我们在Luma应用程序中设置它。

1. 导航至 `Cart.swift`

1. 将以下代码添加到 `processOrder() `函数。

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

个性化团队可能还希望根据用户的忠诚度级别进行定位。 让我们在Luma应用程序中设置它。

1. 导航至 `Account.swift`

1. 将以下代码添加到 `showUserInfo()` 函数。

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

其他 `updateUserAttributes` 可以找到文档 [此处](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Get

更新用户的属性后，该属性将可供其他AdobeSDK使用，但您也可以显式检索属性。

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

其他 `getUserAttributes` 可以找到文档 [此处](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## 使用保证进行验证

1. 查看 [设置说明](assurance.md) 部分。
1. 安装应用程序。
1. 使用保证生成的URL启动应用程序。
1. 选择帐户图标，然后选择登录。 注意：您未提供任何凭据。
1. 关闭登录菜单，然后再次选择帐户图标。 这会将您转到帐户详细信息屏幕，其中 `loyaltyLevel` 设置。
1. 您应会看到 **[!UICONTROL UserProfileUpdate]** 使用更新后的Assurance UI中的事件 `profileMap` 值。
   ![验证配置文件](assets/mobile-profile-validate.png)

下一步： **[将数据映射到Adobe Analytics](analytics.md)**

>[!NOTE]
>
>感谢您投入时间来了解Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此分享这些内容 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)