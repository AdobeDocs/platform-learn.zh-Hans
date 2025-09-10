---
title: 使用Platform Mobile SDK创建和发送推送通知
description: 了解如何使用Platform Mobile SDK和Adobe Journey Optimizer创建指向移动应用程序的推送通知。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
jira: KT-14638
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---

# 创建和发送推送通知

了解如何使用Experience Platform Mobile SDK和Journey Optimizer为移动应用程序创建推送通知。

Journey Optimizer允许您创建历程并向目标受众发送消息。 在使用Journey Optimizer发送推送通知之前，您必须确保已进行适当的配置和集成。 要了解Journey Optimizer中的推送通知数据流，请参阅[文档](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/channels/push/push-config/push-gs)。

![架构](assets/architecture-ajo.png){zoomable="yes"}

>[!NOTE]
>
>本课程是可选的，仅适用于希望发送推送通知的Journey Optimizer用户。


## 先决条件

* 在安装和配置SDK的情况下成功构建并运行应用程序。
* 为Adobe Experience Platform设置应用程序。
* 访问Journey Optimizer和[足够的权限](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/channels/push/push-config/push-configuration)。 此外，您需要具有足够的权限才能使用以下Journey Optimizer功能。
   * 创建推送凭据。
   * 创建推送渠道配置。
   * 创建旅程。
   * 创建消息。
   * 创建消息预设。
* 对于iOS，为&#x200B;**付费Apple开发人员帐户**，该帐户具有创建证书、标识符和密钥的足够访问权限。
* 对于Android，这是Google开发人员帐户，具有创建证书和密钥的足够访问权限。
* 用于测试的物理iOS或Android设备或模拟器。

## 学习目标

在本课程中，您将执行以下操作

* 向Apple推送通知服务(APN)注册应用程序ID。
* 在Journey Optimizer中创建渠道配置。
* 更新您的架构以包含推送消息字段。
* 安装和配置Journey Optimizer标记扩展。
* 更新您的应用程序以注册Journey Optimizer标记扩展。
* 验证Assurance中的设置。
* 从Assurance发送测试消息
* 在Journey Optimizer中定义您自己的推送通知事件、历程和体验。
* 从应用程序内发送您自己的推送通知。


## 设置

>[!TIP]
>
>如果您已将环境设置为[Journey Optimizer应用程序内消息传送](journey-optimizer-inapp.md)课程的一部分，则您可能已执行了此设置部分中的某些步骤。

### 创建推送凭据

对于推送通知，您必须首先为推送通知注册应用程序。

>[!BEGINTABS]

>[!TAB iOS]

以下步骤并非特定于Adobe Experience Cloud，而是旨在引导您完成APN配置。

1. 在Apple开发人员门户中，导航到&#x200B;**[!UICONTROL 密钥]**。
1. 要创建密钥，请选择&#x200B;**[!UICONTROL +]**。

   ![创建新键](assets/mobile-push-apple-dev-new-key.png){zoomable="yes"}

1. 提供&#x200B;**[!UICONTROL 密钥名称]**。
1. 选择&#x200B;**[!UICONTROL Apple推送通知服务] (APN)**，然后选择&#x200B;**[!UICONTROL 配置]**。
   1. 在&#x200B;**[!UICONTROL 配置键]**&#x200B;屏幕中，从&#x200B;**[!UICONTROL 环境]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 沙盒和生产]**。
   1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 选择&#x200B;**[!UICONTROL 继续]**。

   ![配置新密钥](assets/mobile-push-apple-dev-config-key.png){zoomable="yes"}

1. 查看配置并选择&#x200B;**[!UICONTROL 注册]**。
1. 下载`.p8`私钥。 当您配置Journey Optimizer推送凭据时，将在下一个练习中使用它。
1. 记下&#x200B;**[!UICONTROL 密钥ID]**。 当您配置Journey Optimizer推送凭据时，将在下一个练习中使用它。
1. 记下&#x200B;**[!UICONTROL 团队ID]**。 当您配置Journey Optimizer推送凭据时，将在下一个练习中使用它。 团队ID可在屏幕右上角登录名旁边找到。
   ![键详细信息](assets/push-apple-dev-key-details.png){zoomable="yes"}

