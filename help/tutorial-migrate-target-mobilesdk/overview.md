---
title: 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解如何将移动应用程序实施从Adobe Target迁移到Adobe Journey Optimizer - Decisioning扩展
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展

本指南面向经验丰富的Adobe Target实施人员，帮助他们了解如何将现有AdobeExperience Platform Mobile SDK实施从Adobe Target扩展迁移到Adobe Journey Optimizer - Decisioning扩展。

Adobe Experience Platform Mobile SDK支持您的移动应用程序中的端到端参与。 Target扩展以Mobile SDK为基础，可帮助您通过Adobe Target使应用程序体验个性化。 Decisioning扩展是一种在移动设备应用程序中实施Adobe Target的新方法，它使用Adobe Experience PlatformEdge Network功能，帮助将Target与Real-Time CDP和Journey Optimizer等基于平台的应用程序集成。

## 主要优点

与Target扩展相比，Adobe Journey Optimizer Decisioning扩展具有以下优势：

* 更快地从[Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hans)共享受众
* 将Target与Journey Optimizer集成以支持[Offer decisioning交付](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 与Adobe Analytics更紧密集成，后者不依赖拼接来自单独网络调用的信息
* 为开发人员增加实施灵活性

可以说，迁移给Target客户带来的最大好处是与Real-time Customer Data Platform集成。 Real-Time CDP基于摄取到Experience Platform的所有数据及其实时客户档案功能提供了巨大的受众构建功能。 内置的数据治理框架可自动负责任地使用该数据。 通过客户人工智能，可轻松使用机器学习模型构建倾向性和流失模型，模型的输出可共享回Adobe Target。 最后，可选的Healthcare和Privacy &amp; Security Shield加载项的客户可以使用同意强制执行功能轻松地强制执行个别客户的同意首选项。 要在您的移动渠道中使用这些Real-Time CDP功能，需要使用Platform Mobile SDK和Decisioning扩展。


>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
