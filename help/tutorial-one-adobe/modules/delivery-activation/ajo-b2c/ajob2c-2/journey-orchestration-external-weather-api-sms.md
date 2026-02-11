---
title: Adobe Journey Optimizer — 外部天气API、SMS操作等
description: Adobe Journey Optimizer — 外部天气API、SMS操作等
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: f18a0ec9-ee56-42b9-98bd-b5e433d77043
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 3.2 Adobe Journey Optimizer：外部数据源和自定义操作

在本模块中，您将使用Adobe Journey Optimizer在线和离线倾听客户行为，并以智能、情境式和实时方式对其进行响应。 您已在模块6中初步体验了Adobe Journey Optimizer。 在本练习中，您将深入了解并探索更高级的用例，其中外部数据源用作历程的一部分。

## 学习目标

- 了解如何在Adobe Journey Optimizer中创建事件、外部数据源和历程
- 了解如何从开放天气API使用天气信息
- 了解如何使用Adobe Journey Optimizer中的Twilio和Slack等自定义操作目标

## 先决条件

- 访问Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 对Adobe Journey Optimizer的访问权限
- 访问开放天气API

## 业务上下文

作为一个品牌，您已在个性化在线体验方面投入了大量资金。 现在，您希望与离线体验保持上下文相关和相关性。
在本模块中，您将利用客户在离线商店的存在，然后在商店内通过店内屏幕上展示相关内容给该客户，从而提供个性化的体验，与此同时，我们希望实时向同一客户提供个性化的推送或短信消息。
作为品牌，您还了解上下文会极大地影响客户的兴趣，因此您想要引入客户位置的当前天气信息，以决定要显示的内容或促销活动。

>[!NOTE]
>
>请按照[为Chrome文档安装Chrome扩展](../../../getting-started/gettingstarted/ex1.md)中所述，安装、配置并使用Experience League扩展

## 练习

[3.2.1定义事件](./ex1.md)

了解如何使用Adobe Journey Optimizer定义自定义事件。

[3.2.2定义外部数据源](./ex2.md)

了解如何使用Adobe Journey Optimizer配置外部数据源。

[3.2.3定义自定义操作](./ex3.md)

了解如何使用Adobe Journey Optimizer定义外部操作。

[3.2.4创建历程和消息](./ex4.md)

将事件、数据源和操作合并到一个智能的上下文历程中。

[3.2.5触发您的历程](./ex5.md)

触发您的特定历程。

![技术内部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./../../../../overview.md)
