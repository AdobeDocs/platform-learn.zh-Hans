---
title: 使用Mobile SDK在移动应用程序中收集身份数据
description: 了解如何在移动应用程序中收集身份数据。
feature: Mobile SDK,Identities
jira: KT-14633
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: 456c5437cec745f667435e97d21edfba1700750a
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---

# 收集身份数据

了解如何在移动应用程序中收集身份数据。

Adobe Experience Platform Identity服务可帮助您更好地了解客户及其行为。 这些服务跨设备和系统桥接身份，并允许您实时提供有影响力的个人数字体验。 身份字段和命名空间是将不同数据源连接在一起的粘合剂，可构建360度实时客户档案。

在文档中了解有关[Identity扩展](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/)和[Identity服务](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)的更多信息。

## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 设置自定义身份命名空间。
* 更新身份。
* 验证身份图。
* 获取ECID和其他身份。


## 设置自定义身份命名空间

身份命名空间是[身份服务](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)的组件，充当与身份相关的上下文的指示器。 例如，它们将`name@email.com`的值区分为电子邮件地址或`443522`区分为数字CRM ID。

>[!NOTE]
>
>Mobile SDK会在自己的命名空间中生成一个唯一标识，即在安装应用程序时名为Experience Cloud ID (ECID)。 此ECID存储在移动设备上的永久内存中，随每次点击一起发送。 当用户卸载应用程序或将Mobile SDK全局隐私状态设置为选择退出时，将会删除ECID。 在示例Luma应用程序中，您应该删除并重新安装该应用程序，以使用它自己的唯一ECID创建新配置文件。


要创建新的身份命名空间，请执行以下操作：

1. 在数据收集界面中，从左边栏导航中选择&#x200B;**[!UICONTROL 标识]**。
1. 选择&#x200B;**[!UICONTROL 创建身份标识命名空间]**。
1. 提供&#x200B;**[!UICONTROL 的]**&#x200B;显示名称`Luma CRM ID`和&#x200B;**[!UICONTROL 的]**&#x200B;标识符号`lumaCRMId`值。
1. 选择&#x200B;**[!UICONTROL 跨设备ID]**。
1. 选择&#x200B;**[!UICONTROL 创建]**。

   ![创建身份命名空间](assets/identity-create.png){zoomable="yes"}




## 更新身份

当用户登录应用程序时，您希望同时更新标准身份（电子邮件）和自定义身份(Luma CRM ID)。

>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**，并查找`func updateIdentities(emailAddress: String, crmId: String)`函数的实现。 将以下代码添加到函数中。

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

   1. 创建空的`IdentityMap`对象。

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. 为电子邮件和CRM ID设置`IdentityItem`对象。

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. 将这些`IdentityItem`对象添加到`IdentityMap`对象。

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. 将`IdentityItem`对象作为`Identity.updateIdentities` API调用的一部分发送到Edge Network。

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登录工作表]**，并找到要在选择&#x200B;**[!UICONTROL 登录]**&#x200B;按钮时执行的代码。 添加以下代码：

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!TAB Android]

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**，并查找`fun updateIdentities(emailAddress: String, crmId: String) `函数的实现。 将以下代码添加到函数中。

   ```kotlin
   // Set up identity map, add identities to map and update identities
   val identityMap = IdentityMap()
   
   val emailIdentity = IdentityItem(emailAddress, AuthenticatedState.AUTHENTICATED, true)
   val crmIdentity = IdentityItem(crmId, AuthenticatedState.AUTHENTICATED, true)
   identityMap.addItem(emailIdentity, "Email")
   identityMap.addItem(crmIdentity, "lumaCRMId")
   
   Identity.updateIdentities(identityMap)
   ```

   此代码：

   1. 创建空的`IdentityMap`对象。

      ```kotlin
      val identityMap = IdentityMap()
      ```

   1. 为电子邮件和CRM ID设置`IdentityItem`对象。

      ```kotlin
      val emailIdentity = IdentityItem(emailAddress, AuthenticatedState.AUTHENTICATED, true)
      val crmIdentity = IdentityItem(crmId, AuthenticatedState.AUTHENTICATED, true)
      ```

   1. 将这些`IdentityItem`对象添加到`IdentityMap`对象。

      ```kotlin
      identityMap.addItem(emailIdentity, "Email")
      identityMap.addItem(crmIdentity, "lumaCRMId")
      ```

   1. 将`IdentityItem`对象作为`Identity.updateIdentities` API调用的一部分发送到Edge Network。

      ```kotlin
      Identity.updateIdentities(identityMap)
      ```

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 视图]** > **[!UICONTROL LoginSheet.kt]**，并找到要在选择&#x200B;**[!UICONTROL Login]**&#x200B;按钮时执行的代码。 添加以下代码：

   ```kotlin
   // Update identities
   MobileSDK.shared.updateIdentities(
      MobileSDK.shared.currentEmailId.value,
      MobileSDK.shared.currentCRMId.value
   )                             
   ```


