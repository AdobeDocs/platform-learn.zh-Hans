---
title: 使用Target执行A/B测试
description: 了解如何在移动应用程序中通过Platform Mobile SDK和Adobe Target使用Target A/B测试。
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
hide: true
source-git-commit: 56323387deae4a977a6410f9b69db951be37059f
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 2%

---


# 使用Target执行A/B测试

了解如何使用Platform Mobile SDK和Adobe Target在移动应用程序中执行A/B测试。

Target提供了您必须定制和个性化客户体验的所有功能。 Target可帮助您最大限度地提高网站和移动网站、应用程序、社交媒体和其他数字渠道的收入。 本教程重点介绍Target的A/B测试功能。 请参阅 [A/B测试概述](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) 以了解更多信息。

在使用Target执行A/B测试之前，您必须确保已进行适当的配置和集成。

>[!NOTE]
>
>本课程是可选的，仅适用于希望执行A/B测试的Adobe Target用户。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 通过权限、正确配置的角色、工作区和属性访问Adobe Target Premium，如所述 [此处](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=zh-Hans).
您也应该能够使用Target Standard，但本教程使用了一些Target Premium特有的高级概念（例如Target属性）。


## 学习目标

在本课程中，您将执行以下操作

* 更新Target集成的Edge配置。
* 使用Journey Optimizer - Decisioning扩展更新您的标记属性。
* 更新您的架构以捕获建议事件。
* 验证Assurance中的设置。
* 在Target中创建简单的A/B测试。
* 更新您的应用程序以包含Optimizer扩展。
* 在应用程序中实施A/B测试。
* 在Assurance中验证实施。


## 设置您的应用程序

>[!TIP]
>
>如果您已将应用程序设置为 [Journey Optimizer优惠](journey-optimizer-offers.md) 教程，您可以跳过 [安装Adobe Journey Optimizer - Decisioning标记扩展](#install-adobe-journey-optimizer---decisioning-tags-extension) 和 [更新您的架构](#update-your-schema).

### 更新Edge配置

要确保将从您的移动应用程序发送到边缘网络的数据转发到Adobe Target，您必须更新Experience Edge配置。

1. 在数据收集UI中，选择 **[!UICONTROL 数据流]**，并选择您的数据流，例如 **[!UICONTROL Luma移动应用程序]**.
1. 选择 **[!UICONTROL 添加服务]** 并选择 **[!UICONTROL Adobe Target]** 从 **[!UICONTROL 服务]** 列表。
1. 输入目标 **[!UICONTROL 资产令牌]** 要用于此集成的值。

   您可以在Target UI中的以下位置找到您的属性： **[!UICONTROL 管理]** > **[!UICONTROL 属性]**. 选择 ![代码](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) 用于显示要使用的资产的资产令牌。 资产令牌的格式如下 `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`；必须只输入值 `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![向数据流添加Target](assets/edge-datastream-target.png)


### 安装Adobe Journey Optimizer - Decisioning标记扩展

1. 导航到 **[!UICONTROL 标记]** 并找到您的移动标记资产并打开该资产。
1. 选择 **[!UICONTROL 扩展]**.
1. 选择 **[!UICONTROL 目录]**.
1. 搜索 **[!UICONTROL Adobe Journey Optimizer - Decisioning]** 扩展。
1. 安装扩展。 该扩展不需要其他配置。

   ![Add Decisioning扩展](assets/tag-add-decisioning-extension.png)


### 更新您的架构

1. 导航到数据收集UI，然后从左边栏中选择架构。
1. 选择 **[!UICONTROL 浏览]** 从顶部栏中。
1. 选择您的架构以将其打开。
1. 在架构编辑器中，选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加]** 旁边 **[!UICONTROL 字段组]**.
1. 在添加字段组对话框中，搜索 `proposition`，选择 **[!UICONTROL 体验事件 — 建议交互]** 并选择 **[!UICONTROL 添加字段组]**.
   ![建议](assets/schema-fieldgroup-proposition.png)
1. 要保存对架构所做的更改，请选择 **[!UICONTROL 保存]** .


### 验证Assurance中的设置

要在Assurance中验证设置，请执行以下操作：

1. 转到Assurance UI。
1. 选择 **[!UICONTROL 配置]** 在左边栏中选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 旁边 **[!UICONTROL 验证设置]** 下 **[!UICONTROL Adobe Journey Optimizer决策]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 选择 **[!UICONTROL 验证设置]** 在左边栏中。 数据流设置以及应用程序中的SDK设置均已验证。
   ![AJO决策验证](assets/ajo-decisioning-validation.png)

## 创建 A/B 测试

1. 在Target UI中，选择 **[!UICONTROL 活动]** 从顶部栏中。
1. 选择 **[!UICONTROL 创建活动]** 和 **[!UICONTROL A/B测试]** 从上下文菜单中。
1. 在 **[!UICONTROL 创建A/B测试活动]** 对话框，选择 **[!UICONTROL 移动设备]** 作为 **[!UICONTROL 类型]**，从中选择工作区 **[!UICONTROL 选择工作区]** ，并从中选择您的资产 **[!UICONTROL 选择属性]** 列表。
1. 选择&#x200B;**[!UICONTROL 创建]**。
   ![创建Target活动](assets/target-create-activity1.png)

1. 在 **[!UICONTROL 无标题活动]** 屏幕，位于 **[!UICONTROL 体验]** 步骤：

   1. 输入 `luma-mobileapp-abtest` 在 **[!UICONTROL 选择位置]** 下 **[!UICONTROL 位置1]**.
   1. 选择 ![Chrevron下降](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) 旁边 **[!UICONTROL 默认内容]** 并选择 **[!UICONTROL 创建JSON选件]** 从上下文菜单中。
   1. 将以下JSON复制到 **[!UICONTROL 输入有效的JSON对象]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. 选择 **[!UICONTROL +添加体验]**.

      ![体验A](assets/target-create-activity-experienceA.png)

   1. 对体验B重复步骤b和c，而是使用以下JSON：

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. 选择&#x200B;**[!UICONTROL 下一步]**。

      ![体验 B](assets/target-create-activity-experienceB.png)

1. 在 **[!UICONTROL 定位]** 步骤，查看A/B测试的设置。 默认情况下，这两个选件会平均分配到所有访客。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

   ![设定目标](assets/taget-targeting.png)

1. 在 **[!UICONTROL 目标和设置]** 步骤：

   1. 将无标题活动重命名，例如 `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. 输入 **[!UICONTROL 目标]** 例如，用于您的A/B测试 `A/B Test for Luma mobile app tutorial`.
   1. 选择 **[!UICONTROL 转化]**， **[!UICONTROL 已单击mbox]** 在 **[!UICONTROL 目标量度]** > **[!UICONTROL 我的主要目标]** 并输入您的位置(mbox)名称，例如 `luma-mobileapp-abtest`.
   1. 选择 **[!UICONTROL 保存并关闭]**.

      ![目标设置](assets/target-goals.png)

1. 返回 **[!UICONTROL 所有活动]** 屏幕：

   1. 选择 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) 您的活动。
   1. 选择 ![播放](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL 激活]** 以激活A/B测试。

   ![激活](assets/target-activate.png)


