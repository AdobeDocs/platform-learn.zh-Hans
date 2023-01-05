---
title: 规划 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何规划从at.js 2.x到Adobe Target Web SDK的Adobe Experience Platform实施。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 规划从at.js迁移到平台Web SDK

在您的网站上升级到Platform Web SDK之前，您应当评估当前的实施。

## 评估当前的at.js实施

成功迁移的第一步是要对您当前的at.js Target实施有更深入的了解。 您可以使用一些特性、函数和自定义代码来进行更新。 评估时请考虑以下事项：

### 支持哪些功能？

Platform Web SDK正处于持续积极的开发阶段，并且会定期添加功能和增强功能。 在评估当前的at.js实施时，请参阅 [支持的用例](https://github.com/orgs/adobe/projects/18/views/1) 页面以了解最新信息。

### 你今天用什么功能？

Platform Web SDK是一个新库，它将网站的所有Adobe解决方案整合到一个SDK中。 这支持更紧密的集成，并支持Adobe Experience Platform特有的新功能。 但是，这也意味着at.js函数无法向后兼容Platform Web SDK。 在评估当前实施时，请注意以下事项：

- at.js函数，如 `getOffer()` 和 `applyOffer()`
- 对Target全局设置的修改
- 与 Adobe Analytics 集成
- 使用闪烁缓解脚本
- 使用响应令牌
- 使用mbox、配置文件和实体参数
- 实施特有的自定义代码

### 您将采用哪种迁移方法？

重新查看at.js实施后，您需要确定一种迁移方法。 有两个选项：

- 在整个站点中同时迁移所有Adobe应用程序
- 逐页迁移

由于Platform Web SDK组合并支持多个Adobe应用程序，因此您必须协调其他Adobe应用程序(如Analytics和Audience Manager)的Target迁移。 应同时迁移给定页面上的所有Adobe库。 不支持在特定页面上混合实施适用于Target的Platform Web SDK和适用于Analytics的AppMeasurement。 但是，支持跨不同页面的混合实施，例如页面A上的Platform Web SDK，以及页面B上的带有AppMeasurement的at.js。

在迁移时，您应该先规划如何遵循贵公司的测试和发布新代码的流程，并在发布到生产环境之前使用开发、qa和暂存环境等内容。

>[!CAUTION]
>
>如果从具有一个库的页面重定向到具有其他库的页面，则分页迁移中不支持重定向选件


接下来，查看详细 [at.js与Platform Web SDK的比较](detailed-comparison.md) 更好地了解技术差异，并确定需要更多关注的领域。

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
