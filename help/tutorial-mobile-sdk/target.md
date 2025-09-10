---
title: 使用Target和Platform Mobile SDK在移动设备应用程序中执行A/B测试
description: 了解如何在移动应用程序中通过Platform Mobile SDK和Adobe Target使用Target A/B测试。
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
jira: KT-14641
exl-id: 87546baa-2d8a-4cce-b531-bec3782d2e90
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '2102'
ht-degree: 1%

---

# 使用Adobe Target进行优化和个性化

了解如何使用Platform Mobile SDK和Adobe Target优化和个性化移动应用程序中的体验。

Target提供了您必须定制和个性化客户体验的所有功能。 Target可帮助您最大限度地提高网站和移动网站、应用程序、社交媒体和其他数字渠道的收入。 Target可以执行A/B测试、多变量测试、推荐产品和内容、定位内容、使用AI自动个性化内容等等。 本课程重点介绍Target的A/B测试功能。 有关详细信息，请参阅[A/B测试概述](https://experienceleague.adobe.com/en/docs/target/using/activities/abtest/test-ab)。

![架构](assets/architecture-at.png){zoomable="yes"}

在使用Target执行A/B测试之前，您必须确保已进行适当的配置和集成。

>[!NOTE]
>
>本课程是可选的，仅适用于希望执行A/B测试的Adobe Target用户。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 通过[权限、正确配置的角色、工作区和属性](https://experienceleague.adobe.com/en/docs/target/using/administer/manage-users/enterprise/property-channel)访问Adobe Target。


## 学习目标

在本课程中，您将执行以下操作：

* 更新数据流以进行Target集成。
* 使用Offer Decisioning和Target扩展更新您的标记属性。
* 更新您的架构以捕获建议事件。
* 验证Assurance中的设置。
* 在Target中创建简单的A/B测试。
* 更新您的应用程序以注册Optimizer扩展。
* 在应用程序中实施A/B测试。
* 验证Assurance中的实施。


## 设置

>[!TIP]
>
>如果您已将应用程序设置为[Journey Optimizer选件](journey-optimizer-offers.md)课程的一部分，则您可能已执行了此设置部分中的某些步骤。

### 更新数据流配置

#### Adobe Target

要确保将从您的移动应用程序发送到Experience Platform Edge Network的数据转发到Adobe Target，您必须更新数据流配置。

1. 在数据收集UI中，选择&#x200B;**[!UICONTROL 数据流]**，然后选择您的数据流，例如&#x200B;**[!DNL Luma Mobile App]**。
1. 选择&#x200B;**[!UICONTROL 添加服务]**&#x200B;并从&#x200B;**[!UICONTROL 服务]**&#x200B;列表中选择&#x200B;**[!UICONTROL Adobe Target]**。
1. 如果您是Target Premium客户并且希望使用资产令牌，请输入要用于此集成的Target **[!UICONTROL 资产令牌]**&#x200B;值。 Target Standard用户可以跳过此步骤。

   您可以在Target UI的&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 属性]**&#x200B;中找到您的属性。 选择![代码](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg)以显示要使用的属性的属性令牌。 属性令牌的格式为`"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`；您必须仅输入值`xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`。

   或者，您可以指定Target环境ID。 Target使用环境来组织站点和预生产环境，以便轻松管理和单独报告。 预设环境包括生产、暂存和开发。 有关详细信息，请参阅[环境](https://experienceleague.adobe.com/en/docs/target/using/administer/environments)和[目标环境ID](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/implement-web-sdk/applications-setup/setup-target)。

   或者，您可以指定Target第三方ID命名空间，以支持在身份命名空间上同步配置文件（例如CRM ID）。 有关详细信息，请参阅[目标第三方ID命名空间](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/implement-web-sdk/applications-setup/setup-target)。

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![将目标添加到数据流](assets/edge-datastream-target.png){zoomable="yes"}


#### Adobe Journey Optimizer

要确保将从您的移动应用程序发送到Edge Network的数据转发到Journey Optimizer — 决策管理，请更新您的数据流配置。

1. 在数据收集UI中，选择&#x200B;**[!UICONTROL 数据流]**，然后选择您的数据流，例如&#x200B;**[!DNL Luma Mobile App]**。
1. 为![Experience Platform](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)选择&#x200B;**[!UICONTROL 更多]**，然后从上下文菜单中选择![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 编辑]**。
1. 在&#x200B;**[!UICONTROL 数据流]** > ![文件夹](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**&#x200B;屏幕中，确保已选择&#x200B;**[!UICONTROL Offer Decisioning]**、**[!UICONTROL Edge分段]**&#x200B;和&#x200B;**[!UICONTROL Personalization目标]**。 如果您还参加了Journey Optimizer课程，请选择&#x200B;**[!UICONTROL Adobe Journey Optimizer]**。 有关详细信息，请参阅[Adobe Experience Platform设置](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)。
1. 要保存数据流配置，请选择&#x200B;**[!UICONTROL 保存]** 。

   ![AEP数据流配置](assets/datastream-aep-configuration-target.png){zoomable="yes"}


### 安装Offer Decisioning和Target标记扩展

尽管本课程与Target中的A/B测试有关，但测试的结果会被视为选件，并使用Adobe Offer Decisioning和Target标记扩展在Adobe基础架构中实施。 该扩展会处理Journey Optimizer和Target提供的两个选件。

1. 导航到&#x200B;**[!UICONTROL 标记]**，找到您的移动标记属性，然后打开该属性。
1. 选择&#x200B;**[!UICONTROL 扩展]**。
1. 选择&#x200B;**[!UICONTROL 目录]**。
1. 搜索&#x200B;**[!UICONTROL Offer Decisioning和Target]**&#x200B;扩展。
1. 安装扩展。 该扩展不需要其他配置。

   ![添加Offer Decisioning和Target扩展](assets/tag-add-decisioning-extension.png){zoomable="yes"}



### 更新您的架构

1. 导航到数据收集界面，然后从左边栏中选择&#x200B;**[!UICONTROL 架构]**。
1. 从顶部栏中选择&#x200B;**[!UICONTROL 浏览]**。
1. 选择您的架构以将其打开。
1. 在架构编辑器中，选择![字段组](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)旁边的&#x200B;**[!UICONTROL 添加]** **[!UICONTROL 添加]**。
1. 在&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框中，搜索`proposition`，选择&#x200B;**[!UICONTROL 体验事件 — 建议交互]**，然后选择&#x200B;**[!UICONTROL 添加字段组]**。
   ![建议](assets/schema-fieldgroup-proposition.png){zoomable="yes"}
1. 若要保存对架构所做的更改，请选择&#x200B;**[!UICONTROL 保存]**。


### 验证Assurance中的设置

要验证Assurance中的设置，请执行以下操作：

1. 转到Assurance UI。
1. 在左边栏中选择&#x200B;**[!UICONTROL 配置]**，然后选择![OFFER DECISIONING和TARGET](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)下的&#x200B;**[!UICONTROL 验证设置]**&#x200B;旁的&#x200B;**[!UICONTROL 添加]**。
1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 在左边栏中选择&#x200B;**[!UICONTROL 验证设置]**。 您的应用程序中的数据流设置和SDK设置均已验证。
   ![AJO Decisioning验证](assets/ajo-decisioning-validation.png){zoomable="yes"}

## 创建A/B测试

您可以创建多种类型的活动，并在Adobe Target中实施这些活动，如简介中所述。 在本课程中，您将实施A/B测试。

1. 在Target UI中，从顶部栏中选择&#x200B;**[!UICONTROL 活动]**。
1. 从上下文菜单中选择&#x200B;**[!UICONTROL 创建活动]**&#x200B;和&#x200B;**[!UICONTROL A/B测试]**。
1. 在&#x200B;**[!UICONTROL 创建A/B测试活动]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 移动设备]**&#x200B;作为&#x200B;**[!UICONTROL 类型]**，从&#x200B;**[!UICONTROL 选择Workspace]**&#x200B;列表中选择一个工作区。 如果您是Target Premium客户并在数据流中指定了资产令牌，请从&#x200B;**[!UICONTROL 选择资产]**&#x200B;列表中选择您的资产。
1. 选择&#x200B;**[!UICONTROL 创建]**。
   ![创建Target活动](assets/target-create-activity1.png){zoomable="yes"}

1. 在&#x200B;**[!UICONTROL 无标题的活动]**&#x200B;屏幕中，位于&#x200B;**[!UICONTROL 体验]**&#x200B;步骤：

   1. 在`luma-mobileapp-abtest`位置1 **[!UICONTROL 下的]**&#x200B;选择位置&#x200B;**[!UICONTROL 中输入]**。 此位置名称（通常称为mbox）稍后将在应用程序实施中使用。
   1. 选择![内容](/help/assets/icons/More.svg)旁边的&#x200B;**[!UICONTROL 更多]**，然后从上下文菜单中选择&#x200B;**[!UICONTROL 创建JSON选件]**。
   1. 在&#x200B;**[!UICONTROL 创建JSON选件]**&#x200B;对话框中，粘贴以下JSON。

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

      ![体验A](assets/target-create-activity-experienceA.png){zoomable="yes"}

      选择&#x200B;**[!UICONTROL 创建]**。

   1. 选择&#x200B;**[!UICONTROL 体验]**&#x200B;旁边的&#x200B;**[!UICONTROL +]**&#x200B;以添加&#x200B;**[!UICONTROL 体验B]**。



   1. 对体验B重复步骤b和c，但改用`Aim Analog Watch`作为标题并粘贴以下JSON：

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```


1. 在&#x200B;**[!DNL Targeting]**&#x200B;步骤中，查看A/B测试的设置。 默认情况下，这两个选件会平均分配给所有访客。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

   ![定位](assets/target-targeting.png){zoomable="yes"}

1. 在&#x200B;**[!UICONTROL 目标和设置]**&#x200B;步骤中：

   1. 将无标题活动重命名，例如`Luma Mobile SDK Tutorial - A/B Test Example`。
   1. 输入A/B测试的&#x200B;**[!UICONTROL 目标]**，例如`A/B Test for Luma mobile app tutorial`。
   1. 选择&#x200B;**[!UICONTROL 转化]**，**[!UICONTROL 在]**&#x200B;目标量度&#x200B;**[!UICONTROL >]**&#x200B;我的主要目标&#x200B;**[!UICONTROL 拼贴中查看了mbox]**，并输入您的位置(mbox)名称，例如`luma-mobileapp-abtest`。
   1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。

      ![目标设置](assets/target-goals.png){zoomable="yes"}

1. 返回&#x200B;**[!UICONTROL 所有活动]**&#x200B;屏幕：

   1. 在活动中选择![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)。
   1. 选择![播放](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL 激活]**&#x200B;以激活您的A/B测试。

   ![激活](assets/target-activate.png){zoomable="yes"}


## 在应用程序中实施Target

如前面的课程中所述，安装移动标记扩展仅提供配置。 接下来，您必须安装并注册优化SDK。 如果未清除这些步骤，请查看[安装SDK](install-sdks.md)部分。

>[!NOTE]
>
>如果您已完成[安装SDK](install-sdks.md)部分，则表明已安装SDK，您可以跳过此步骤。
>

>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode中，确保将[AEP Optimize](https://github.com/adobe/aepsdk-messaging-ios)添加到包依赖关系中的包列表中。 请参阅[Swift包管理器](install-sdks.md#swift-package-manager)。
1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]**。
1. 确保`AEPOptimize`是导入列表的一部分。

   `import AEPOptimize`

1. 请确保`Optimize.self`是正在注册的扩展数组的一部分。

   ```swift
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
   ```

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]**。 查找` func updatePropositionAT(ecid: String, location: String) async`函数。 添加以下代码：

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData) { data, error in
           if let error = error {
               Logger.aepMobileSDK.error("MobileSDK - updatePropositionsAT: Error updating propositions: \(error.localizedDescription)")
           }
       }
   }
   ```

   此函数：

   * 设置XDM字典`xdmData`，该字典包含ECID以标识必须提供A/B测试的配置文件，并且
   * 定义一个`decisionScope`，一个位置数组，用于表示A/B测试。

   然后，该函数调用两个API： [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions)和[`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions)。 这些函数清除任何缓存的建议并更新此用户档案的建议。 此上下文中的建议是从Target活动（您的A/B测试）中选择并且您在[创建A/B测试](#create-an-ab-test)中定义的体验（选件）。

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Personalization]** > **[!DNL TargetOffersView]**。 查找`func onPropositionsUpdateAT(location: String) async {`函数并检查此函数的代码。 此函数最重要的部分是[`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) API调用，其中：
   * 根据决策范围（即您在A/B测试中定义的位置）检索当前用户档案的建议，
   * 从建议中检索优惠，
   * 解包选件的内容，以便该内容可以在应用程序中正确显示，并且
   * 触发对选件的`displayed()`操作，该操作会将事件发送回Platform Edge Network，通知选件已显示。

1. 仍然在&#x200B;**[!DNL TargetOffersView]**&#x200B;中，将以下代码添加到`.onFirstAppear`修饰符中。 此代码确保用于更新优惠的回调仅注册一次。

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateAT(location: location)
   }
   ```

1. 仍然在&#x200B;**[!DNL TargetOffersView]**&#x200B;中，将以下代码添加到`.task`修饰符中。 刷新视图后，此代码会更新选件。

   ```swift
   // Clear and update offers
   await self.updatePropositionsAT(ecid: currentEcid, location: location)
   ```

>[!TAB Android]

1. 在Android Studio中，确保[aepsdk-optimize-android](https://github.com/adobe/aepsdk-optimize-android)是&#x200B;**[!UICONTROL Android]** **[!UICONTROL ChevronDown]** > ![Gradle脚本](/help/assets/icons/ChevronDown.svg)中&#x200B;**[!UICONTROL build.gradle.kts]**&#x200B;的依赖项的一部分。 查看[Gradle](install-sdks.md#gradle)。
1. 在Android Studio导航器中导航到&#x200B;**[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL MainActivity]**。
1. 确保`Optimize`是导入列表的一部分。

   ```kotlin
   import com.adobe.marketing.mobile.optimize.Optimize
   ```

1. 请确保`Optimize.EXTENSION`是正在注册的扩展数组的一部分。

   ```kotlin
   val extensions = listOf(
      Identity.EXTENSION,
      Lifecycle.EXTENSION,
      Signal.EXTENSION,
      Edge.EXTENSION,
      Consent.EXTENSION,
      UserProfile.EXTENSION,
      Places.EXTENSION,
      Messaging.EXTENSION,
      Optimize.EXTENSION,
      Assurance.EXTENSION
   )
   ```

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!DNL models]** > **[!UICONTROL MobileSDK]**。 查找` suspend fun updatePropositionsAT(ecid: String, location: String)`函数。 添加以下代码：

   ```kotlin
   // set up the XDM dictionary, define decision scope and call update proposition API
   withContext(Dispatchers.IO) {
       val ecidMap = mapOf("ECID" to mapOf("id" to ecid, "primary" to true))
       val identityMap = mapOf("identityMap" to ecidMap)
       val xdmData = mapOf("xdm" to identityMap)
       val decisionScope = DecisionScope(location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(listOf(decisionScope), xdmData, null, object :
           AdobeCallbackWithOptimizeError<MutableMap<DecisionScope?, OptimizeProposition?>?> {
           override fun fail(optimizeError: AEPOptimizeError?) {
               val responseError = optimizeError
               Log.i("MobileSDK", "updatePropositionsAT error: ${responseError}")
           }
           override fun call(propositionsMap: MutableMap<DecisionScope?, OptimizeProposition?>?) {
               val responseMap = propositionsMap
               Log.i("MobileSDK", "updatePropositionsOD call: ${responseMap}")
           }
       })
   }
   ```

   此函数：

   * 设置XDM字典`xdmData`，该字典包含ECID以标识必须提供A/B测试的配置文件，并且
   * 定义一个`decisionScope`，一个位置数组，用于表示A/B测试。

   然后，该函数调用两个API： [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions)和[`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions)。 这些函数清除任何缓存的建议并更新此用户档案的建议。 此上下文中的建议是从Target活动（您的A/B测试）中选择并且您在[创建A/B测试](#create-an-ab-test)中定义的体验（选件）。

1. 在Android Studio导航器中导航到&#x200B;**[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!DNL views]** > **[!DNL TargetOffers.kt]**。 查找`fun onPropositionsUpdateAT(location: String): List<OfferItem>`函数并检查此函数的代码。 此函数最重要的部分是[`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) API调用，其中：
   * 根据决策范围（即您在A/B测试中定义的位置）检索当前用户档案的建议，
   * 从建议中检索优惠，
   * 解包选件的内容，以便该内容可以在应用程序中正确显示，并且
   * 返回选件。

1. 仍在&#x200B;**[!DNL TargetOffers.kt]**&#x200B;中，添加`LaunchedEffect`函数以确保在启动Personalization选项卡时刷新选件。

   ```kotlin
   // recompose the view when the number of received offers changes
   LaunchedEffect(offersAT.count()) {
       updatePropositionsAT(currentEcid, MobileSDK.shared.targetLocation.value)
       offersAT = onPropositionsUpdateAT(MobileSDK.shared.targetLocation.value)
   }
   ```

>[!ENDTABS]

您可以在个性化查询请求中将其他Target参数（如mbox、配置文件、产品或订单参数）发送到Experience Edge网络，方法是在调用[`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions) API时将它们添加到数据字典中。 有关详细信息[目标参数](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/#target-parameters)，请参阅。



## 使用应用程序进行验证

>[!BEGINTABS]

>[!TAB iOS]

1. 使用![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)，在模拟器中或在Xcode的物理设备上重建并运行应用程序。

1. 转到&#x200B;**[!UICONTROL Personalization]**&#x200B;选项卡。

1. 向下滚动到底部，您会看到&#x200B;**[!UICONTROL TARGET]**&#x200B;图块中显示您在A/B测试中定义的两个选件之一。

   <img src="assets/target-app-offer.png" width="300">


>[!TAB Android]

1. 使用![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)，在模拟器中或在Android Studio的物理设备上重建并运行应用程序。

1. 转到 **[!DNL Personalization]** 选项卡。

1. 您会在&#x200B;**[!UICONTROL TARGET]**&#x200B;图块的底部框中看到您在A/B测试中定义的两个选件之一。

   <img src="assets/ajo-app-offers-android.png" width="300">


>[!ENDTABS]

## 验证Assurance中的实施

要在Assurance中验证A/B测试，请执行以下操作：

1. 查看[设置说明](assurance.md#connecting-to-a-session)部分以将模拟器或设备连接到Assurance。
1. 在左边栏中选择&#x200B;**[!UICONTROL 配置]**，然后选择![OFFER DECISIONING和TARGET](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)下的&#x200B;**[!UICONTROL 审阅和模拟]**&#x200B;旁边的&#x200B;**[!UICONTROL 添加]**。
1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 在左边栏中选择&#x200B;**[!UICONTROL 查看和模拟]**。 您的应用程序中的数据流设置和SDK设置均已验证。
1. 选择顶部栏中的&#x200B;**[!UICONTROL 请求]**。 您会看到您的&#x200B;**[!DNL Target]**请求。
   ![AJO Decisioning验证](assets/assurance-decisioning-requests.png){zoomable="yes"}

1. 您可以浏览&#x200B;**[!UICONTROL 模拟]**&#x200B;和&#x200B;**[!UICONTROL 事件列表]**&#x200B;选项卡，以了解有助于验证Target选件设置的其他功能。

## 后续步骤

现在，您应该拥有所有工具，能够根据相关情况和适用情况，开始向应用程序添加更多A/B测试或其他Target活动（例如体验定位、多变量测试）。 在[GitHub存储库中，提供了有关优化扩展](https://github.com/adobe/aepsdk-optimize-ios)的更深入的信息，您还可以在该存储库中找到指向有关如何跟踪Adobe Target产品的专用[教程](https://opensource.adobe.com/aepsdk-optimize-ios/#/tutorials/README)的链接。

>[!SUCCESS]
>
>您已为A/B测试启用应用程序，并在Adobe Experience Platform Mobile SDK中使用Offer Decisioning和Target扩展显示了A/B测试的结果。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有任何疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享这些内容。

下一步： **[结论和后续步骤](conclusion.md)**
