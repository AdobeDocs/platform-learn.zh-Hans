---
title: 配置文件
description: 了解如何在移动设备应用程序中收集用户档案数据。
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# 配置文件

了解如何在移动设备应用程序中收集用户档案数据。

您可以使用配置文件扩展在客户端上存储有关用户的属性。 此信息稍后可用于在线或离线场景期间定位和个性化消息，而无需连接到服务器即可获得最佳性能。 配置文件扩展可管理客户端操作配置文件(CSOP)，提供一种对API做出响应、更新用户配置文件属性，以及将用户配置文件属性与系统其余部分共享为生成事件的方法。

其他扩展会使用配置文件数据来执行与配置文件相关的操作。 例如，规则引擎扩展使用用户档案数据并根据用户档案数据运行规则。 进一步了解 [用户档案扩展](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) 文档

>[!IMPORTANT]
>
>本课程中描述的用户档案功能与Adobe Experience Platform和基于平台的应用程序中的实时客户用户档案功能是分开提供的。


## 先决条件

* 已成功构建并运行安装并配置了SDK的应用程序。
* 导入了配置文件SDK。

   ```swift
   import AEPUserProfile
   ```

## 学习目标

在本课程中，您将：

* 设置或更新用户属性。
* 检索用户属性。


## 设置和更新

快速了解用户之前是否在应用程序中购买过产品，这有助于进行定位和/或进行个性化。 让我们在Luma应用程序中设置。

1. 导航至 `Cart.swift`

1. 将以下代码添加到 `processOrder() `函数。

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

个性化团队可能还希望根据用户的忠诚度级别进行定位。 让我们在Luma应用程序中设置。

1. 导航至 `Account.swift`

1. 将以下代码添加到 `showUserInfo()` 函数。

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

其他 `updateUserAttributes` 文档可找到 [此处](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## 获取

更新用户的属性后，该属性将可供其他AdobeSDK使用，但您也可以显式检索属性。

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

其他 `getUserAttributes` 文档可找到 [此处](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## 通过保证进行验证

1. 查看 [设置说明](assurance.md) 中。
1. 安装应用程序。
1. 使用生成的保证URL启动应用程序。
1. 选择帐户图标，然后选择登录。 注意：您没有提供任何凭据。
1. 关闭登录菜单，然后再次选择帐户图标。 这会将您转到帐户详细信息屏幕，其中 `loyaltyLevel` 设置。
1. 您应会看到 **[!UICONTROL UserProfileUpdate]** 在Assurance UI中发生事件，并且更新了 `profileMap` 值。
   ![验证配置文件](assets/mobile-profile-validate.png)

下一个： **[将数据映射到Adobe Analytics](analytics.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)