其他文档可在[此处](https://help.apple.com/developer-account/#/devcdfbb56a3)找到。

>[!TAB Android]

以下步骤并非特定于Adobe Experience Cloud，而是旨在引导您完成Firebase配置。

1. 访问Firebase控制台。
1. 选择&#x200B;**[!UICONTROL 创建Firebase项目]**。
   1. 输入&#x200B;**[!UICONTROL 项目名称]**。
   1. 在&#x200B;**[!UICONTROL 创建项目]**&#x200B;中选择&#x200B;**[!UICONTROL 继续]** - **[!UICONTROL 让我们为您的项目起一个名称]**。 例如：`Luma Android App.`
   1. 在Firebase中禁用&#x200B;**[!UICONTROL Gemini]**，并在&#x200B;**[!UICONTROL 创建项目]**&#x200B;中选择&#x200B;**[!UICONTROL 继续]** - **[!UICONTROL Firebase项目的AI帮助]**。
   1. 为此项目&#x200B;**[!UICONTROL 禁用]** Google Analytics，并在&#x200B;**[!UICONTROL 为您的Firebase项目创建项目]** - **[!UICONTROL Google Analytics]**&#x200B;中选择&#x200B;**[!UICONTROL 继续]**。
   1. 选择&#x200B;**[!UICONTROL 创建项目]**。
   1. 项目就绪后，选择&#x200B;**[!UICONTROL 继续]**。

1. 返回到Firebase控制台，确保在顶部选择您的项目。 例如，**[!UICONTROL Luma Android应用程序]**。

   ![Firebase控制台](assets/fcm-1.png){zoomable="yes"}

1. 选择![设置](/help/assets/icons/Setting.svg) > **[!UICONTROL 项目设置]**。

1. 在&#x200B;**[!UICONTROL 项目设置]**&#x200B;中，选择&#x200B;**[!UICONTROL 添加应用程序]**。
   1. 在&#x200B;**[!UICONTROL 将Firebase添加到应用程序]**&#x200B;中，选择&#x200B;**[!UICONTROL Android]**&#x200B;作为平台。
   1. 在&#x200B;**[!UICONTROL 将Firebase添加到您的Android应用程序中：]**
      1. 在步骤1，**[!UICONTROL 注册应用程序]**：
         1. 输入Android包名称，该名称与您的应用程序标识符类似。 例如：`com.adobe.luma.tutorial.android`。
         1. 输入可选的&#x200B;**[!UICONTROL 应用程序昵称]**。
         1. 选择&#x200B;**[!UICONTROL 注册应用程序]**。
      1. 在步骤2中，**[!UICONTROL 下载配置文件]**，然后添加该文件。
         1. 选择![下载](/help/assets/icons/Download.svg)**[!UICONTROL 下载google-services.json]**。 当您构建自己的Android应用程序版本时，您应该将示例Android Studio项目中的当前`google-services.json`文件替换为由此新应用程序配置生成的文件版本。
其他步骤已在示例应用程序中完成。

   您的屏幕应如下所示：

   ![Firebase控制台](assets/fcm-2.png){zoomable="yes"}

1. 在&#x200B;**[!UICONTROL 项目设置]**&#x200B;中，选择&#x200B;**[!UICONTROL 服务帐户]**。
1. 选择&#x200B;**[!UICONTROL 生成新的私钥]**。 已生成`luma-android-app-firebase-adminsdk-xxxx-xxxxxxxx.json`文件。 将此文件存储在安全位置，因为您以后需要此文件。

有关详细信息，请参阅[Firebase开发人员文档](https://firebase.google.com/docs)。

>[!ENDTABS]

### 在数据收集中添加您的应用程序推送凭据

接下来，您需要添加移动应用程序推送凭据，以授权Adobe代表您发送推送通知。 您可以在数据收集或Journey Optimizer中添加推送凭据。 在本教程中，将使用数据收集界面。 然后，推送凭据将链接到Journey Optimizer中的渠道配置。

1. 在数据收集中，选择&#x200B;**[!UICONTROL 应用程序表面]**。
1. 选择&#x200B;**[!UICONTROL 创建应用程序表面]**。
1. 在&#x200B;**[!UICONTROL 创建应用程序表面]**&#x200B;界面中：
   1. 输入&#x200B;**[!UICONTROL 名称]**。
   1. 如果要发送Apple iOS的推送通知，请选择&#x200B;**[!UICONTROL iOS]**。
      1. 输入您的&#x200B;**[!UICONTROL 应用程序ID]**，例如`com.adobe.luma.tutorial.swiftui`。
      1. 选择沙盒（可选）。
      1. 启用&#x200B;**[!UICONTROL 推送凭据]**。
      1. 将保存的`.p8`私钥文件拖放到&#x200B;**[!UICONTROL 上拖放您的文件]**。
      1. 输入&#x200B;**[!UICONTROL 密钥ID]**。
      1. 输入&#x200B;**[!UICONTROL 团队ID]**。
   1. 如果要发送Android的推送通知，请选择&#x200B;**[!UICONTROL Android]**。
      1. 输入您的&#x200B;**[!UICONTROL 应用程序ID]**，例如`com.adobe.luma.tutorial.android`。
      1. 选择沙盒（可选）。
      1. 启用&#x200B;**[!UICONTROL 推送凭据]**。
      1. 将保存的`luma-android-app-firebase-adminsdk-xxxx-xxxxxxxx.json`文件拖放到&#x200B;**[!UICONTROL 上拖放您的文件]**。

   ![在Journey Optimizer中新建推送凭据配置](assets/add-push-credentials.png){zoomable="yes"}

1. 选择 **[!UICONTROL Save]**。如果所有信息都正确，则表示您已经创建了推送凭据来与渠道配置关联。


### 在Journey Optimizer中创建推送的渠道配置

创建推送凭据配置后，必须创建配置才能从Journey Optimizer发送推送通知。

1. 在Journey Optimizer界面中，打开&#x200B;**[!UICONTROL 渠道]** > **[!UICONTROL 常规设置]** > **[!UICONTROL 渠道配置]**&#x200B;菜单，然后选择&#x200B;**[!UICONTROL 创建渠道配置]**。

   ![创建新的渠道配置](assets/push-config-9.png){zoomable="yes"}

1. 输入配置的名称和说明（可选）。

   >[!NOTE]
   >
   > 名称必须以字母(A-Z)开头。 它只能包含字母数字字符。 您还可以使用下划线 `_`、点 `.` 和连字符 `-` 符号。


1. 要为配置分配自定义或核心数据使用标签，您可以选择&#x200B;**[!UICONTROL 管理访问权限]**。 [了解有关对象级访问控制(OLAC)的更多信息](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/access-control/object-based-access)。

1. 选择&#x200B;**推送**&#x200B;渠道。


1. 选择&#x200B;**[!UICONTROL 营销操作]**&#x200B;以使用此配置将同意策略与消息关联。 所有与营销活动相关的同意政策都可以用来尊重客户的偏好。 [了解有关营销操作的更多信息](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions)。

1. 选择您的&#x200B;**[!UICONTROL 平台]**。 您可以为渠道配置同时配置&#x200B;**[!UICONTROL iOS]**&#x200B;和&#x200B;**[!UICONTROL Android]**。

1. 选择您之前用于定义推送凭据的相应&#x200B;**[!UICONTROL 应用程序ID]**。 例如，iOS的&#x200B;**[!UICONTROL com.adobe.luma.tutorial.swiftui]**&#x200B;和Android的&#x200B;**[!UICONTROL com.adobe.luma.tutorial.android]**。 绿色![CheckmarkCircle](/help/assets/icons/CheckmarkCircle.svg)表示有效的推送凭据与通道配置相关联。


   ![推送渠道配置](assets/push-config-10.png){zoomable="yes"}

1. 选择&#x200B;**[!UICONTROL 提交]**&#x200B;以保存更改。




### 更新数据流配置

要确保将从您的移动应用程序发送到Edge Network的数据转发到Journey Optimizer，请更新您的Experience Edge配置。

1. 在数据收集UI中，选择&#x200B;**[!UICONTROL 数据流]**，然后选择您的数据流，例如&#x200B;**[!DNL Luma Mobile App]**。
1. 为![Experience Platform](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)选择&#x200B;**[!UICONTROL 更多]**，然后从上下文菜单中选择![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 编辑]**。
1. 在&#x200B;**[!UICONTROL 数据流]** > ![文件夹](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**&#x200B;屏幕中：

   1. 如果尚未选择，请从&#x200B;**[!UICONTROL 配置文件数据集]**&#x200B;中选择&#x200B;**[!UICONTROL AJO推送配置文件数据集]**。 使用`MobileCore.setPushIdentifier` API调用时需要此配置文件数据集（请参阅[注册推送通知的设备令牌](#register-device-token-for-push-notifications)）。 此选择还可确保将推送通知的唯一标识符（即推送标识符）存储为用户配置文件的一部分。

   1. 已选择&#x200B;**[!UICONTROL Adobe Journey Optimizer]**。 有关详细信息，请参阅[Adobe Experience Platform设置](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/datastreams/configure)。

   1. 要保存数据流配置，请选择&#x200B;**[!UICONTROL 保存]**。

   ![AEP数据流配置](assets/datastream-aep-configuration.png){zoomable="yes"}



### 安装Journey Optimizer标记扩展

要使您的应用程序能够与Journey Optimizer配合使用，必须更新标记属性。

1. 导航到&#x200B;**[!UICONTROL 标记]** > **[!UICONTROL 扩展]** > **[!UICONTROL 目录]**，
1. 打开您的属性，例如&#x200B;**[!DNL Luma Mobile App Tutorial]**。
1. 选择&#x200B;**[!UICONTROL 目录]**。
1. 搜索&#x200B;**[!UICONTROL Adobe Journey Optimizer]**&#x200B;扩展。
1. 安装扩展。
1. 在&#x200B;**[!UICONTROL 安装扩展]**&#x200B;对话框中
   1. 选择一个环境，例如&#x200B;**[!UICONTROL 开发]**。
   1. 从&#x200B;**[!UICONTROL 事件数据集]**&#x200B;列表中选择&#x200B;**[!UICONTROL AJO推送跟踪体验事件数据集]**&#x200B;数据集。
   1. 选择&#x200B;**[!UICONTROL 保存到库并生成]**。
      ![AJO扩展设置](assets/push-tags-ajo.png){zoomable="yes"}

>[!NOTE]
>
>如果您未看到&#x200B;**[!UICONTROL AJO推送跟踪体验事件数据集]**&#x200B;作为一个选项，请联系客户关怀团队。
>

## 使用Assurance验证设置

1. 查看[设置说明](assurance.md#connecting-to-a-session)部分以将模拟器或设备连接到Assurance。
1. 在Assurance用户界面中，选择&#x200B;**[!UICONTROL 配置]**。
   ![配置click](assets/push-validate-config.png){zoomable="yes"}
1. 选择![推送调试](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)旁边的&#x200B;**[!UICONTROL 加号]**。
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/push-validate-save.png){zoomable="yes"}
1. 从左侧导航中选择&#x200B;**[!UICONTROL 推送调试]**。
1. 选择&#x200B;**[!UICONTROL 验证设置]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 客户端]**&#x200B;列表中选择您的设备。
1. 确认您没有收到任何错误。
   ![验证](assets/push-validate-confirm.png){zoomable="yes"}
1. 选择&#x200B;**[!UICONTROL 发送测试推送]**&#x200B;选项卡。
1. （可选）更改&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Body]**&#x200B;的默认详细信息，并确保提供应用程序需要的所有参数，如&#x200B;**[!UICONTROL Advanced]** > **[!UICONTROL Notification Channel]**(Android的必需参数，例如`LUMA_CHANNEL_ID`)。
1. 选择![错误](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL 发送测试推送通知]**。
1. 检查&#x200B;**[!UICONTROL 测试结果]**。

   ![从Assurance测试推送通知](assets/test-push.png){zoomable="yes"}
1. 您应会看到测试推送通知显示在应用程序中。

>[!BEGINTABS]

>[!TAB iOS]

<img src="assets/luma-app-push.png" width="300" />

>[!TAB Android]

<img src="assets/luma-app-push-android.png" width="300" />

>[!ENDTABS]

## 签名

>[!IMPORTANT]
>
>需要签署iOS应用才能在iOS上发送推送通知，并且&#x200B;**需要付费Apple开发人员帐户**。 您无需签署Android应用程序即可发送推送通知。


要更新应用程序的签名，请执行以下操作：

1. 在Xcode中转到您的应用程序。
1. 在项目导航器中选择&#x200B;**[!DNL Luma]**。
1. 选择&#x200B;**[!DNL Luma]**&#x200B;目标。
1. 选择&#x200B;**签名和功能**&#x200B;选项卡。
1. 配置&#x200B;**[!UICONTROL 自动管理签名]**、**[!UICONTROL 团队]**&#x200B;和&#x200B;**[!UICONTROL 捆绑包标识符]**，或者使用您的特定Apple开发配置详细信息。

   >[!IMPORTANT]
   >
   >请确保使用&#x200B;_唯一_&#x200B;捆绑标识符并替换`com.adobe.luma.tutorial.swiftui`捆绑标识符，因为每个捆绑标识符必须是唯一的。 通常，您使用反向DNS格式来打包的ID字符串，如`com.organization.brand.uniqueidentifier`。 例如，本教程的完成版本使用`com.adobe.luma.tutorial.swiftui`。


   ![Xcode签名功能](assets/xcode-signing-capabilities.png){zoomable="yes"}


## 向应用程序添加推送通知功能

>[!IMPORTANT]
>
>要在iOS应用程序中实施和测试推送通知，您必须拥有&#x200B;**付费** Apple开发人员帐户。

>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode中，从&#x200B;**[!DNL Luma]** TARGETS **[!UICONTROL 列表中选择]**，选择&#x200B;**[!UICONTROL 签名和功能]**&#x200B;选项卡，选择&#x200B;**[!UICONTROL +功能]**&#x200B;按钮，然后选择&#x200B;**[!UICONTROL 推送通知]**。 此选项使您的应用程序能够接收推送通知。

1. 接下来，您必须向应用程序添加通知扩展。 返回&#x200B;**[!DNL General]**&#x200B;选项卡并选择&#x200B;**[!UICONTROL 目标]**&#x200B;部分底部的&#x200B;**[!UICONTROL +]**&#x200B;图标。

1. 系统将提示您为新目标选择模板。 选择&#x200B;**[!UICONTROL 通知服务扩展]**，然后选择&#x200B;**[!UICONTROL 下一步]**。

1. 在下一个窗口中，使用`NotificationExtension`作为扩展的名称，然后单击&#x200B;**[!UICONTROL 完成]**&#x200B;按钮。

现在，您应该将推送通知扩展添加到应用程序中，类似于以下屏幕。

![Pusn通知扩展](assets/xcode-signing-capabilities-pushnotifications.png){zoomable="yes"}

>[!TAB Android]

已为推送通知设置了Android Studio项目。 您无需执行其他步骤即可为推送通知启用Android版本的Luma应用程序。 有关详细信息，请参阅[关于通知](https://developer.android.com/develop/ui/views/notifications)。

Android推送通知要求您在应用程序中和在发送推送通知时定义通知渠道id。 Android Luma应用中使用的渠道通知ID为`LUMA_CHANNEL ID`。

>[!ENDTABS]


## 在应用程序中实施Journey Optimizer

如前面的课程中所述，安装移动标记扩展仅提供配置。 接下来，您必须安装并注册消息传送SDK。 如果未清除这些步骤，请查看[安装SDK](install-sdks.md)部分。

>[!NOTE]
>
>如果您已完成[安装SDK](install-sdks.md)部分，则表明已安装SDK，您可以跳过此步骤。
>

>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode中，确保将[AEP消息](https://github.com/adobe/aepsdk-messaging-ios)添加到包依赖关系中的包列表中。 请参阅[Swift包管理器](install-sdks.md#swift-package-manager)。
1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]**。
1. 确保`AEPMessaging`是导入列表的一部分。

   `import AEPMessaging`

1. 请确保`Messaging.self`是正在注册的扩展数组的一部分。

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

>[!TAB Android]

1. 在Android Studio中，确保[aepsdk-messing-android](https://github.com/adobe/aepsdk-messaging-android)是&#x200B;**[!UICONTROL Android:app]** ChevronDown **&#x200B;**&#x200B;Gradle脚本![中](/help/assets/icons/ChevronDown.svg)build.gradle.kts （模块&#x200B;**[!UICONTROL ）]**&#x200B;的依赖项的一部分。 查看[Gradle](install-sdks.md#gradle)。
1. 在Android Studio项目导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]**。
1. 确保`com.adobe.marketing.mobile.Messaging`是导入列表的一部分。

   `import import com.adobe.marketing.mobile.Messaging`

1. 请确保`Messaging.EXTENSION`是正在注册的扩展数组的一部分。

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

>[!ENDTABS]



## 注册推送通知的设备令牌

您需要注册推送通知的设备令牌。

>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]**。
1. 将[`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) API添加到`func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)`函数。

   ```swift
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(deviceToken)
   ```

   此函数检索与安装应用程序的设备特有的设备令牌。 然后，使用您设置的依赖于Apple推送通知服务(APN)的配置来设置推送通知投放令牌。

>[!TAB Android]

1. 在Android Studio项目导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]**。
1. 在[`MobileCore.setPushIdentifier`中将](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier)`override fun onCreate()` API添加到`class LumaAplication : Application`中的`FirebaseMessaging.getInstance().token.addOnCompleteListener`函数。

   ```kotlin
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(token)
   ```

   此函数检索与安装应用程序的设备特有的设备令牌。 然后，使用您设置的依赖于Firebase Cloud Messaging (FCM)的配置来设置推送通知投放令牌。

>[!ENDTABS]

>[!IMPORTANT]
>
>**仅适用于iOS**： `MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])`确定推送通知是使用APNs沙盒还是生产服务器来发送推送通知。 在模拟器中或在设备上测试您的应用程序时，请确保`messaging.useSandbox`设置为`true`，以便您接收推送通知。 在使用Apple的Testflight部署应用程序以进行生产测试时，请确保将`messaging.useSandbox`设置为`false`，否则生产应用程序将无法接收推送通知。<br/><br/>
>&#x200B;>Firebase Cloud Messaging (FCM) **不**&#x200B;支持推送通知沙盒的概念。


## 创建自己的推送通知

要创建自己的推送通知，您必须在Journey Optimizer中定义一个事件，以触发负责发送推送通知的历程。

### 更新您的架构

您即将定义一个新的事件类型，该类型还不能作为您在架构中定义的事件列表的一部分使用。 您稍后在触发推送通知时使用此事件类型。

1. 在Journey Optimizer UI中，从左边栏中选择&#x200B;**[!UICONTROL 架构]**。
1. 在选项卡栏中选择&#x200B;**[!UICONTROL 浏览]**。
1. 选择您的架构，例如&#x200B;**[!DNL Luma Mobile App Event Schema]**&#x200B;以将其打开。
1. 在架构编辑器中：
   1. 选择&#x200B;**[!UICONTROL eventType]**&#x200B;字段。
   1. 在&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗格中，向下滚动以查看事件类型可能值的列表。 选择&#x200B;**[!UICONTROL 添加行]**，并将`application.test`添加为&#x200B;**[!UICONTROL VALUE]**，将`[!UICONTROL Test event for push notification]`添加为`DISPLAY NAME`。
   1. 选择&#x200B;**[!UICONTROL 应用]**。
   1. 选择&#x200B;**[!UICONTROL 保存]**。

      ![向事件类型添加值](assets/ajo-update-schema-eventtype-enum.png){zoomable="yes"}

### 定义事件

Journey Optimizer中的事件允许您触发发送消息的历程，例如推送通知。 有关详细信息，请参阅[关于事件](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/configure-journeys/events-journeys/about-events)。

1. 在Journey Optimizer UI中，从左边栏中选择&#x200B;**[!UICONTROL 配置]**。

1. 在&#x200B;**[!UICONTROL 仪表板]**&#x200B;屏幕中，选择&#x200B;**[!UICONTROL 事件]**&#x200B;拼贴中的&#x200B;**[!UICONTROL 管理]**&#x200B;按钮。

1. 在&#x200B;**[!UICONTROL 事件]**&#x200B;屏幕中，选择&#x200B;**[!UICONTROL 创建事件]**。

1. 在&#x200B;**[!UICONTROL 编辑事件event1]**&#x200B;窗格中：

   1. 输入`LumaTestEvent`作为事件的&#x200B;**[!UICONTROL Name]**。
   1. 提供&#x200B;**[!UICONTROL 描述]**，例如`Test event to trigger push notifications in Luma app`。

   1. 选择您之前在[从](create-schema.md)架构&#x200B;**[!UICONTROL 列表创建XDM架构]**&#x200B;中创建的移动应用体验事件架构，例如&#x200B;**[!DNL Luma Mobile App Event Schema v.1]**。
   1. 选择![字段](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)列表旁边的&#x200B;**[!UICONTROL 编辑]**。

      ![编辑事件步骤1](assets/ajo-edit-event1.png){zoomable="yes"}

      在&#x200B;**[!UICONTROL 字段]**&#x200B;对话框中，确保选择以下字段(位于始终选择的默认字段之上（**[!UICONTROL _id]**、**[!UICONTROL id]**&#x200B;和&#x200B;**[!UICONTROL 时间戳]**）。 您可以使用下拉列表在&#x200B;**[!UICONTROL Selected]**、**[!UICONTROL All]**&#x200B;和&#x200B;**[!UICONTROL Primary]**&#x200B;之间切换，或者使用![Search](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg)字段。

      * **[!UICONTROL 已识别应用程序(ID)]**，
      * **[!UICONTROL 事件类型(eventType)]**，
      * **[!UICONTROL 主要（主要）]**。

      ![编辑事件字段](assets/ajo-event-fields.png){zoomable="yes"}

      然后选择&#x200B;**[!UICONTROL 确定]**。

   1. 选择![事件ID条件](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)字段旁边的&#x200B;**[!UICONTROL 编辑]**。

      1. 在&#x200B;**[!UICONTROL 添加事件ID条件]**&#x200B;对话框中，将&#x200B;**[!UICONTROL 事件类型(eventType)]**&#x200B;拖放到&#x200B;**[!UICONTROL 将元素拖放到此处]**。
      1. 在弹出窗口中，滚动到底部并选择&#x200B;**[!UICONTROL application.test]**（这是您之前作为[更新架构](#update-your-schema)的一部分添加到事件类型列表中的事件类型）。 然后向上滚动到顶部并选择&#x200B;**[!UICONTROL 确定]**。
      1. 选择&#x200B;**[!UICONTROL 确定]**&#x200B;以保存条件。
         ![编辑事件条件](assets/ajo-edit-condition.png){zoomable="yes"}

   1. 从&#x200B;**[!UICONTROL 命名空间]**&#x200B;列表中选择&#x200B;**[!UICONTROL ECID (ECID)]**。 自动使用&#x200B;**[!UICONTROL 映射identityMap]**&#x200B;的键ECID的第一个元素的ID填充&#x200B;**[!UICONTROL 配置文件标识符]**&#x200B;字段。
   1. 选择&#x200B;**[!UICONTROL 保存]**。
      ![编辑事件步骤2](assets/ajo-edit-event2.png){zoomable="yes"}

您刚刚创建了一个事件配置，该配置基于您之前在本教程中创建的“移动应用程序体验事件”架构。 此事件配置将使用您的特定事件类型(`application.test`)筛选传入的体验事件，因此，只有从该移动应用程序发起的特定类型的事件才会触发您在下一步中构建的历程。 在现实场景中，您可能希望从外部服务发送推送通知。 但是，同样的概念也适用：从外部应用程序将体验事件发送到Experience Platform，该事件具有特定字段，您可以在这些事件触发历程之前对其应用条件。

### 创建历程

您的下一步是创建在收到相应的事件时触发推送通知发送的历程。

1. 在Journey Optimizer UI中，从左边栏中选择&#x200B;**[!UICONTROL 历程]**。
1. 选择&#x200B;**[!UICONTROL 创建历程]**。
1. 在&#x200B;**[!UICONTROL 历程属性]**&#x200B;面板中：

   1. 输入历程的&#x200B;**[!UICONTROL 名称]**，例如`Luma - Test Push Notification Journey`。
   1. 输入历程的&#x200B;**[!UICONTROL 描述]**，例如`Journey for test push notifications in Luma mobile app`。
   1. 确保已选择&#x200B;**[!UICONTROL 允许重新进入]**，并将&#x200B;**[!UICONTROL 重新进入等待期]**&#x200B;设置为&#x200B;**[!UICONTROL 30]** **[!UICONTROL 秒]**。
   1. 选择&#x200B;**[!UICONTROL 确定]**。
      ![历程属性](assets/ajo-journey-properties.png){zoomable="yes"}

1. 返回历程画布，从&#x200B;**[!UICONTROL EVENTS]**，将![Event](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!DNL LumaTestEvent]**&#x200B;拖放到画布上，其中显示&#x200B;**[!UICONTROL 选择一个进入事件或读取受众活动]**。

   * 在&#x200B;**[!UICONTROL Events： LumaTestEvent]**&#x200B;面板中，输入&#x200B;**[!UICONTROL 标签]**，例如`Luma Test Event`。

1. 从&#x200B;**[!UICONTROL ACTIONS]**&#x200B;下拉列表中，将![推送](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL 推送]**&#x200B;拖放到显示于![活动右侧的](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)添加&#x200B;**[!DNL LumaTestEvent]**&#x200B;上。 在&#x200B;**[!UICONTROL 操作：推送]**&#x200B;窗格中：

   1. 提供&#x200B;**[!UICONTROL 标签]**，例如`Luma Test Push Notification`，提供&#x200B;**[!UICONTROL 描述]**，例如`Test push notification for Luma mobile app`，从&#x200B;**[!UICONTROL 类别]**&#x200B;列表中选择&#x200B;**[!UICONTROL 事务型]**，并从&#x200B;**[!DNL Luma]**&#x200B;推送表面&#x200B;**[!UICONTROL 中选择]**。
   1. 选择![编辑](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 编辑内容]**&#x200B;以开始编辑实际的推送通知。

      ![推送属性](assets/ajo-push-properties.png){zoomable="yes"}

      在&#x200B;**[!UICONTROL 推送通知]**&#x200B;编辑器中：

      1. 输入&#x200B;**[!UICONTROL 标题]**，例如`Luma Test Push Notification`，并输入&#x200B;**[!UICONTROL 正文]**，例如`Test push notification for Luma mobile app`。
      1. 或者，您可以在&#x200B;**[!UICONTROL 添加媒体]**&#x200B;中输入指向图像(.png或.jpg)的链接。 如果这样做，则图像是推送通知的一部分。 请注意，如果这样做，您需要注意在移动设备应用程序中正确处理图像。
      1. 要保存并退出编辑器，请选择![左V形](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg)。

         ![推送编辑器](assets/ajo-push-editor.png){zoomable="yes"}

   1. 要保存并完成推送通知定义，请选择&#x200B;**[!UICONTROL 确定]**。

1. 您的历程应如下所示。 选择&#x200B;**[!UICONTROL 发布]**&#x200B;以发布并激活您的历程。
   ![已完成历程](assets/ajo-journey-finished.png){zoomable="yes"}


## 触发推送通知

您已具备发送推送通知的所有要素。 剩下的问题是如何触发此推送通知。 实质上，它与您之前看到的相同：只需发送具有适当有效负载的体验事件（如[Events](events.md)中的）。

此时，您即将发送的体验事件未构建为简单的XDM词典。 您即将使用表示推送通知有效负载的`struct`。 定义专用数据类型是如何在应用程序中实施构建体验事件有效负载的替代方法。

请注意，仅出于说明目的，您才会从应用程序内发送推送通知。 更典型的情况是，您从其他应用程序或服务发送体验事件（触发推送通知历程）。

>[!BEGINTABS]

>[!TAB iOS]

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL 模型]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]**，并检查代码。

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   该代码呈现了您要发送的以下简单有效负载，以触发测试推送通知历程。

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**，并将以下代码添加到`func sendTestPushEvent(applicationId: String, eventType: String)`：

   ```swift
   // Create payload and send experience event
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   此代码使用提供给函数（`testPushPayload`和`applicationId`）的参数创建一个`eventType`实例，然后在将有效负载转换为字典时调用`sendExperienceEvent`。 此代码还通过使用Swift的基于`await`和`async`的并发模型来考虑调用Adobe Experience Platform SDK的异步方面。

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]**。 在推送通知按钮定义中，添加以下代码以发送测试推送通知体验事件有效负载，以便在点击该按钮时触发您的历程。

   ```swift
   // Setting parameters and calling function to send push notification
   Task {
       let eventType = testPushEventType
       let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
       await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)
   }
   ```

