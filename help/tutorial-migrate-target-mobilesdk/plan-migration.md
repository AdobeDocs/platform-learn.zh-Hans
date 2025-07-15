---
title: 规划迁移 — 将移动应用程序中的Adobe Target实施迁移到Offer Decisioning和Target扩展
description: 了解at.js与Platform Web SDK之间的主要区别，以及如何规划您的迁移工作。
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 规划迁移

从Target扩展迁移到Offer Decisioning和Target扩展的工作量级别取决于当前实施的复杂性和所使用的Target功能。

无论您的实施是多么简单或复杂，在迁移之前充分了解您的当前状态都非常重要。 本指南可帮助您划分当前实施的组件，并制定可管理的计划来迁移每个组件。

迁移过程涉及以下关键步骤：

1. 评估您当前的实施并确定迁移方法
1. 设置初始组件以连接到Adobe Experience Platform Edge Network
1. 更新了基础实施，以便将Target扩展替换为Offer Decisioning扩展和Target扩展
1. 针对您的特定用例，增强优化SDK实施。 这可能涉及传递其他参数、使用响应令牌等。
1. 更新Target界面中的对象，例如配置文件脚本、活动和受众定义
1. 在生产应用程序中进行切换之前，请验证最终实施

>[!INFO]
>
>在Adobe Experience Platform Mobile SDK生态系统内，扩展由导入到您的应用程序中的SDK实施，这些SDK可能具有不同的名称：
>
> * **Target SDK**&#x200B;实现&#x200B;**Adobe Target扩展**
> * **优化SDK**&#x200B;实现&#x200B;**Offer Decisioning和Target扩展**


接下来，查看Target扩展与Offer Decisioning和Target扩展的详细[比较](detailed-comparison.md)，以更好地了解技术差异，并确定需要额外关注的领域。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Offer Decisioning和Target扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625)中发帖让我们知道。
