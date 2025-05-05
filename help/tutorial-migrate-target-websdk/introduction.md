---
title: 将Target从at.js 2.x迁移到Web SDK
description: 了解如何将Adobe Target实施从at.js 2.x迁移到Adobe Experience Platform Web SDK。 主题包括加载JavaScript库、发送参数、渲染活动以及其他值得注意的标注。
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# 将Target从at.js 2.x迁移到Platform Web SDK

本指南面向经验丰富的Adobe Target实施人员，帮助他们了解如何将at.js实施迁移到Adobe Experience Platform Web SDK。

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience Platform Edge Network与Experience Cloud服务交互。 此新库将各个Adobe应用程序库的功能整合到一个轻量级包中，以便充分利用新的Adobe Experience Platform功能。


>[!NOTE]
>
>类似的迁移教程可用于：
>
> * [Adobe Analytics](../tutorial-migrate-analytics-websdk/migration-to-websdk-overview.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/zh-hans/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> 由于Platform Web SDK支持多个Adobe应用程序，因此应同时迁移给定页面上的所有Adobe库。 例如，不支持在单个页面&#x200B;_上混合实施适用于Target的Web SDK和适用于Analytics的AppMeasurement。_ 但是，支持跨不同页面的混合实施，例如，在页面A上使用Web SDK，以及在页面B上使用AppMeasurement的at.js。



## 主要优点

与独立的at.js库相比，Platform Web SDK具有以下优势：

* 更快地从[Real-Time Customer Data Platform](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)共享受众
* 将Target与Journey Optimizer集成以支持[Offer Decisioning交付](https://experienceleague.adobe.com/zh-hans/docs/target/using/integrate/ajo/offer-decision)
* 能够使用[第一方ID](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids)生成ECID以延长访客识别持续时间
* 占用更小的空间以改进页面速度量度
* 为开发人员增加实施灵活性

可以说，迁移给Target客户带来的最大好处是与Real-Time Customer Data Platform集成。 Real-Time CDP基于摄取到Experience Platform的所有数据及其实时客户档案功能提供了巨大的受众构建功能。 一个内置的数据管理框架，可自动负责任地使用该数据。 通过客户人工智能，可轻松使用机器学习模型构建倾向性和流失模型，模型的输出可共享回Adobe Target。 最后，可选的Healthcare和Privacy &amp; Security Shield加载项的客户可以使用同意强制执行功能轻松地强制执行个别客户的同意首选项。 要在您的Web渠道中使用这些Real-Time CDP功能，需要使用Platform Web SDK。

## 学习目标

在本教程结束后，您将能够：

* 了解at.js和平台Web SDK之间的Target实施差异
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
* 确保您拥有Target实例的[编辑者或发布者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=zh-Hans#section_8C425E43E5DD4111BBFC734A2B7ABC80)，以便您可以自行尝试示例
* 了解如何在Adobe Target中设置活动。 如果您需要复习者，以下教程和指南对本课程很有帮助：
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html?lang=zh-Hans)
   * [使用基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html?lang=zh-Hans)
   * [创建体验目标选择活动](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html?lang=zh-Hans) 

准备就绪后，成功迁移的第一步是[了解迁移过程](migration-overview.md)以及at.js和平台Web SDK之间的差异。

>[!NOTE]
>
>我们致力于帮助您成功从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
