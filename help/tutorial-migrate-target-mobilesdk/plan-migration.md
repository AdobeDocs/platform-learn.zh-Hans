---
title: 规划 — 在移动应用程序中将Target从Target扩展迁移到优化扩展
description: 了解如何从at.js 2.x到Adobe Experience Platform Web SDK的Adobe Target实施规划。
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 规划Target到Optimize扩展的迁移

在移动应用程序中将Target从Target扩展升级到Optimize扩展之前，您应该评估当前的实施。

## 评估当前的Target扩展实施

成功迁移的第一步是深入了解您当前的Target扩展实施。 有些特性、函数和自定义代码可能需要更新。 评估时请考虑以下事项：

### 支持哪些功能？

<!--Platform Web SDK is under continuous active development and features and enhancements are added regularly. As you evaluate your current at.js implementation, refer to the [supported use cases](https://github.com/orgs/adobe/projects/18/views/1) page for the latest information.-->

### 您现在使用哪些功能？

<!--Platform Web SDK is a new library that consolidates all Adobe solutions for the websites into a single SDK. This enables tighter integration and enables new capabilities unique to Adobe Experience Platform. However, this also means at.js functions are not backwards compatible with Platform Web SDK. As you evaluate your current implementation, make note of the following:

- at.js functions such as `getOffer()` and `applyOffer()`
- Modifications to Target's global settings
- Integration with Adobe Analytics
- Use of a flicker mitigation script
- Use of response tokens
- Use of mbox, profile, and entity parameters
- Custom code unique to your implementation-->

### 您将采用哪种迁移方法？

<!--Once you have revisited your at.js implementation, you need to determine a migration approach. There are two options:

- Migrate all Adobe applications at once across the entire site
- Migrate on a page-by-page basis

Because Platform Web SDK combines and enables multiple Adobe applications, you must coordinate the Target migration of other Adobe applications like Analytics and Audience Manager. All Adobe libraries on a given page should be migrated at the same time. A mixed implementation of Platform Web SDK for Target and AppMeasurement for Analytics on a particular page is not supported. However, a mixed implementation across different pages is supported, for example Platform Web SDK on page A, and at.js with AppMeasurement on page B.

As you migrate, you should plan on following your company's process for testing and releasing new code and use things like development, qa, and staging environments before you release to production.-->

<!--
>[!CAUTION]
>
>Redirect offers are not supported in page-by-page migrations if redirecting from a page with one library to a page with a different library
-->


接下来，查看Target扩展与Optimize扩展](detailed-comparison.md)的详细[比较，以更好地了解技术差异，并确定需要额外关注的领域。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备从Target扩展迁移到Optimize扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