>[!TAB Android]

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL xdm]** > **[!UICONTROL TestPushPayload.kt]**，并检查代码。

   ```kotlin
   import com.google.gson.annotations.SerializedName
   
   data class TestPushPayload(
      @SerializedName("application") val application: Application,
      @SerializedName("eventType") val eventType: String
   ) {
      fun asMap(): Map<String, Any> {
         return mapOf(
               "application" to application.asMap(),
               "eventType" to eventType
         )
      }
   }
   
   data class Application(
      @SerializedName("id") val id: String
   ) {
      fun asMap(): Map<String, Any> {
         return mapOf(
               "id" to id
         )
      }
   }
   ```

   该代码呈现了您要发送的以下简单有效负载，以触发测试推送通知历程。

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**，并将以下代码添加到`func sendTestPushEvent(applicationId: String, eventType: String)`：

   ```kotlin
   // Create payload and send experience event
   val testPushPayload = TestPushPayload(
      Application(applicationId),
      eventType
   )
   sendExperienceEvent(testPushPayload.asMap())
   ```

   此代码使用提供给函数（`testPushPayload`和`applicationId`）的参数创建一个`eventType`实例，然后在将有效负载转换为映射时调用`sendExperienceEvent`。

1. 在Android Studio导航器中导航到&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.android.tutorial]** > **[!DNL views]** > **[!UICONTROL ConfigView.kt]**。 在推送通知按钮定义中，添加以下代码以发送测试推送通知体验事件有效负载，以便在点击该按钮时触发您的历程。

   ```kotlin
   // Setting parameters and calling function to send push notification
   val eventType = testPushEventType
   val applicationId = context.packageName
   scope.launch {
         MobileSDK.shared.sendTestPushEvent(
            applicationId,
            eventType
         )
   }
   ```


