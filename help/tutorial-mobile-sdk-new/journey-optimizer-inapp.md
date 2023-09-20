---
title: 创建和发送应用程序内消息
description: 了解如何使用Platform Mobile SDK和Adobe Journey Optimizer创建应用程序内消息并将其发送到移动应用程序。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 4%

---

# 创建和发送应用程序内消息

了解如何使用Experience PlatformMobile SDK和Journey Optimizer为移动应用程序创建应用程序内消息。

Journey Optimizer允许您创建营销活动，以将应用程序内消息发送给目标受众。 Journey Optimizer中的营销活动用于通过各种渠道向特定受众投放一次性内容。 借助营销活动，可同时执行诸多操作：立即执行或根据指定计划执行。使用历程时(请参阅 [Journey Optimizer推送通知](journey-optimizer-push.md) 课程)，操作将按顺序执行。

![架构](assets/architecture-ajo.png)

在使用Journey Optimizer发送应用程序内消息之前，必须确保进行适当的配置和集成。 要了解Journey Optimizer中的应用程序内消息传送数据流，请参阅 [文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>本课程是可选的，仅适用于希望发送应用程序内消息的Journey Optimizer用户。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 为Adobe Experience Platform设置应用程序。
* 对Journey Optimizer的访问权限和足够的权限，如所述 [此处](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 此外，您需要具有足够的权限才能使用以下Journey Optimizer功能。
   * 管理营销活动。
* 具有创建证书、标识符和密钥的足够访问权限的付费Apple开发人员帐户。
* 用于测试的物理iOS设备或模拟器。


## 学习目标

在本课程中，您将执行以下操作

* 向Apple推送通知服务(APN)注册应用程序ID。
* 在AJO中创建应用程序表面。
* 安装和配置Journey Optimizer标记扩展。
* 更新您的应用程序以注册Journey Optimizer标记扩展。
* 验证Assurance中的设置。
* 在Journey Optimizer中定义您自己的营销活动和应用程序内消息体验。
* 在应用程序中发送您自己的应用程序内消息。

## 设置

>[!TIP]
>
>如果您已将环境设置为 [Journey Optimizer推送消息](journey-optimizer-push.md) 课程，您可能已经执行了此设置部分中的某些步骤。


### 在数据收集中添加应用程序表面

1. 从 [数据收集界面](https://experience.adobe.com/data-collection/)，选择 **[!UICONTROL 应用程序表面]** 在左侧面板中。
1. 要创建配置，请选择 **[!UICONTROL 创建应用程序表面]**.
   ![应用程序表面主页](assets/push-app-surface.png)
1. 输入 **[!UICONTROL 名称]** 例如，对于配置 `Luma App Tutorial`  .
1. 从 **[!UICONTROL 移动应用程序配置]**，选择 **[!UICONTROL Apple iOS]**.
1. 在中输入移动应用程序捆绑包ID **[!UICONTROL 应用程序ID(iOS捆绑包ID)]** 字段。 例如：`com.adobe.luma.tutorial.swiftui`。
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![应用程序表面配置](assets/push-app-surface-config.png)

### 更新数据流配置

要确保将从您的移动应用程序发送到边缘网络的数据转发到Journey Optimizer，请更新您的Experience Edge配置。

1. 在数据收集UI中，选择 **[!UICONTROL 数据流]**，并选择您的数据流，例如 **[!DNL Luma Mobile App]**.
1. 选择 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) 对象 **[!UICONTROL Experience Platform]** 并选择 ![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 编辑]** 从上下文菜单中。
1. 在 **[!UICONTROL 数据流]** > ![文件夹](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** 屏幕，确保 **[!UICONTROL Adobe Journey Optimizer]** 已选中。 请参阅 [Adobe Experience Platform设置](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) 以了解更多信息。
1. 要保存数据流配置，请选择 **[!UICONTROL 保存]**.

   ![AEP数据流配置](assets/datastream-aep-configuration.png)


### 安装Journey Optimizer标记扩展

要使您的应用程序能够与Journey Optimizer配合使用，您需要更新标记属性。

1. 导航到 **[!UICONTROL 标记]** > **[!UICONTROL 扩展]** > **[!UICONTROL 目录]**.
1. 打开您的资产，例如 **[!DNL Luma Mobile App Tutorial]**.
1. 选择 **[!UICONTROL 目录]**.
1. 搜索 **[!UICONTROL Adobe Journey Optimizer]** 扩展。
1. 安装扩展。
1. 在 **[!UICONTROL 安装扩展]** 对话框
   1. 选择环境，例如 **[!UICONTROL 开发]**.
   1. 选择 **[!UICONTROL AJO推送跟踪体验事件数据集]** 来自的数据集 **[!UICONTROL 事件数据集]** 列表。
   1. 选择 **[!UICONTROL 保存到库并生成]**.
      ![AJO扩展设置](assets/push-tags-ajo.png)

>[!NOTE]
>
>如果您没有看到 `AJO Push Tracking Experience Event Dataset` 或者，请联系客户关怀团队。
>

### 在应用程序中实施Journey Optimizer

如前面的课程中所述，安装移动标记扩展仅提供配置。 接下来，您必须安装并注册消息传送SDK。 如果这些步骤不明确，请查阅 [安装SDK](install-sdks.md) 部分。

>[!NOTE]
>
>如果您已完成 [安装SDK](install-sdks.md) 部分，则该SDK已安装，您可以跳过此步骤。
>

1. 在Xcode中，确保 [AEP消息](https://github.com/adobe/aepsdk-messaging-ios.git) 会添加到包依赖关系中的包列表中。 请参阅 [Swift包管理器](install-sdks.md#swift-package-manager).
1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** 在Xcode项目导航器中。
1. 确保 `AEPMessaging` 是导入列表的一部分。

   `import AEPMessaging`

1. 确保 `Messaging.self` 是您注册的扩展数组的一部分。

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


## 使用Assurance验证设置

1. 查看 [设置说明](assurance.md) 部分。
1. 在物理设备或模拟器上安装应用程序。
1. 使用保障生成的URL启动应用程序。
1. 在Assurance UI中，选择 **[!UICONTROL 配置]**.
   ![配置点击](assets/push-validate-config.png)
1. 选择 ![加号](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 按钮旁边 **[!UICONTROL 应用程序内消息传送]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/assurance-in-app-config.png)
1. 选择 **[!UICONTROL 应用程序内消息传送]** 从左侧导航栏中。
1. 选择 **[!UICONTROL 验证]** 选项卡。 确认您没有收到任何错误。

   ![应用程序内验证](assets/assurance-in-app-validate.png)


## 创建您自己的应用程序内消息

要创建您自己的应用程序内消息，您必须在Journey Optimizer中定义一个促销活动，以根据发生的事件触发应用程序内消息。 这些事件可以是：

* 数据发送到Adobe Experience Platform，
* 通过Mobile Core通用API的核心跟踪事件（如操作）或PII数据的状态或集合，
* 应用程序生命周期事件，例如启动、安装、升级、关闭或崩溃，
* 地理位置事件，例如进入或退出目标点。

在本教程中，您将使用移动核心通用和独立于扩展的API(请参阅 [Mobile Core通用API](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis))以方便对用户屏幕、操作和PII数据进行事件跟踪。 这些API生成的事件将发布到SDK事件中心，可供扩展使用。 SDK事件中心提供了与所有AEP Mobile SDK扩展绑定的核心数据结构，其中维护着已注册的扩展和内部模块的列表、已注册的事件侦听器的列表以及共享状态数据库。
SDK事件中心发布并接收来自已注册的扩展的事件数据，以简化与Adobe和第三方解决方案的集成。 例如，在安装优化扩展时，事件中心将处理所有请求以及与Journey Optimizer — 决策管理选件引擎的交互。

1. 在Journey Optimizer UI中，选择 **[!UICONTROL 营销活动]** 从左边栏开始。
1. 选择 **[!UICONTROL 创建营销活动]**.
1. 在 **[!UICONTROL 创建营销活动]** 屏幕：
   1. 选择 **[!UICONTROL 应用程序内消息]** 并从中选择一个应用程序表面 **[!UICONTROL 应用程序表面]** 列表，例如 **[!DNL Luma Mobile App]**.
   1. 选择 **[!UICONTROL 创建]**
      ![营销活动属性](assets/ajo-campaign-properties.png)
1. 在Campaign定义屏幕中，位于 **[!UICONTROL 属性]**，输入 **[!UICONTROL 名称]** 例如，促销活动 `Luma - In-App Messaging Campaign`，和 **[!UICONTROL 描述]**&#x200B;例如 `In-app messaging campaign for Luma app`.
   ![营销活动名称](assets/ajo-campaign-properties-name.png)
1. 向下滚动到 **[!UICONTROL 操作]**，并选择 **[!UICONTROL 编辑内容]**.
1. 在 **[!UICONTROL 应用程序内消息]** 屏幕：
   1. 选择 **[!UICONTROL 模态]** 作为 **[!UICONTROL 消息布局]**.
   2. 输入 `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` 对于 **[!UICONTROL 媒体URL]**.
   3. 输入 **[!UICONTROL 页眉]**&#x200B;例如 `Welcome to this Luma In-App Message` 并输入 **[!UICONTROL 正文]**&#x200B;例如 `Triggered by pushing that button in the app...`.
   4. 输入 **[!UICONTROL 取消]** 作为 **[!UICONTROL 按钮#1文本（主要）]**.
   5. 请注意预览的更新方式。
   6. 选择 **[!UICONTROL 审查以激活]**.
      ![应用程序内编辑器](assets/ajo-in-app-editor.png)
1. 在 **[!UICONTROL 审查以激活（Luma — 应用程序内消息传送促销活动）]** 屏幕，选择 ![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) 在 **[!UICONTROL 计划]** 磁贴。
   ![复查计划选择计划](assets/ajo-review-select-schedule.png)
1. 返回 **[!DNL Luma - In-App Messaging Campaign]** 屏幕，选择 ![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 编辑触发器]**.
1. 在 **[!UICONTROL 应用程序内消息触发器]** 对话框，您可以配置触发应用程序内消息的跟踪操作的详细信息：
   1. 要删除 **[!UICONTROL 应用程序启动事件]**，选择 ![关闭](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. 使用 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加条件]** 反复构建以下逻辑 **[!UICONTROL 显示消息条件]**.
   1. 单击&#x200B;**[!UICONTROL 完成]**。
      ![触发器逻辑](assets/ajo-trigger-logic.png)

   您已定义一个跟踪操作，其中 **[!UICONTROL 操作]** 等于 `in-app` 和 **[!UICONTROL 上下文数据]** （操作是键值对） `"showMessage" : "true"`.

1. 返回 **[!DNL Luma - In-App Messaging Campaign]** 屏幕，选择 **[!UICONTROL 审查以激活]**.
1. 在 **[!UICONTROL 审查以激活（Luma — 应用程序内消息传送促销活动）]** 屏幕，选择 **[!UICONTROL 激活]**.
1. 您看到您的 **[!DNL Luma - In-App Messaging Campaign]** 状态 **[!UICONTROL 实时]** 在 **[!UICONTROL 营销活动]** 列表。
   ![营销活动列表](assets/ajo-campaign-list.png)


## 触发应用程序内消息

您已具备发送应用程序内消息的所有条件。 剩下的是如何在应用程序中触发此应用程序内消息的。

1. 转到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode项目导航器中。 查找 `func sendTrackAction(action: String, data: [String: Any]?)` 函数，并添加以下代码，以调用 [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) 函数，基于参数 `action` 和 `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. 转到 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 配置视图]** 在Xcode项目导航器中。 查找应用程序内消息按钮的代码并添加以下代码：

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## 使用应用程序进行验证

1. 在设备或模拟器中打开您的应用程序。

1. 转到 **[!UICONTROL 设置]** 选项卡。

1. 点按 **[!UICONTROL 应用程序内消息]**. 您会在应用程序中看到应用程序内消息。

   <img src="assets/ajo-in-app-message.png" width="300" />


## 在Assurance中验证实施

您可以在Assurance UI中验证应用程序内消息。

1. 选择 **[!UICONTROL 应用程序内消息传送]**.
1. 选择 **[!UICONTROL 事件列表]**.
1. 选择 **[!UICONTROL 显示消息]** 进入。
1. Inspect原始事件，特别是 `html`，其中包含应用程序内消息的完整布局和内容。
   ![保证应用程序内消息](assets/assurance-in-app-display-message.png)


## 后续步骤

现在，您应该拥有所有相关和适用的所有工具，以便开始添加应用程序内消息。  例如，根据您在应用程序中跟踪的特定交互来促销产品。

>[!SUCCESS]
>
>您已为应用程序内消息传送启用应用程序，并为Experience PlatformMobile SDK使用Journey Optimizer和Journey Optimizer扩展添加了应用程序内消息传送促销活动。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[通过Journey Optimizer显示优惠](journey-optimizer-offers.md)**