## 在应用程序中实施Target

如前面的课程中所述，安装移动标记扩展仅提供配置。 接下来，您必须安装并注册优化SDK。 如果这些步骤不明确，请查阅 [安装SDK](install-sdks.md) 部分。

>[!NOTE]
>
>如果您已完成 [安装SDK](install-sdks.md) 部分，则该SDK已安装，您可以跳过此步骤。
>

1. 在Xcode中，确保 [AEP优化](https://github.com/adobe/aepsdk-messaging-ios.git) 会添加到包依赖关系中的包列表中。 请参阅 [Swift包管理器](install-sdks.md#swift-package-manager).
1. 导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** 在Xcode项目导航器中。
1. 确保 `AEPOptimize` 是导入列表的一部分。

   `import AEPOptimize`

1. 确保 `Optimize.self` 是您注册的扩展数组的一部分。

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

1. 导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 实用工具]** > **[!UICONTROL MobileSDK]** 在Xcode项目导航器中。 查找 ` func updatePropositionAT(ecid: String, location: String) async` 函数。 添加以下代码：

   ```swift
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   此函数

   * 设置XDM词典 `xdmData`，包含ECID以标识必须提供A/B测试的配置文件，并且
   * 定义 `decisionScope`，提供A/B测试的位置数组。

   然后，函数调用两个API： [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  和 [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). 这些函数清除任何缓存的建议并更新此用户档案的建议。

1. 导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 视图]** > **[!UICONTROL 个性化]** > **[!UICONTROL TargetOffersView]** 在Xcode项目导航器中。 查找 `func getPropositionAT(location: String) async` 函数并检查此函数的代码。 此函数最重要的部分是  [`Optimize.getPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#getpropositions) API调用，其中
   * 根据决策范围（即您在A/B测试中定义的位置）检索当前用户档案的建议，并且
   * 在应用程序中正确显示的内容中将结果解包。

1. 仍在使用 **[!UICONTROL TargetOffersView]**，查找f`unc updatePropositions(location: String) async` 函数并添加以下代码：

   ```swift
       Task {
           await self.updatePropositionAT(
               ecid: currentEcid,
               location: location
           )
       }
       try? await Task.sleep(seconds: 2.0)
       Task {
           await self.getPropositionAT(
               location: location
           )
       }
   ```

   此代码确保您更新建议，然后使用步骤5和步骤6中描述的函数检索结果。


## 使用应用程序进行验证

1. 在设备或模拟器中打开您的应用程序。

1. 转到 **[!UICONTROL 个性化]** 选项卡。

1. 选择 **[!UICONTROL 边缘个性化]**.

1. 向下滚动到底部，您会看到在A/B测试中定义的两个选件之一显示在 **[!UICONTROL TARGET]** 磁贴。

   <img src="assets/target-app-offer.png" width="300">


## 在Assurance中验证实施

要在保证中验证A/B测试，请执行以下操作：

1. 转到Assurance UI。
1. 选择 **[!UICONTROL 配置]** 在左边栏中选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 旁边 **[!UICONTROL 审阅和模拟]** 下 **[!UICONTROL Adobe Journey Optimizer决策]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 选择 **[!UICONTROL 审阅和模拟]** 在左边栏中。 数据流设置以及应用程序中的SDK设置均已验证。
1. 选择 **[!UICONTROL 请求]** 在顶栏里。 您看到您的 **[!UICONTROL Target]** 请求。
   ![AJO决策验证](assets/assurance-decisioning-requests.png)

1. 您可以浏览“模拟”和“事件列表”选项卡，以进一步了解功能检查您的Target选件设置。

## 后续步骤

现在，您应该拥有所有工具，以便开始向Luma应用程序添加更多A/B测试或其他Target活动（例如体验定位、多变量测试）（如果相关且适用）。

>[!SUCCESS]
>
>您已为应用程序启用A/B测试，并显示了使用Adobe Target和适用于Adobe Experience Platform Mobile SDK的Adobe Journey Optimizer - Decisioning扩展的A/B测试的结果。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[结论和后续步骤](conclusion.md)**
