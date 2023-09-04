---
title: Adobe Journey Optimizer应用程序内消息传送
description: 了解如何使用Platform Mobile SDK和Adobe Journey Optimizer在移动应用程序中创建应用程序内消息。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
hide: true
source-git-commit: 56323387deae4a977a6410f9b69db951be37059f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 2%

---

# Journey Optimizer应用程序内消息传送

了解如何使用Experience PlatformMobile SDK和Journey Optimizer为移动应用程序创建应用程序内消息。

Journey Optimizer允许您创建营销活动，以将应用程序内消息发送给目标受众。 在使用Journey Optimizer发送应用程序内消息之前，必须确保进行适当的配置和集成。 要了解Journey Optimizer中的应用程序内消息传送数据流，请参阅 [文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>本课程是可选的，仅适用于希望发送应用程序内消息的Journey Optimizer用户。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 对Journey Optimizer的访问权限和足够的权限，如所述 [此处](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 此外，您需要具有足够的权限才能使用以下Journey Optimizer功能。
   * 管理营销活动。
* 具有创建证书、标识符和密钥的足够访问权限的付费Apple开发人员帐户。
* 用于测试的物理iOS设备或模拟器。
* 向Apple推送通知服务注册的应用程序ID
* 已在数据收集中添加您的应用程序推送凭据
* 已安装Journey Optimizer标记扩展
* 在应用程序中实施了Journey Optimizer


## 学习目标

在本课程中，您将执行以下操作

* 向Apple推送通知服务(APN)注册应用程序ID。
* 在AJO中创建应用程序表面。
* 安装和配置Journey Optimizer标记扩展。
* 更新您的应用程序以包含Journey Optimizer标记扩展。
* 验证Assurance中的设置。
* 在Journey Optimizer中定义您自己的营销活动和应用程序内消息体验。
* 在应用程序中发送您自己的应用程序内消息。

## 设置

>[!TIP]
>
>如果您已将环境设置为 [Journey Optimizer推送消息](journey-optimizer-push.md) 教程中，您可以跳过此部分。

### 向APNS注册应用程序ID

以下步骤并非特定于Adobe Experience Cloud，而是旨在引导您完成APNS配置。

### 创建私钥

1. 在Apple开发人员门户中，导航到 **[!UICONTROL 键]**.
1. 要创建键，请选择 **[!UICONTROL +]**.
   ![创建新键](assets/mobile-push-apple-dev-new-key.png)

1. 提供 **[!UICONTROL 密钥名称]**.
1. 选择 **[!UICONTROL Apple推送通知服务] (APNs)** 复选框。
1. 选择 **[!UICONTROL 继续]**.
   ![配置新密钥](assets/mobile-push-apple-dev-config-key.png)
1. 查看配置并选择 **[!UICONTROL 注册]**.
1. 下载 `.p8` 私钥。 它用在应用程序表面配置中。
1. 记下 **[!UICONTROL 密钥ID]**. 它用在应用程序表面配置中。
1. 记下 **[!UICONTROL 团队编号]**. 它用在应用程序表面配置中。
   ![关键详细信息](assets/push-apple-dev-key-details.png)

其他文档可以是 [在此处找到](https://help.apple.com/developer-account/#/devcdfbb56a3).

### 在数据收集中添加您的应用程序推送凭据

1. 从 [数据收集界面](https://experience.adobe.com/data-collection/)，选择 **[!UICONTROL 应用程序表面]** 在左侧面板中。
1. 要创建配置，请选择 **[!UICONTROL 创建应用程序表面]**.
   ![应用程序表面主页](assets/push-app-surface.png)
1. 输入 **[!UICONTROL 名称]** 例如，对于配置 `Luma App Tutorial`  .
1. 从 **[!UICONTROL 移动应用程序配置]**，选择 **[!UICONTROL Apple iOS]**.
1. 在中输入移动应用程序捆绑包ID **[!UICONTROL 应用程序ID(iOS捆绑包ID)]** 字段。 例如：`com.adobe.luma.tutorial.swiftui`。
1. 打开 **[!UICONTROL 推送凭据]** 切换以添加您的凭据。
1. 拖放 `.p8` **Apple推送通知身份验证密钥** 文件。
1. 提供 **[!UICONTROL 密钥ID]**，在创建期间分配的10个字符的字符串 `p8` 身份验证密钥。 它可以在以下位置找到 **[!UICONTROL 键]** 选项卡 **证书、标识符和配置文件** Apple开发人员门户页面的页面。 另请参阅 [创建私钥](#create-a-private-key).
1. 提供 **[!UICONTROL 团队编号]**. “团队ID”是一个值，该值可在下找到 **会员资格** 选项卡或Apple开发人员门户页面顶部的。 另请参阅 [创建私钥](#create-a-private-key).
1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![应用程序表面配置](assets/push-app-surface-config.png)

### 安装Journey Optimizer标记扩展

要使您的应用程序能够与Journey Optimizer配合使用，您需要更新标记属性。

1. 导航到 **[!UICONTROL 标记]** > **[!UICONTROL 扩展]** > **[!UICONTROL 目录]**，
1. 打开您的资产，例如 **[!UICONTROL Luma移动应用程序教程]**.
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
1. 导航到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** 在Xcode项目导航器中。
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

在本教程中，您将使用Mobile Core通用和独立于扩展的API来促进对用户屏幕、操作和PII数据的事件跟踪。 这些API生成的事件将发布到SDK事件中心，可供扩展使用。 例如，安装Analytics扩展后，所有用户操作和应用程序屏幕事件数据都会发送到相应的Analytics报表端点。

1. 在Journey Optimizer UI中，选择 **[!UICONTROL 营销活动]** 从左边栏开始。
1. 选择 **[!UICONTROL 创建营销活动]**.
1. 在 **[!UICONTROL 创建营销活动]** 屏幕：
   1. 选择 **[!UICONTROL 应用程序内消息]** 并从中选择一个应用程序表面 **[!UICONTROL 应用程序表面]** 列表，例如 **[!UICONTROL Luma移动应用程序]**.
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
1. 返回 **[!UICONTROL Luma — 应用程序内消息传送促销活动]** 屏幕，选择 ![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 编辑触发器]**.
1. 在 **[!UICONTROL 应用程序内消息触发器]** 对话框，您可以配置触发应用程序内消息的跟踪操作的详细信息：
   1. 要删除 **[!UICONTROL 应用程序启动事件]**，选择 ![关闭](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. 使用 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加条件]** 反复构建以下逻辑 **[!UICONTROL 显示消息条件]**.
   1. 单击&#x200B;**[!UICONTROL 完成]**。
      ![触发器逻辑](assets/ajo-trigger-logic.png)

   您已定义一个跟踪操作，其中 **[!UICONTROL 操作]** 等于 `in-app` 和 **[!UICONTROL 上下文数据]** （操作是键值对） `"showMessage" : "true"`.

1. 返回 **[!UICONTROL Luma — 应用程序内消息传送促销活动]** 屏幕，选择 **[!UICONTROL 审查以激活]**.
1. 在 **[!UICONTROL 审查以激活（Luma — 应用程序内消息传送促销活动）]** 屏幕，选择 **[!UICONTROL 激活]**.
1. 您看到您的 **[!UICONTROL Luma — 应用程序内消息传送促销活动]** 状态 **[!UICONTROL 实时]** 在 **[!UICONTROL 营销活动]** 列表。
   ![营销活动列表](assets/ajo-campaign-list.png)


## 触发应用程序内消息

您已具备发送应用程序内消息的所有条件。 剩下的是如何在应用程序中触发此应用程序内消息的。

1. 转到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 实用工具]** > **[!UICONTROL MobileSDK]** 在Xcode项目导航器中。 查找 `func sendTrackAction(action: String, data: [String: Any]?)` 函数，并添加以下代码，以调用 [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) 函数，基于参数 `action` 和 `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. 转到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 视图]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置视图]** 在Xcode项目导航器中。 查找应用程序内消息按钮的代码并添加以下代码：

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

您现在应该拥有所有工具，可以开始向Luma应用程序添加相关的适用应用程序内消息。 例如，根据您在应用程序中跟踪的特定交互来促销产品。

>[!SUCCESS]
>
>您已为应用程序内消息传送启用应用程序，并为Experience PlatformMobile SDK使用Journey Optimizer和Journey Optimizer扩展添加了应用程序内消息传送促销活动。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[通过Journey Optimizer显示优惠](journey-optimizer-offers.md)**
