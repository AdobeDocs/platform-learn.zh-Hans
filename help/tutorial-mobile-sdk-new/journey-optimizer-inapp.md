---
title: Adobe Journey Optimizer应用程序内消息传送
description: 了解如何使用Platform Mobile SDK和Adobe Journey Optimizer在移动应用程序中创建应用程序内消息。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
hide: true
source-git-commit: c3c12d63762f439faa9c45d27e66468455774b43
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 2%

---

# Adobe Journey Optimizer应用程序内消息传送

了解如何使用Platform Mobile SDK和Adobe Journey Optimizer为移动应用程序创建应用程序内消息。

Journey Optimizer允许您创建历程，并向目标受众发送应用程序内消息。 在使用Journey Optimizer发送应用程序内消息之前，必须确保进行适当的配置和集成。 要了解Adobe Journey Optimizer中的应用程序内消息传送数据流，请参阅 [文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>本课程是可选的，仅适用于希望发送应用程序内消息的Adobe Journey Optimizer用户。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 对Adobe Journey Optimizer的访问权限和足够的权限，如所述 [此处](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 您还需要具有足够权限才能使用以下Adobe Journey Optimizer功能。
   * 创建营销活动.
* 具有创建证书、标识符和密钥的足够访问权限的付费Apple开发人员帐户。
* 用于测试的物理iOS设备或模拟器。
* [已注册应用程序的APN ID](journey-optimizer-push.md#register-app-id-with-apn)
* [已在数据收集中添加您的应用程序推送凭据](journey-optimizer-push.md#add-your-app-push-credentials-in-data-collection)
* [已安装Adobe Journey Optimizer标记扩展](journey-optimizer-push.md#install-adobe-journey-optimizer-tags-extension)
* [在应用程序中实施了Adobe Journey Optimizer](journey-optimizer-push.md#implement-adobe-journey-optimizer-in-the-app)


## 使用保障进行验证

1. 查看 [设置说明](assurance.md) 部分。
1. 在物理设备或模拟器上安装应用程序。
1. 使用保障生成的URL启动应用程序。
1. 在Assurance UI中，选择 **[!UICONTROL 配置]**.
   ![配置点击](assets/push-validate-config.png)
1. 选择 ![加号](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 按钮旁边 **[!UICONTROL 应用程序内消息传送]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/assurance-in-app-config.png)
1. 选择 **[!UICONTROL 应用程序内消息传送]** 从左侧导航栏中。
1. 选择 **[!UICONTROL 验证]** 选项卡。
1. 确认您没有收到任何错误。
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
   1. 选择 **[!UICONTROL 应用程序内消息]** 并选择 **[!UICONTROL Luma移动应用程序]** 从 **[!UICONTROL 应用程序表面]** 列表。
   1. 选择 **[!UICONTROL 创建]**
      ![营销活动属性](assets/ajo-campaign-properties.png)
1. 在Campaign定义屏幕中，位于 **[!UICONTROL 属性]**，输入 **[!UICONTROL 名称]** 例如，促销活动 `Luma - In-App Messaging Campaign`，和 **[!UICONTROL 描述]**&#x200B;例如 `In-app messaging campaign for Luma app`.
   ![营销活动名称](assets/ajo-campaign-properties-name.png)
1. 向下滚动到 **[!UICONTROL 操作]**，并选择 **[!UICONTROL 编辑内容]**.
1. 在 **[!UICONTROL 应用程序内消息]** 屏幕：
   1. 选择 **[!UICONTROL 模态]** 作为 **[!UICONTROL 消息布局]**.
   2. 输入 `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` 对象 **[!UICONTROL 媒体URL]**.
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

您已具备发送应用程序内消息的所有条件。 剩下的是如何在代码中触发此应用程序内消息的。

1. 在Xcode项目导航器中，转到Luma > Luma > Utils > MobileSDK，然后找到 `func sendTrackAction(action: String, data: [String: Any]?)` 函数，并添加以下代码，以调用 `MobileCore.track` 函数，基于参数 `action` 和 `data`.


   ```swift
   // send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. 转到 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 视图]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置视图]** 在Xcode项目导航器中。 查找应用程序内消息按钮的代码并添加以下代码：

   ```swift
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## 使用应用程序进行验证

1. 在设备或模拟器中打开您的应用程序。

1. 转到 **[!UICONTROL 设置]** 选项卡。

1. 点按 **[!UICONTROL 应用程序内消息]**. 您会在应用程序中看到应用程序内消息。
   <img src="assets/ajo-in-app-message.png" width="300" />


## 在Assurance中验证

您可以在Assurance UI中验证应用程序内消息。

1. 选择 **[!UICONTROL 应用程序内消息传送]**.
1. 选择 **[!UICONTROL 事件列表]**.
1. 选择 **[!UICONTROL 显示消息]** 进入。
1. Inspect原始事件，特别是 `html`，其中包含应用程序内消息的完整布局和内容。
   ![保证应用程序内消息](assets/assurance-in-app-display-message.png)


## 在应用程序中实施

您现在应该拥有所有工具，以便开始将推送通知添加到Luma应用程序（如果相关适用）。 例如，在登录应用程序或访问特定地理位置时欢迎用户。

>[!SUCCESS]
>
>现在，您已为应用程序内消息传送启用应用程序，并为Adobe Experience Platform Mobile SDK使用Adobe Journey Optimizer和Adobe Journey Optimizer扩展添加了应用程序内消息传送促销活动。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[结论和后续步骤](conclusion.md)**
