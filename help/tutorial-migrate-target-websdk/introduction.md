---
title: 将Target从at.js 2.x迁移到Web SDK
description: 了解如何将Adobe Target实施从at.js 2.x迁移到Adobe Experience Platform Web SDK。 主题包括加载JavaScript库、发送参数、渲染活动以及其他值得注意的标注。
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: eebe598e55228d038dfc2adb97df0f8ff03748ac
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# 将Target从at.js 2.x迁移到Platform Web SDK

本指南面向经验丰富的Adobe Target实施人员，帮助他们了解如何将at.js实施迁移到Adobe Experience Platform Web SDK。

Adobe Experience Platform Web SDK是客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience PlatformEdge Network与Experience Cloud服务进行交互。 此新库将各个Adobe应用程序库的功能整合到一个轻量级包中，以便充分利用Adobe Experience Platform的新增功能。

## 主要优点

与独立的at.js库相比，Platform Web SDK具有以下优势：

* 更快地从[Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hans)共享受众
* 将Target与Journey Optimizer集成以支持[Offer decisioning交付](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 能够使用[第一方ID](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=zh-Hans)生成ECID以延长访客识别持续时间
* 跨Adobe应用程序整合网络调用
* 占用更小的空间以改进页面速度量度
* 与Adobe Analytics更紧密集成，后者不依赖拼接来自单独网络调用的信息
* 为开发人员增加实施灵活性

可以说，迁移给Target客户带来的最大好处是与Real-time Customer Data Platform集成。 Real-Time CDP基于摄取到Experience Platform的所有数据及其实时客户档案功能提供了巨大的受众构建功能。 一个内置的数据管理框架，可自动负责任地使用该数据。 通过客户人工智能，可轻松使用机器学习模型构建倾向性和流失模型，模型的输出可共享回Adobe Target。 最后，可选的Healthcare和Privacy &amp; Security Shield加载项的客户可以使用同意强制执行功能轻松地强制执行个别客户的同意首选项。 要在您的Web渠道中使用这些RTCDP功能，需要使用Platform Web SDK。

## 学习目标

在本教程结束后，您将能够：

* 了解at.js与Platform Web SDK之间的Target实施差异
* 设置Target功能的初始配置
* 将at.js库升级到Platform Web SDK
* 渲染基于表单和可视化体验编辑器活动
* 将参数传递到Target
* 跟踪转化事件
* 启用跨域支持
* 更新受众和个人资料脚本
* 验证实施
* 调试Target体验交付


## 先决条件

要完成本教程，您应该首先：

* 从技术角度了解您当前的Target at.js实施
* 确保您拥有Target实例的[编辑者或发布者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80)，以便您可以自行尝试示例
* 了解如何在Adobe Target中设置活动。 如果您需要复习者，以下教程和指南对本课程很有帮助：
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [使用基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [创建体验定位活动](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

准备就绪后，成功迁移的第一步是[了解迁移过程](migration-overview.md)以及at.js和Platform Web SDK之间的差异。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
