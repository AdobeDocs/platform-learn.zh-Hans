---
title: 更新受众和配置文件脚本 — 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解如何更新Adobe Target受众和配置文件脚本，以便与Experience PlatformWeb SDK兼容。
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 更新Target受众和配置文件脚本，以确保Adobe Journey Optimizer - Decisioning Mobile扩展兼容性


## 调整受众


有关更多信息和最佳实践，请参阅有关[配置文件脚本](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)的专用文档。

## 更新动态内容的参数令牌



如果您选择在迁移后进行调整以考虑新的XDM mbox参数名称，请确保在迁移事件期间暂停任何受影响的活动，以防止活动向访客显示错误。

接下来，了解如何[验证Target实施](validate.md)。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
