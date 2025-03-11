---
title: 将移动应用程序中的Adobe Target实施迁移到Adobe Journey Optimizer - Decisioning扩展
description: 了解如何将移动应用程序实施从Adobe Target迁移到Adobe Journey Optimizer - Decisioning扩展
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# 将移动应用程序中的Adobe Target实施迁移到Adobe Journey Optimizer - Decisioning扩展

本指南面向经验丰富的Adobe Target实施人员，帮助他们了解如何将现有Adobe Experience Platform Mobile SDK实施从Adobe Target扩展迁移到Adobe Journey Optimizer - Decisioning扩展。

Adobe Experience Platform Mobile SDK支持您的移动应用程序中的端到端参与。 Target扩展以Mobile SDK为基础，可帮助您通过Adobe Target使应用程序体验个性化。 Decisioning扩展是一种在移动设备应用程序中实施Adobe Target的新方法，它使用Adobe Experience Platform Edge Network功能，帮助将Target与Real-Time CDP和Journey Optimizer等基于平台的应用程序集成。

![显示通过带有Decisioning扩展的Edge Network连接到Target的移动SDK的图表](assets/datacollection.png)

>[!INFO]
>
>在Adobe Experience Platform Mobile SDK生态系统内，扩展由导入到您的应用程序中的SDK实施，这些SDK可能具有不同的名称：
>
> * **Target SDK**&#x200B;实现&#x200B;**Adobe Target扩展**
> * **优化SDK**&#x200B;实施&#x200B;**Adobe Journey Optimizer - Decisioning扩展**


## 主要优点

与Target扩展相比，Adobe Journey Optimizer Decisioning扩展具有以下优势：

* 更快地从[Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hans)共享受众
* 将Target与Journey Optimizer集成以支持[Offer Decisioning交付](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 与Adobe Analytics更紧密集成，后者不依赖拼接来自单独网络调用的信息
* 为开发人员增加实施灵活性

可以说，迁移给Target客户带来的最大好处是与Real-Time Customer Data Platform集成。 Real-Time CDP基于摄取到Experience Platform的所有数据及其实时客户档案功能提供了巨大的受众构建功能。 内置的数据治理框架可自动负责任地使用该数据。 通过客户人工智能，可轻松使用机器学习模型构建倾向性和流失模型，模型的输出可共享回Adobe Target。 最后，可选的Healthcare和Privacy &amp; Security Shield加载项的客户可以使用同意执行功能来强制实施单个客户的同意首选项。 要在您的移动渠道中使用这些Real-Time CDP功能，需要使用Platform Mobile SDK和Decisioning扩展。

## 迁移步骤

从Target扩展迁移到Decisioning扩展的工作量级别取决于当前实施的复杂性和使用的Target功能。

无论您的实施是多么简单或复杂，在迁移之前充分了解您的当前状态都非常重要。 本指南可帮助您划分当前实施的组件，并制定可管理的计划来迁移每个组件。

迁移过程涉及以下关键步骤：

1. 评估您当前的实施，包括：
   1. 使用的所有Target SDK API
   1. 修改Target全局设置
   1. 与 Adobe Analytics 集成
   1. mbox、配置文件和实体参数的使用
   1. 使用配置文件脚本和受众
   1. 您的实施特有的自定义代码
1. 设置初始组件以连接到Adobe Experience Platform Edge Network
1. 更新基本实施，将Target扩展替换为Decisioning扩展
1. 针对您的特定用例，增强优化SDK实施。 这可能涉及传递其他参数、使用响应令牌等。
1. 更新Target界面中的对象，例如配置文件脚本、活动和受众定义
1. 在生产应用程序中进行切换之前，请验证最终实施


>[!INFO]
>
>在Adobe Experience Platform Mobile SDK生态系统内，扩展由导入到您的应用程序中的SDK实施，这些SDK可能具有不同的名称：
>
> * **Target SDK**&#x200B;实现&#x200B;**Adobe Target扩展**
> * **优化SDK**&#x200B;实施&#x200B;**Adobe Journey Optimizer - Decisioning扩展**

接下来，查看Target扩展与Decisioning扩展的[详细比较](comparison.md)，以更好地了解技术差异，并确定需要额外关注的领域。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