>[!ENDTABS]



>[!NOTE]
>
>您可以在单个`updateIdentities`调用中发送多个身份。 您还可以修改以前发送的身份。


## 删除身份

您可以使用[`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) API从存储的客户端标识映射中删除标识。 Identity扩展停止向Edge Network发送标识符。 使用此API不会从服务器端标识图中删除标识符。 有关身份图的详细信息，请参阅[查看身份图](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/view-identity-graphs)。


>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**，并将以下代码添加到`func removeIdentities(emailAddress: String, crmId: String)`函数：

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "b642b4217b34b1e8d3bd915fc65c4452"
   ```

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登录工作表]**，并找到要在选择&#x200B;**[!UICONTROL 注销]**&#x200B;按钮时执行的代码。 添加以下代码：

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```

>[!TAB Android]

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**，并将以下代码添加到`fun removeIdentities(emailAddress: String, crmId: String)`函数：

   ```kotlin
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(IdentityItem(emailAddress), "Email")
   Identity.removeIdentity(IdentityItem(crmId), "lumaCRMId")
   currentEmailId.value = "testUser@gmail.com"
   currentCRMId.value = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1.在Android Studio导航器中导航到&#x200B;**[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 视图]** > **[!UICONTROL LoginSheet.kt]**，并找到要在选择&#x200B;**[!UICONTROL 注销]**&#x200B;按钮时执行的代码。 添加以下代码：

```kotlin
// Remove identities
MobileSDK.shared.removeIdentities(
   MobileSDK.shared.currentEmailId.value,
   MobileSDK.shared.currentCRMId.value
)              
```


>[!ENDTABS]

## 使用 Assurance 进行验证

1. 查看[设置说明](assurance.md#connecting-to-a-session)部分以将模拟器或设备连接到Assurance。
1. 在Luma应用程序中
   1. 选择&#x200B;**[!UICONTROL 主页]**&#x200B;选项卡，并将Assurance图标向左移动。
   1. 从右上角选择![用户](/help/assets/icons/User.svg)图标。

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/identity1.png" width="300">

>[!TAB Android]

<img src="./assets/identity1-android.png" width="300">

>[!ENDTABS]

在&#x200B;**[!UICONTROL 标识]**&#x200B;屏幕中：

1. 提供电子邮件地址和CRM ID，或者
1. 选择&#x200B;**[!UICONTROL A |]** (iOS)或&#x200B;**[!UICONTROL 生成随机电子邮件]** (Android)以随机生成&#x200B;**[!UICONTROL 电子邮件]**&#x200B;和&#x200B;**[!UICONTROL CRM ID]**。
1. 选择&#x200B;**[!UICONTROL 登录]**。

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/identity2.png" width="300">

>[!TAB Android]

<img src="./assets/identity2-android.png" width="300">


>[!ENDTABS]

返回Assurance：

1. 在Assurance Web界面中检查&#x200B;**[!UICONTROL com.adobe.griffon.mobile]**&#x200B;供应商的&#x200B;**[!UICONTROL Edge标识更新标识]**&#x200B;事件。
1. 选择事件并查看&#x200B;**[!UICONTROL ACPExtensionEventData]**&#x200B;对象中的数据。 您应该会看到已更新的身份。
   ![验证标识更新](assets/identity-validate-assurance.png){zoomable="yes"}

## 使用身份图进行验证

完成[Experience Platform课程](platform.md)中的步骤后，便可以在Experience Platform身份图查看器中确认身份捕获：

1. 在数据收集UI中选择&#x200B;**[!UICONTROL 标识]**。
1. 从顶部栏中选择&#x200B;**[!UICONTROL 标识图]**。
1. 输入`Luma CRM ID`作为&#x200B;**[!UICONTROL 身份命名空间]**，输入CRM ID （例如`24e620e255734d8489820e74f357b5c8`）作为&#x200B;**[!UICONTROL 身份值]**。
1. 您看到列出了&#x200B;**[!UICONTROL 标识]**。

   ![验证身份图](assets/identity-validate-graph.png){zoomable="yes"}

>[!INFO]
>
>应用程序中没有任何代码可重置ECID。 您只能通过卸载并重新安装应用程序来重置ECID（并使用新的ECID有效地创建新的配置文件）。 要实施标识符的重置，请参阅[`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities)和[`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities) API调用。 请注意，当您使用推送通知标识符时（请参阅[发送推送通知](journey-optimizer-push.md)），该标识符将成为设备上的另一个“粘性”配置文件标识符。


>[!SUCCESS]
>
>现在，您已设置应用程序以在Edge Network中和（设置后）使用Adobe Experience Platform更新身份。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有任何疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享这些内容

下一步： **[收集配置文件数据](profile.md)**
