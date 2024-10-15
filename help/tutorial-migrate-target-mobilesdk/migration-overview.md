---
title: 迁移概述 — 将Target从at.js 2.x迁移到Web SDK
description: 了解at.js与Platform Web SDK之间的主要差异以及如何规划迁移工作。
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---

# Target at.js到Platform Web SDK迁移概述

从at.js迁移到Platform Web SDK所需的工作量级别取决于您当前实施的复杂性和使用的产品功能。

无论您的实施是多么简单或复杂，在迁移之前充分了解您的当前状态都非常重要。 本指南可帮助您划分当前实施的组件，并制定可管理的计划来迁移每个组件。

迁移过程涉及以下关键步骤：

1. 评估您当前的实施并确定迁移方法
1. 设置初始组件以连接到Adobe Experience PlatformEdge Network
1. 更新了基础实施，将at.js替换为Platform Web SDK
1. 针对特定用例增强Platform Web SDK实施。 这可能涉及传递其他参数、对单页应用程序(SPA)视图更改进行说明、使用响应令牌等。
1. 更新Target界面中的对象，例如配置文件脚本、活动和受众定义
1. 在生产环境中进行切换之前，请验证最终实施

## at.js与Platform Web SDK之间的主要区别

在开始迁移过程之前，请务必了解at.js与Platform Web SDK之间的差异。

### 操作差异

Platform Web SDK将多个Adobe应用程序的功能整合到一个库中。 这种统一的方法意味着您应当考虑跨团队的责任和流程，以确保健康的实施。

| | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 所有权 | at.js库独立于其他应用程序库。 这些不同库的自定义项和所有权可能会与组织中不同的团队保持一致。 | Platform Web SDK库和传递的数据对于所有Adobe应用程序都是统一的。 Platform Web SDK实施的所有权应代表所有下游应用程序的利益相关者。 |
| 维护 | 各个团队可能分别负责每个Adobe应用程序（如Target和Analytics）的实施增强功能。 | 理想情况下，应由一个团队负责实施影响Platform Web SDK实施的增强功能。 |
| 进程 | 对Target实施所做的更改可能会遵循与其他应用程序（如Analytics）相比节奏或QA要求不同的流程。 | 对Platform Web SDK实施所做的更改应考虑所有下游应用程序，并应相应地调整QA和发布流程。 |
| 协作 | 可以在Target调用中直接传递特定于Target的数据。 根据实施，可能会有其他Target调用。 这对Adobe Analytics数据没有直接影响，而且与Analytics团队的协调也没有那么重要。 | 在Platform Web SDK调用中传递的数据可以转发到Target和Analytics。 各团队之间需要进行协调，以确保更改不会对特定应用程序产生负面影响。 |

### 技术差异

Platform Web SDK不是Target at.js库的演变。 这是一种新的统一方法，用于为Web渠道实施所有Adobe应用程序。 您应当了解一些技术差异。

| | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 库功能 | at.js提供的Target功能。 与Visitor.js和AppMeasurement.js提供的其他应用程序集成 | 单个Platform Web SDK库提供的所有Adobe应用程序的功能：alloy.js |
| 绩效 | at.js是必须加载的多个库之一，才能跨应用程序进行正确集成。 这会导致加载时间少于最佳加载时间。 | Platform Web SDK是一个轻量级库，消除了对多个特定于应用程序的库的需求，从而提高页面加载性能。 |
| 请求 | 为每个Adobe应用程序分别调用。 Target调用基本上独立于其他网络调用。 | 针对所有Adobe应用程序的一次调用。 对这些调用中传递的数据所做的更改可能会影响多个下游应用程序。 |
| 加载顺序 | 要与其他Adobe应用程序正确集成，需要库和网络调用的特定加载顺序。 | 正确的集成不依赖于拼接来自不同应用程序特定网络调用的数据，因此无需考虑加载顺序。 |
| Edge Network | 使用Adobe Experience CloudEdge Network(tt.omtrdc.net)，可以选择使用特定于Target的CNAME。 | 使用Adobe Experience PlatformEdge Network(edge.adobedc.net)，可以选择使用单个CNAME。 |
| 基本术语 | at.js命名： <br> - `mbox` <br> - `pageLoad`事件（全局mbox） <br> - `offer` | Platform Web SDK等效项： <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### 视频概述

以下视频概述了Adobe Experience Platform Web SDK和Adobe Experience PlatformEdge Network。


现在您已了解at.js与Platform Web SDK之间的高级差异，您可以[规划迁移](plan-migration.md)。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备从Target扩展迁移到Optimize扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