>[!ENDTABS]

## 使用应用程序进行验证

要验证推送通知事件和历程，请执行以下操作：

>[!BEGINTABS]

>[!TAB iOS]

1. 使用![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)，在模拟器中或在Xcode的物理设备上重建并运行应用程序。

1. 转到&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡。

1. 点按&#x200B;**[!UICONTROL 推送通知]**。


   您会看到推送通知显示在应用程序顶部。

   <img src="assets/ajo-test-push.png" width="300" />

>[!TAB Android]

1. 使用![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)，在模拟器中或在Android Studio的物理设备上重建并运行应用程序。

1. 转到&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡。

1. 点按&#x200B;**[!UICONTROL 推送通知]**。

   您会看到推送通知显示在应用程序顶部。

   <img src="assets/ajo-test-push-android.png" width="300" />

>[!ENDTABS]

如何在应用程序本身中处理和显示推送通知不属于此部分的主题。 每个平台都实施处理并以特定方式显示通知。 有关详细信息，请参阅：

* 对于iOS： [用户通知](https://developer.apple.com/documentation/usernotifications)
* 对于Android： [Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)

## 后续步骤

现在，您应该拥有在应用程序中处理推送通知的所有工具。 例如，您可以在Journey Optimizer中构建一个历程，当应用程序用户登录时，该历程会发送欢迎推送通知。 或确认推送通知（当用户在该应用程序中购买产品时）。 或输入位置的地理围栏（如您在[位置](places.md)课程中所见）。

>[!SUCCESS]
>
>现在，您已使用适用于Experience Platform Mobile SDK的Journey Optimizer和Journey Optimizer扩展为推送通知启用应用程序。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有任何疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享这些内容。

下一步： **[创建并发送应用程序内消息](journey-optimizer-inapp.md)**
