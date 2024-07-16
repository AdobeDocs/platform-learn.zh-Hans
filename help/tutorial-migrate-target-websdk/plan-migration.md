---
title: 规划 | 将Target从at.js 2.x迁移到Web SDK
description: 了解如何从at.js 2.x到Adobe Experience Platform Web SDK的Adobe Target实施规划。
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 规划从at.js到Platform Web SDK的迁移

在网站上升级到Platform Web SDK之前，您应该评估当前的实施。

## 评估当前的at.js实施

成功迁移的第一步是深入了解您当前的at.js Target实施。 有些特性、函数和自定义代码可能需要更新。 评估时请考虑以下事项：

### 支持哪些功能？

Platform Web SDK正在持续积极开发，并定期添加功能和增强功能。 在您评估当前的at.js实施时，请参阅[支持的用例](https://github.com/orgs/adobe/projects/18/views/1)页面以了解最新信息。

### 您现在使用哪些功能？

Platform Web SDK是一个新库，它将网站的所有Adobe解决方案整合到一个SDK中。 这样可以实现更紧密的集成，并实现Adobe Experience Platform独有的新功能。 但是，这也意味着at.js函数无法向后兼容Platform Web SDK。 评估当前实施时，请注意以下事项：

- at.js函数，如`getOffer()`和`applyOffer()`
- 修改Target全局设置
- 与 Adobe Analytics 集成
- 使用闪烁缓解脚本
- 使用响应令牌
- mbox、配置文件和实体参数的使用
- 您的实施特有的自定义代码

### 您将采用哪种迁移方法？

在重新访问at.js实施后，您需要确定迁移方法。 有两个选项：

- 跨整个站点同时迁移所有Adobe应用程序
- 逐页迁移

由于Platform Web SDK可结合并启用多个Adobe应用程序，因此您必须协调其他Adobe应用程序(如Analytics和Audience Manager)的Target迁移。 给定页面上的所有Adobe库都应同时迁移。 不支持在特定页面上混合实施适用于Target的Platform Web SDK和适用于Analytics的AppMeasurement。 但是，支持跨不同页面的混合实施，例如支持在页面A上实施Platform Web SDK，以及支持在页面B上具有AppMeasurement的at.js。

在迁移时，您应该计划按照公司的流程测试和发布新代码，并在发布到生产环境之前使用开发、qa和暂存环境等。

>[!CAUTION]
>
>如果从具有一个库的页面重定向到另一个库的页面，则在逐页迁移中不支持重定向选件


接下来，查看[at.js与Platform Web SDK的详细比较](detailed-comparison.md)，以更好地了解技术差异，并确定需要额外关注的领域。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
