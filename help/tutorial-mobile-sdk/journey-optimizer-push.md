---
title: Adobe Journey Optimizer推送消息
description: 了解如何使用Platform Mobile SDK和Adobe Journey Optimizer创建到移动设备应用程序的推送消息。
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# Adobe Journey Optimizer推送消息

了解如何使用Platform Mobile SDK和Adobe Journey Optimizer为移动设备应用程序创建推送消息。

Journey Optimizer允许您创建历程并向目标受众发送消息。 在通过Journey Optimizer发送推送通知之前，必须确保已部署正确的配置和集成。 要了解Adobe Journey Optimizer中的推送通知数据流，请参阅 [文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>本课程是可选的，仅适用于希望发送推送消息的Adobe Journey Optimizer用户。


## 先决条件

* 已成功构建并运行安装并配置了SDK的应用程序。
* 对Adobe Journey Optimizer的访问权限和足够的权限，如所述 [此处](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 此外，您还需要拥有对以下Adobe Journey Optimizer功能的足够权限。
   * 创建应用程序表面。
   * 创建历程
   * 创建消息.
   * 创建消息预设.
* 具有足够权限创建证书、标识符和密钥的付费Apple开发人员帐户。
* 用于测试的物理iOS设备。

## 学习目标

在本课程中，您将：

* 在Apple推送通知服务(APN)中注册应用程序ID。
* 创建 **[!UICONTROL 应用程序表面]** 在AJO中。
* 更新 **[!UICONTROL 模式]** ，以包含推送消息字段。
* 安装和配置 **[!UICONTROL Adobe Journey Optimizer]** 标记扩展。
* 更新您的应用程序以包含AJO标记扩展。
* 在保证中验证设置。
* 发送测试消息。


## 在APN中注册应用程序ID

以下步骤不是特定于Adobe Experience Cloud的，旨在引导您完成APN配置。

### 创建 `.p8` 私钥

1. 在Apple开发人员门户中，导航到 **[!UICONTROL 键]**.
1. 选择+图标以创建键。
   ![创建新键](assets/mobile-push-apple-dev-new-key.png)

1. 提供 **[!UICONTROL 键名称]**.
1. 选择 **[!UICONTROL APN]** 复选框。
1. 选择 **[!UICONTROL 继续]**.
   ![配置新密钥](assets/mobile-push-apple-dev-config-key.png)
1. 查看配置并选择 **[!UICONTROL 注册]**.
1. 下载 `.p8` 私钥。 它用在应用程序表面配置中。
1. 记下 **[!UICONTROL 密钥ID]**. 它用在应用程序表面配置中。

其他文档可以是 [此处](https://help.apple.com/developer-account/#/devcdfbb56a3).

### 检索您的Apple开发人员团队ID

1. 在Apple开发人员门户中，导航到 **[!UICONTROL 会员资格]**.
1. 您的 **[!UICONTROL 团队ID]** 列在您其他会员信息旁边。 它用在应用程序表面配置中。

## 在数据收集中添加您的应用程序推送凭据

1. 从 [数据收集界面](https://experience.adobe.com/data-collection?lang=zh-Hans/)，选择左侧面板中的应用程序曲面选项卡。
1. 选择 **[!UICONTROL 创建应用程序曲面]** 创建配置。
   ![app surface主页](assets/mobile-push-app-surface.png)
1. 输入 **[!UICONTROL 名称]** 例如，对于配置 `Luma App Tutorial`  .
1. 在移动应用程序配置中，选择 **[!UICONTROL AppleiOS]**.
1. 在应用程序ID(iOS包ID)字段中输入移动设备应用程序包ID。 如果您与Luma应用程序一起使用，则该值为 `com.adobe.luma.tutorial`.
1. 打开 **[!UICONTROL 推送凭据]** 按钮以添加您的凭据。
1. 拖放 `.p8` **Apple推送通知身份验证密钥** 文件。
1. 提供键ID，该键ID是在创建 `p8` 身份验证密钥。 可在的键值选项卡下找到 **证书、标识符和配置文件** 页面。
1. 提供团队ID。 这是一个字符串值，可在 **会员资格** 选项卡。
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![应用程序表面配置](assets/mobile-push-app-surface-config.png)

## 安装Adobe Journey Optimizer标记扩展

1. 导航到 [!UICONTROL 标记] > [!UICONTROL 扩展] > [!UICONTROL 目录]，并查找 **[!UICONTROL Adobe Journey Optimizer]** 扩展。
1. 安装扩展。
   ![安装ajo扩展](assets/mobile-push-tags-install.png)
1. 选择 `CJM Push Tracking Experience Event Dataset` Adobe Experience Platform数据集。
   ![AJO扩展设置](assets/mobile-push-tags-ajo.png)
1. 选择 **[!UICONTROL 保存到库并构建]**.

>[!NOTE]
>如果您没有看到“CJM推送跟踪体验事件数据集”选项，请联系客户关怀团队。

## 在应用程序中实施Adobe Journey Optimizer

如前面的课程中所述，安装移动标记扩展仅提供配置。 接下来，您必须安装并注册消息传送SDK。 如果这些步骤不明确，请查看 [安装SDK](install-sdks.md) 中。

>[!NOTE]
>
>如果您完成了 [安装SDK](install-sdks.md) 部分，则表明SDK已经安装，您可以跳转到步骤#7。

1. 打开 `Podfile` 并添加以下行并保存文件。

   `pod 'AEPMessaging', '~>1'`
1. 打开终端并导航到包含您的 `Podfile`.
1. 通过执行命令安装SDK `pod install`.
   ![验证同意](assets/mobile-push-terminal-install.png)
1. 打开Xcode并导航到 `AppDelegate.swift`.
1. 将以下内容添加到导入列表中。

   `import AEPMessaging`
1. 添加 `Messaging.self` 到要注册的扩展数组。
1. 将以下函数添加到文件中。

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   此函数可检索应用程序所安装设备特有的设备令牌，并将其发送到Adobe/Apple以进行推送消息传递。

## 通过发送测试推送消息进行验证

1. 查看 [设置说明](assurance.md) 中。
1. 在您的物理设备上安装应用程序。
1. 使用生成的保证URL启动应用程序。
1. 将应用程序发送到后台。
1. 在保证UI中，选择 **[!UICONTROL 配置]**.
   ![配置单击](assets/mobile-push-validate-config.png)
1. 选择 **[!UICONTROL +]** 按钮 **[!UICONTROL 推送调试]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/mobile-push-validate-save.png)
1. 选择 **[!UICONTROL 推送调试]** 的上界。
1. 从 **[!UICONTROL 客户端列表]**.
1. 确认您未收到任何错误。
   ![验证](assets/mobile-push-validate-confirm.png)
1. 向下滚动并选择 **[!UICONTROL 发送测试推送通知]**.
1. 确认您没有收到和错误，并且在设备上收到了消息。
   ![发送测试推送](assets/mobile-push-validate-send-test.png)

下一个： **[结论和后续步骤](conclusion.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)