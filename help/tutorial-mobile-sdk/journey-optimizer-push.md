---
title: Adobe Journey Optimizer推送消息
description: 了解如何使用Platform Mobile SDK和Adobe Journey Optimizer创建发送到移动应用程序的推送消息。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# Adobe Journey Optimizer推送消息

了解如何使用Platform Mobile SDK和Adobe Journey Optimizer为移动应用程序创建推送消息。

Journey Optimizer允许您创建历程并向目标受众发送消息。 在使用Journey Optimizer发送推送通知之前，您必须确保已实施适当的配置和集成。 要了解Adobe Journey Optimizer中的推送通知数据流，请参阅 [文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>本课程是可选的，仅适用于希望发送推送消息的Adobe Journey Optimizer用户。


## 先决条件

* 成功构建并运行安装并配置了SDK的应用程序。
* 对Adobe Journey Optimizer的访问权限和足够的权限，如所述 [此处](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 此外，您还需要拥有访问以下Adobe Journey Optimizer功能的足够权限。
   * 创建应用程序表面。
   * 创建历程
   * 创建消息.
   * 创建消息预设.
* 具有创建证书、标识符和密钥的足够访问权限的付费Apple开发人员帐户。
* 用于测试的物理iOS设备。

## 学习目标

在本课程中，您将执行以下操作：

* 向Apple推送通知服务(APN)注册应用程序ID。
* 创建 **[!UICONTROL 应用程序表面]** 在AJO中。
* 更新您的 **[!UICONTROL 架构]** 以包含推送消息字段。
* 安装和配置 **[!UICONTROL Adobe Journey Optimizer]** 标记扩展。
* 更新您的应用程序以包含AJO标记扩展。
* 验证Assurance中的设置。
* 发送测试消息。


## 使用APN注册应用程序ID

以下步骤并非特定于Adobe Experience Cloud，而是旨在引导您完成APN配置。

### 创建 `.p8` 私钥

1. 在Apple开发人员门户中，导航到 **[!UICONTROL 键]**.
1. 选择+图标以创建密钥。
   ![创建新密钥](assets/mobile-push-apple-dev-new-key.png)

1. 提供 **[!UICONTROL 密钥名称]**.
1. 选择 **[!UICONTROL APN]** 复选框。
1. 选择 **[!UICONTROL 继续]**.
   ![配置新密钥](assets/mobile-push-apple-dev-config-key.png)
1. 查看配置并选择 **[!UICONTROL 注册]**.
1. 下载 `.p8` 私钥。 它用于App Surface配置。
1. 记下 **[!UICONTROL 密钥ID]**. 它用于App Surface配置。

其他文档可以是 [在此处找到](https://help.apple.com/developer-account/#/devcdfbb56a3).

### 检索您的Apple开发人员团队ID

1. 在Apple开发人员门户中，导航到 **[!UICONTROL 会员资格]**.
1. 您的 **[!UICONTROL 团队编号]** 与其他会员资格信息一起列出。 它用于App Surface配置。

## 在数据收集中添加您的应用程序推送凭据

1. 从 [数据收集界面](https://experience.adobe.com/data-collection/)，选择左侧面板中的“应用程序表面”选项卡。
1. 选择 **[!UICONTROL 创建应用程序表面]** 以创建配置。
   ![应用程序表面主页](assets/mobile-push-app-surface.png)
1. 输入 **[!UICONTROL 名称]** 例如，对于配置 `Luma App Tutorial`  .
1. 在移动应用程序配置中，选择 **[!UICONTROL Apple iOS]**.
1. 在“应用程序ID (iOS捆绑包ID)”字段中输入移动应用程序捆绑包ID。 如果您将与Luma应用程序一起关注，则该值为 `com.adobe.luma.tutorial`.
1. 打开 **[!UICONTROL 推送凭据]** 按钮以添加您的凭据。
1. 拖放 `.p8` **Apple推送通知身份验证密钥** 文件。
1. 提供密钥ID，在创建期间分配的10个字符的字符串 `p8` 身份验证密钥。 它可以在中的键选项卡下找到 **证书、标识符和配置文件** 页面。
1. 提供团队ID。 这是一个字符串值，可以在 **会员资格** 选项卡。
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![应用程序表面配置](assets/mobile-push-app-surface-config.png)

## 安装Adobe Journey Optimizer标记扩展

1. 导航到 [!UICONTROL 标记] > [!UICONTROL 扩展] > [!UICONTROL 目录]，并查找 **[!UICONTROL Adobe Journey Optimizer]** 扩展。
1. 安装扩展。
   ![安装ajo扩展](assets/mobile-push-tags-install.png)
1. 选择 `CJM Push Tracking Experience Event Dataset` Adobe Experience Platform数据集。
   ![AJO扩展设置](assets/mobile-push-tags-ajo.png)
1. 选择 **[!UICONTROL 保存到库并生成]**.

>[!NOTE]
>如果您没有看到“CJM推送跟踪体验事件数据集”作为一个选项，请联系客户关怀团队。
>

## 在应用程序中实施Adobe Journey Optimizer

如前面的课程中所述，安装移动标记扩展仅提供配置。 接下来，您必须安装并注册消息SDK。 如果这些步骤不明确，请查阅 [安装SDK](install-sdks.md) 部分。

>[!NOTE]
>
>如果您已完成 [安装SDK](install-sdks.md) 部分，则该SDK已安装，您可以跳至步骤#7。

1. 打开您的 `Podfile` 并添加以下行并保存文件。

   `pod 'AEPMessaging', '~>1'`
1. 打开终端并导航到包含 `Podfile`.
1. 通过执行命令安装SDK `pod install`.
   ![验证同意](assets/mobile-push-terminal-install.png)
1. 打开代码并导航到 `AppDelegate.swift`.
1. 将以下内容添加到导入列表中。

   `import AEPMessaging`
1. 添加 `Messaging.self` 到要注册的扩展数组。
1. 将以下函数添加到该文件中。

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   此函数检索安装有应用程序的设备所特有的设备令牌，并将其发送到Adobe/Apple以进行推送消息投放。

## 通过发送测试推送消息进行验证

1. 查看 [设置说明](assurance.md) 部分。
1. 在物理设备上安装应用程序。
1. 使用保证生成的URL启动应用程序。
1. 将应用程序发送到后台。
1. 在保证UI中，选择 **[!UICONTROL 配置]**.
   ![配置点击](assets/mobile-push-validate-config.png)
1. 选择 **[!UICONTROL +]** 按钮旁边 **[!UICONTROL 推送调试]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/mobile-push-validate-save.png)
1. 选择 **[!UICONTROL 推送调试]** 从左侧导航栏中。
1. 从中选择设备 **[!UICONTROL 客户端列表]**.
1. 确认您未收到任何错误。
   ![验证](assets/mobile-push-validate-confirm.png)
1. 向下滚动并选择 **[!UICONTROL 发送测试推送通知]**.
1. 确认您没有收到和错误，并在设备上收到消息。
   ![发送测试推送](assets/mobile-push-validate-send-test.png)

下一步： **[结论和后续步骤](conclusion.md)**

>[!NOTE]
>
>感谢您投入时间来了解Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此分享这些内容 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)