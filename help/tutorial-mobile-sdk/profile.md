---
title: 使用Platform Mobile SDK收集配置文件数据
description: 了解如何在移动应用程序中收集用户档案数据。
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 收集配置文件数据

了解如何在移动应用程序中收集用户档案数据。

您可以使用Profile扩展在客户端存储有关用户的属性。 此信息以后可用于在线或离线情景中定位和个性化消息，而无需连接到服务器以获得最佳性能。 配置文件扩展管理客户端操作配置文件(CSOP)，提供对API做出反应的方式，更新用户配置文件属性，并将用户配置文件属性作为已生成事件与系统的其他部分共享。

配置文件数据由其他扩展用于执行与配置文件相关的操作。 规则引擎扩展就是一个示例，该扩展会使用用户档案数据并根据用户档案数据运行规则。 了解关于 [配置文件扩展](https://developer.adobe.com/client-sdks/documentation/profile/) 在文档中

>[!IMPORTANT]
>
>本课程中介绍的配置文件功能与Adobe Experience Platform中的实时客户配置文件功能以及基于平台的应用程序不同。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 设置或更新用户属性。
* 检索用户属性。


## 设置和更新用户属性

快速了解用户过去或最近是否进行了购买有助于在应用程序中定位和/或个性化。 让我们在Luma应用程序中设置它。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** >  **[!DNL MobileSDK]** 在Xcode项目导航器中查找 `func updateUserAttribute(attributeName: String, attributeValue: String)` 函数。 添加以下代码：

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   此代码：

   1. 设置空的词典，名为 `profileMap`.

   1. 使用以下方式将元素添加到词典 `attributeName` (例如 `isPaidUser`)，和 `attributeValue` (例如 `yes`)。

   1. 使用 `profileMap` 词典作为值 `attributeDict` 的参数 [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) API调用。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** 在Xcode项目导航器中找到对的调用 `updateUserAttributes` (在购买行为守则内， <img src="assets/purchase.png" width="15" /> 按钮)。 添加以下代码：

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## 获取用户属性

更新了用户的属性后，其他AdobeSDK便可以使用该属性，但您也可以显式检索属性，以使应用程序按所需的方式运行。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** 在Xcode项目导航器中查找 `.onAppear` 修饰符。 添加以下代码：

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   此代码：

   1. 调用 [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) 包含的API `isPaidUser` 属性名称作为 `attributeNames` 数组。
   1. 然后检查的值 `isPaidUser` 属性和时间 `yes`，在 <img src="assets/paiduser.png" width="20" /> 图标（位于右上角）进行标记。

可找到其他文档 [此处](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## 使用保障进行验证

1. 查看 [设置说明](assurance.md#connecting-to-a-session) 部分以将模拟器或设备连接到Assurance。
1. 运行应用程序以登录并与产品交互。

   1. 将“Assurance（保证）”图标向左移动。
   1. 选择 **[!UICONTROL 主页]** 在选项卡栏中。
   1. 要打开“登录”工作表，请选择 <img src="assets/login.png" width="15" /> 按钮。

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. 要插入随机电子邮件和客户ID，请选择 <img src="assets/insert.png" width="15" /> 按钮。
   1. 选择 **[!UICONTROL 登录]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. 选择 **[!DNL Products]** 在选项卡栏中。
   1. 选择一个产品。
   1. 选择 <img src="assets/saveforlater.png" width="15" />。
   1. 选择 <img src="assets/addtocart.png" width="20" />。
   1. 选择 <img src="assets/purchase.png" width="15" />。

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. 返回至 **[!UICONTROL 主页]** 屏幕。 您应该会看到已添加徽章 <img src="assets/person-badge-icon.png" width="15" />。

      <img src="./assets/personbadges.png" width="300">



1. 在Assurance UI中，您应该看到 **[!UICONTROL UserProfileUpdate]** 和 **[!UICONTROL getuserattributes]** 具有已更新内容的事件 `profileMap` 值。
   ![验证配置文件](assets/profile-validate.png)

>[!SUCCESS]
>
>您现在已设置应用程序，以更新Edge Network和（设置后）Adobe Experience Platform中用户档案的属性。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[使用地标](places.md)**
