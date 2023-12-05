---
title: 使用Platform Mobile SDK收集生命周期数据
description: 了解如何在移动应用程序中收集生命周期数据。
jira: KT-14630
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 2%

---

# 收集生命周期数据

了解如何在移动应用程序中收集生命周期数据。

Adobe Experience Platform Mobile SDK生命周期扩展支持来自您的移动应用程序的收集生命周期数据。 Adobe Experience Platform Edge Network扩展会将此生命周期数据发送到Platform Edge Network，之后将根据您的数据流配置将其转发到其他应用程序和服务。 了解关于 [生命周期扩展](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) 在产品文档中。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。 在本课程中，您已启动生命周期监控。 请参阅 [安装SDK — 更新AppDelegate](install-sdks.md#update-appdelegate) 以进行审核。
* 已注册保证扩展，如中所述 [上一课程](install-sdks.md).

## 学习目标

在本课程中，您将执行以下操作：

<!--
* Add lifecycle field group to the schema.
* -->
* 在应用程序在前台与后台之间切换时，通过正确启动/暂停来实现准确的生命周期量度。
* 将数据从应用程序发送到Platform Edge Network。
* 在Assurance中进行验证。

<!--
## Add lifecycle field group to schema

The Consumer Experience Event field group you added in the [previous lesson](create-schema.md) already contains the lifecycle fields, so you can skip this step. If you don't use Consumer Experience Event field group in your own app, you can add the lifecycle fields by doing the following:

1. Navigate to the schema interface as described in the [previous lesson](create-schema.md).
1. Open the **Luma Mobile App Event Schema** schema and select **[!UICONTROL Add]** next to Field groups.
    ![select add](assets/lifecycle-add.png)
1. In the search bar, enter "lifecycle".
1. Select the checkbox next to **[!UICONTROL AEP Mobile Lifecycle Details]**.
1. Select **[!UICONTROL Add field groups]**.
    ![add field group](assets/lifecycle-lifecycle-field-group.png)
1. Select **[!UICONTROL Save]**.
    ![save](assets/lifecycle-lifecycle-save.png)
-->

## 实施更改

现在，您可以更新项目以注册生命周期事件。

1. 导航到 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** 在Xcode项目导航器中。

1. 启动后，如果您的应用程序从后台状态恢复，iOS可能会调用您的 `sceneWillEnterForeground:` 委托方法，并且您要在此触发生命周期开始事件。 将此代码添加到 `func sceneWillEnterForeground(_ scene: UIScene)`：

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 当应用程序进入后台时，您希望暂停来自应用程序的生命周期数据收集 `sceneDidEnterBackground:` 委托方法。 将此代码添加到  `func sceneDidEnterBackground(_ scene: UIScene)`：

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   ```

## 使用保障进行验证

1. 查看 [设置说明](assurance.md#connecting-to-a-session) 部分以将模拟器或设备连接到Assurance。
1. 将应用程序发送到后台。 检查 **[!UICONTROL LifecyclePause]** Assurance UI中的事件。
1. 将应用程序置于前台。 检查 **[!UICONTROL LifecycleResume]** Assurance UI中的事件。
   ![验证生命周期](assets/lifecycle-lifecycle-assurance.png)


## 将数据转发到Platform Edge Network

上一个练习将前台和后台事件调度到Adobe Experience Platform Mobile SDK。 要将这些事件转发到Platform Edge Network，请执行以下操作：

1. 选择 **[!UICONTROL 规则]** 在Tags属性中。
   ![创建规则](assets/rule-create.png)
1. 选择 **[!UICONTROL 初始构建]** 作为要使用的库。
1. 选择&#x200B;**[!UICONTROL 创建新规则]**。
   ![创建新规则](assets/rules-create-new.png)
1. 在 **[!UICONTROL 创建规则]** 屏幕，输入 `Application Status` 对象 **[!UICONTROL 名称]**.
1. 选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加]** 以下 **[!UICONTROL 活动]**.
   ![“创建规则”对话框](assets/rule-create-name.png)
1. 在 **[!UICONTROL 事件配置]** 步骤：
   1. 选择 **[!UICONTROL 移动核心]** 作为 **[!UICONTROL 扩展名]**.
   1. 选择 **[!UICONTROL 前景]** 作为 **[!UICONTROL 事件类型]**.
   1. 选择&#x200B;**[!UICONTROL 保留更改]**。
      ![规则事件配置](assets/rule-event-configuration.png)
1. 返回 **[!UICONTROL 创建规则]** 屏幕，选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加]** 旁边 **[!UICONTROL 移动核心 — 前台]**.
   ![下一个事件配置](assets/rule-event-configuration-next.png)
1. 在 **[!UICONTROL 事件配置]** 步骤：
   1. 选择 **[!UICONTROL 移动核心]** 作为 **[!UICONTROL 扩展名]**.
   1. 选择 **[!UICONTROL 背景]** 作为 **[!UICONTROL 事件类型]**.
   1. 选择&#x200B;**[!UICONTROL 保留更改]**。
      ![规则事件配置](assets/rule-event-configuration-background.png)
1. 返回 **[!UICONTROL 创建规则]** 屏幕，选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加]** 下 **[!UICONTROL 操作]**.
   ![规则添加操作](assets/rule-action-button.png)
1. 在 **[!UICONTROL 操作配置]** 步骤：
   1. 选择 **[!UICONTROL AdobeExperience Edge Network]** 作为 **[!UICONTROL 扩展名]**.
   1. 选择 **[!UICONTROL 将事件转发到Edge Network]** 作为 **[!UICONTROL 操作类型]**.
   1. 选择&#x200B;**[!UICONTROL 保留更改]**。
      ![规则操作配置](assets/rule-action-configuration.png)
1. 选择 **[!UICONTROL 保存到库]**.
   ![规则 — 保存到库](assets/rule-save-to-library.png)
1. 选择 **[!UICONTROL 生成]** 重建库。
   ![规则 — 内部版本](assets/rule-build.png)

成功构建资产后，事件将发送到Platform Edge Network，并根据数据流配置转发到其他应用程序和服务。

您应该看到 **[!UICONTROL 应用程序关闭（背景）]** 和 **[!UICONTROL 应用程序启动（前台）]** 包含Assurance中的XDM数据的事件。

![验证发送到Platform Edge的生命周期](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>现在，您已将应用程序设置为将应用程序状态（前台、后台）事件发送到Adobe Experience Platform Edge Network以及您在数据流中定义的所有服务。
>
> 感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[跟踪事件数据](events.md)**
