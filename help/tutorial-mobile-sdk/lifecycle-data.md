---
title: 生命周期数据
description: 了解如何在移动设备应用程序中收集生命周期数据。
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 生命周期数据

了解如何在移动设备应用程序中收集生命周期数据。

Adobe Experience Platform Mobile SDK生命周期扩展允许从您的移动设备应用程序中收集生命周期数据。 Adobe Experience Platform边缘网络扩展将此生命周期数据发送到平台边缘网络，然后根据您的数据流配置将其转发到其他应用程序和服务。 进一步了解 [生命周期扩展](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network) （在产品文档中）。


## 先决条件

* 已成功构建并运行安装并配置了SDK的应用程序。
* 导入了保障SDK。

   ```swift
   import AEPAssurance
   ```

* 注册了保证扩展，如 [上一课](install-sdks.md).

## 学习目标

在本课程中，您将：

* 将生命周期字段组添加到架构。
* 当应用程序在前台和后台之间移动时，通过正确启动/暂停来启用准确的生命周期量度。
* 将数据从应用程序发送到Platform Edge Network。
* 在保证中验证。

## 将生命周期字段组添加到架构

您在 [上一课](create-schema.md) 已包含生命周期字段，因此您可以跳过此步骤。 如果您未在自己的应用程序中使用消费者体验事件字段组，则可以通过执行以下操作来添加生命周期字段：

1. 按照 [上一课](create-schema.md).
1. 打开“Luma应用程序”架构，然后选择 **[!UICONTROL 添加]**.
   ![选择添加](assets/mobile-lifecycle-add.png)
1. 在搜索栏中，输入“生命周期”。
1. 选中旁边的复选框 **[!UICONTROL AEP移动设备生命周期详细信息]**.
1. 选择 **[!UICONTROL 添加字段组]**.
   ![添加字段组](assets/mobile-lifecycle-lifecycle-field-group.png)
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![保存](assets/mobile-lifecycle-lifecycle-save.png)


## 实施更改

现在，您可以更新 `AppDelegate.swift` 要注册生命周期事件，请执行以下操作：

1. 启动后，如果您的应用程序正在从后台状态恢复，iOS可能会调用 `applicationWillEnterForeground:` 委托方法。 Add `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 当应用程序进入后台时，暂停从应用程序的 `applicationDidEnterBackground:` 委托方法。

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>对于iOS 13及更高版本，请查看 [文档](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle#register-lifecycle-with-mobile-core-and-add-appropriate-start-pause-calls) 代码略有不同。

## 通过保证进行验证

1. 查看 [设置说明](assurance.md) 部分，并将您的模拟器或设备连接到“保证”。
1. 启动应用程序。
1. 将应用程序发送到后台。 检查 `LifecyclePause`.
1. 将应用程序置于前台。 检查 `LifecycleResume`.
   ![验证生命周期](assets/mobile-lifecycle-lifecycle-assurance.png)


## 将数据转发到Platform Edge Network

上一个练习将前台事件和后台事件调度到Mobile SDK。 要将这些事件发送到Platform Edge Network，请按照列出的步骤操作 [此处](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network#configure-a-rule-to-forward-lifecycle-metrics-to-platform). 事件发送到Platform Edge Network后，将根据您的数据流配置将其转发到其他应用程序和服务。

添加规则以将生命周期事件发送到Platform Edge Network后，您应会看到 `Application Close (Background)` 和 `Application Launch (Foreground)` 在“保证”中包含XDM数据的事件。

![验证发送到Platform Edge的生命周期](assets/mobile-lifecycle-edge-assurance.png)



下一个： **[跟踪事件](events.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)