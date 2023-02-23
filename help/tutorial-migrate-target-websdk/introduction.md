---
title: 简介 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何将Adobe Target实施从at.js 2.x迁移到Adobe Experience Platform Web SDK。 主题包括加载JavaScript库、发送参数、渲染活动和其他值得注意的标注。
recommendations: catalog,noDisplay
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 5%

---

# 将Target从at.js 2.x迁移到平台Web SDK

本指南面向经验丰富的Adobe Target实施人员，介绍如何将at.js实施迁移到Adobe Experience Platform Web SDK。

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience Platform边缘网络与Experience Cloud服务进行交互。 此新库将单独Adobe应用程序库的功能整合到单个轻量级包中，以便充分利用Adobe Experience Platform的新增功能。

## 主要优点

与独立at.js库相比，Platform Web SDK的一些好处包括：

* 更快地从 [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hans)
* 将Target与Journey Optimizer集成以支持 [offer decisioning投放](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 使用功能 [第一方id](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=zh-Hans) 以生成持续时间较长的访客识别ECID
* 整合跨Adobe应用程序的网络调用
* 占用的空间更小，可提高页面速度量度
* 与Adobe Analytics的更紧密集成，不依赖于拼合来自单独网络调用的信息
* 为开发人员提供了更大的实施灵活性

可以说，迁移对Target客户最大的好处是与Real-time Customer Data Platform集成。 Real-Time CDP基于摄取到Experience Platform的完整数据及其实时客户资料功能，提供了巨大的受众构建功能。 内置的数据管理框架可自动负责地使用该数据。 Customer AI允许您轻松使用机器学习模型构建倾向和流失模型，其输出可共享回Adobe Target。 最后，可选的医疗保健和隐私与安全保护地址的客户可以使用同意强制功能轻松强制执行各个客户的同意首选项。 在Web渠道中使用这些RTCDP功能时，需要使用Platform Web SDK。

## 学习目标

在本教程结束后，您将能够：

* 了解at.js和Platform Web SDK之间的Target实施差异
* 为Target功能设置初始配置
* 将at.js库升级到平台Web SDK
* 渲染基于表单的活动和可视化体验编辑器活动
* 将参数传递到Target
* 跟踪转化事件
* 启用跨域支持
* 更新受众和配置文件脚本
* 验证实施
* 调试Target体验交付


## 先决条件

要完成本教程，您应首先：

* 对您当前的Target at.js实施有了技术上的了解
* 确保您具有 [编辑者或发布者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 的示例，以便您自己尝试使用
* 了解如何在Adobe Target中设置活动。 如果您需要刷新，以下教程和指南将对本课程很有帮助：
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [使用基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [创建体验定位活动](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

准备就绪后，成功迁移的第一步是 [了解迁移过程](migration-overview.md) 以及at.js和Platform Web SDK有何不同。

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).