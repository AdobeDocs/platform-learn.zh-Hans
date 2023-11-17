---
title: 生命周期数据
description: 了解如何在移动应用程序中收集生命周期数据。
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 生命周期数据

了解如何在移动应用程序中收集生命周期数据。

>[!INFO]
>
> 2023年11月下旬，本教程将替换为使用新示例移动应用程序的新教程

Adobe Experience Platform Mobile SDK生命周期扩展支持来自您的移动应用程序的收集生命周期数据。 Adobe Experience Platform Edge Network扩展会将此生命周期数据发送到Platform Edge Network，之后将根据您的数据流配置将其转发到其他应用程序和服务。 了解关于 [生命周期扩展](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) 在产品文档中。


## 先决条件

* 在安装和配置SDK的情况下成功构建和运行应用程序。
* 已导入Assurance SDK。

  ```swift
  import AEPAssurance
  ```

* 已注册保证扩展，如中所述 [上一课程](install-sdks.md).

## 学习目标

在本课程中，您将执行以下操作：

* 将生命周期字段组添加到架构。
* 在应用程序在前台与后台之间切换时，通过正确启动/暂停来实现准确的生命周期量度。
* 将数据从应用程序发送到Platform Edge Network。
* 在Assurance中进行验证。

## 将生命周期字段组添加到架构

您在中添加的消费者体验事件字段组 [上一课程](create-schema.md) 已包含生命周期字段，因此您可以跳过此步骤。 如果您没有在自己的应用程序中使用使用者体验事件字段组，则可以通过执行以下操作来添加生命周期字段：

1. 导航到架构界面，如 [上一课程](create-schema.md).
1. 打开“Luma应用程序”架构并选择 **[!UICONTROL 添加]**.
   ![选择“添加”](assets/mobile-lifecycle-add.png)
1. 在搜索栏中，输入“lifecycle”。
1. 选中旁边的复选框 **[!UICONTROL AEP移动生命周期详细信息]**.
1. 选择&#x200B;**[!UICONTROL 添加字段组]**。
   ![添加字段组](assets/mobile-lifecycle-lifecycle-field-group.png)
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/mobile-lifecycle-lifecycle-save.png)


## 实施更改

现在您可以更新 `AppDelegate.swift` 注册生命周期事件：

1. 启动后，如果您的应用程序从后台状态恢复，iOS可能会调用您的 `applicationWillEnterForeground:` 委托方法。 Add `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 当应用程序进入后台时，暂停从应用程序的 `applicationDidEnterBackground:` 委托方法。

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>对于iOS 13及更高版本，请查看 [文档](https://developer.adobe.com/client-sdks/documentation/mobile-core/lifecycle/#register-lifecycle-with-mobile-core-and-add-appropriate-startpause-calls) 代码稍有不同。

## 使用保障进行验证

1. 查看 [设置说明](assurance.md) 并将模拟器或设备连接到Assurance。
1. 启动应用程序。
1. 将应用程序发送到后台。 检查 `LifecyclePause`.
1. 将应用程序置于前台。 检查 `LifecycleResume`.
   ![验证生命周期](assets/mobile-lifecycle-lifecycle-assurance.png)


## 将数据转发到Platform Edge Network

上一个练习将前台和后台事件调度到Mobile SDK。 要将这些事件发送到Platform Edge Network，请按照列出的步骤操作 [此处](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/#configure-a-rule-to-forward-lifecycle-metrics-to-platform). 将事件发送到Platform Edge Network后，将根据您的数据流配置将其转发到其他应用程序和服务。

添加将生命周期事件发送到Platform Edge Network的规则后，您应会看到 `Application Close (Background)` 和 `Application Launch (Foreground)` 包含Assurance中的XDM数据的事件。

![验证发送到Platform Edge的生命周期](assets/mobile-lifecycle-edge-assurance.png)



下一步： **[跟踪事件](events.md)**

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)