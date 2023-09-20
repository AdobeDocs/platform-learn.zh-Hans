---
title: 收集身份数据
description: 了解如何在移动应用程序中收集身份数据。
feature: Mobile SDK,Identities
hide: true
source-git-commit: cd1efbfaa335c08cbcc22603fe349b4594cc1056
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---

# 收集身份数据

了解如何在移动应用程序中收集身份数据。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。 身份字段和命名空间是将不同数据源连接在一起的粘合剂，可构建360度实时客户档案。

了解关于 [身份扩展](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 和 [身份服务](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hans) 在文档中。

## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 设置自定义身份命名空间。
* 更新身份。
* 验证身份图。
* 获取ECID和其他身份。


## 设置自定义身份命名空间

身份命名空间是的组件 [Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hans) 作为与身份相关的上下文指示器。 例如，它们会将`name@email.com`的值区别于电子邮件地址或将`443522`区别于数字 CRM ID。

>[!NOTE]
>
>Mobile SDK会在安装应用程序后在自身的命名空间中生成一个唯一标识，名为Experience CloudID (ECID)。 此ECID存储在移动设备上的永久内存中，随每次点击一起发送。 当用户卸载应用程序或将Mobile SDK全局隐私状态设置为optedout时，将删除ECID。 在示例Luma应用程序中，您应该删除并重新安装该应用程序，以使用它自己的唯一ECID创建新配置文件。


要创建新的身份命名空间，请执行以下操作：

1. 在数据收集界面中，选择 **[!UICONTROL 身份]** 从左边栏导航中。
1. 选择&#x200B;**[!UICONTROL 创建身份命名空间]**。
1. 提供 **[!UICONTROL 显示名称]** 之 `Luma CRM ID` 和 **[!UICONTROL 身份符号]** 值 `lumaCRMId`.
1. 选择 **[!UICONTROL 跨设备ID]**.
1. 选择&#x200B;**[!UICONTROL 创建]**。

   ![创建身份命名空间](assets/identity-create.png)




## 更新身份

当用户登录应用程序时，您希望同时更新标准身份（电子邮件）和自定义身份(Luma CRM ID)。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode项目导航器中找到 `func updateIdentities(emailAddress: String, crmId: String)` 函数实现。 将以下代码添加到函数中。

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   Identity.updateIdentities(with: identityMap)
   ```

   此代码：

   1. 创建空的 `IdentityMap` 对象。

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. 设置 `IdentityItem` 电子邮件和CRM ID的对象。

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. 添加这些 `IdentityItem` 对象到 `IdentityMap` 对象。

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. 发送 `IdentityItem` 对象，作为 `Identity.updateIdentities` 对Edge Network的API调用。

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. 导航到 **[!DNL Luma]** **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登录表]** 在Xcode项目导航器中，找到要在选择 **[!UICONTROL 登录]** 按钮。 添加以下代码：

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>您可以在单个中发送多个身份 `updateIdentities` 呼叫。 您还可以修改以前发送的身份。


## 删除身份

您可以使用 [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) 用于从存储的客户端身份映射中删除身份的API。 Identity扩展停止向Edge Network发送标识符。 使用此API不会从服务器端标识图中删除标识符。 请参阅 [查看身份图](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) 以了解有关身份图的详细信息。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL General]** > **[!UICONTROL MobileSDK]** 在Xcode项目导航器中，将以下代码添加到 `func removeIdentities(emailAddress: String, crmId: String)` 函数：

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登录表]** 在Xcode项目导航器中，找到要在选择 **[!UICONTROL 注销]** 按钮。 添加以下代码：

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## 使用保障进行验证

1. 查看 [设置说明](assurance.md) 并将模拟器或设备连接到Assurance。
1. 在Luma应用程序中
   1. 选择 **[!UICONTROL 主页]** 选项卡。
   1. 选择 <img src="assets/login.png" width="15" /> 图标。

      <img src="./assets/identity1.png" width="300">

   1. 提供电子邮件地址和CRM ID，或者
   1. 选择 <img src="assets/insert.png" width="15" /> 随机生成 **[!UICONTROL 电子邮件]** 和 **[!UICONTROL CRM ID]**.
   1. 选择 **[!UICONTROL 登录]**.

      <img src="./assets/identity2.png" width="300">


1. 在Assurance Web界面中查看 **[!UICONTROL Edge Identity更新身份]** 来自的事件 **[!UICONTROL com.adobe.griffon.mobile]** 供应商。
1. 选择事件并查看 **[!UICONTROL ACPExtensionEventData]** 对象。 您应该会看到已更新的身份。
   ![验证身份更新](assets/identity-validate-assurance.png)

## 使用身份图进行验证

一旦您完成 [Experience Platform课程](platform.md)，您便能够在Platforms身份图查看器中确认身份捕获：

1. 选择 **[!UICONTROL 身份]** 在数据收集UI中。
1. 选择 **[!UICONTROL 身份图]** 从顶部栏中。
1. 输入 `Luma CRM ID` 作为 **[!UICONTROL 身份命名空间]** 和您的CRM ID(例如， `24e620e255734d8489820e74f357b5c8`)作为 **[!UICONTROL 标识值]**.
1. 您会看到 **[!UICONTROL 身份]** 已列出。

   ![验证身份图](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>现在，您已设置应用程序以在Edge Network中和（设置后）使用Adobe Experience Platform更新身份。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[个人资料](profile.md)**
