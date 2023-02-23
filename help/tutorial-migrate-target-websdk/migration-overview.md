---
title: 迁移概述 |将Target从at.js 2.x迁移到Web SDK
description: 了解at.js和Platform Web SDK之间的主要区别以及如何规划迁移工作。=
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# 将at.js迁移到平台Web SDK概述

从at.js迁移到Platform Web SDK的工作量取决于您当前实施的复杂程度以及使用的产品功能。

无论您的实施多么简单或复杂，在迁移之前必须充分了解您的当前状态。 本指南可帮助您划分当前实施的组件，并制定一个可管理的计划来迁移每个组件。

迁移过程涉及以下关键步骤：

1. 评估您当前的实施并确定迁移方法
1. 设置初始组件以连接到Adobe Experience Platform Edge Network
1. 更新基础实施，以使用平台Web SDK替换at.js
1. 增强适用于您的特定用例的平台Web SDK实施。 这可能涉及传递其他参数、考虑单页应用程序(SPA)视图更改、使用响应令牌等。
1. 在Target界面中更新对象，如配置文件脚本、活动和受众定义
1. 在生产环境中进行切换之前验证最终实施

## at.js与Platform Web SDK之间的主要区别

在开始迁移过程之前，请务必了解at.js与平台Web SDK之间的差异。

### 运营差异

Platform Web SDK将多个Adobe应用程序的功能整合到单个库中。 这种统一的方法意味着您应考虑跨团队的责任和流程，以确保实施的正常进行。

|  | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 所有权 | at.js库与其他应用程序库无关。 这些不同库的自定义设置和所有权可能与组织中的不同团队保持一致。 | 平台Web SDK库和传递的数据可以统一到所有Adobe应用程序。 Platform Web SDK实施的所有权应代表所有下游应用程序的利益相关方。 |
| 维护 | 不同的团队可能会针对每个Adobe应用程序（如Target和Analytics）进行实施增强。 | 理想情况下，应由一个团队负责影响Platform Web SDK实施的增强功能。 |
| 过程 | 对Target实施所做的更改可能会遵循一个与Analytics等其他应用程序相比具有不同终止时间或QA要求的过程。 | 对Platform Web SDK实施所做的更改应考虑所有下游应用程序，并且应相应地调整QA和发布过程。 |
| 协作 | 特定于Target的数据可以直接在Target调用中传递。 根据实施，可能会有其他的Target调用。 这对Adobe Analytics数据没有直接影响，与分析团队的协调也没有那么重要。 | 在Platform Web SDK调用中传递的数据可以转发到Target和Analytics。 需要各小组之间进行协调，以确保更改不会对特定应用程序产生不利影响。 |

### 技术差异

平台Web SDK不是Target at.js库的演变。 它是一种新的统一方法，用于为Web渠道实施所有Adobe应用程序。 需要注意的技术差异有多种。

|  | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 库功能 | at.js提供的Target功能。 与由Visitor.js和AppMeasurement.js提供的其他应用程序集成 | 由单个平台Web SDK库提供的所有Adobe应用程序的功能：alloy.js |
| 性能 | at.js是必须加载的多个库之一，才能在应用程序之间进行正确集成。 这会导致负载时间小于最佳值。 | Platform Web SDK是一个轻量级的库，它消除了对多个特定于应用程序的库的需求，从而提高了页面加载性能。 |
| 请求 | 对每个Adobe应用程序分别进行调用。 Target调用基本上独立于其他网络调用。 | 对所有Adobe应用程序进行一次调用。 对这些调用中传递的数据所做的更改可能会影响多个下游应用程序。 |
| 加载顺序 | 与其他Adobe应用程序的正确集成需要特定的库加载顺序和网络调用。 | 正确的集成不依赖于拼合来自不同应用程序特定网络调用的数据，因此无需考虑加载顺序。 |
| 边缘网络 | 使用Adobe Experience Cloud边缘网络(tt.omtrdc.net)，可选择使用特定于Target的CNAME。 | 使用Adobe Experience Platform Edge Network(edge.adobedc.net)，可选择使用单个CNAME。 |
| 基本术语 | at.js命名： <br> - `mbox` <br> - `pageLoad` 事件（全局mbox） <br> - `offer` | 平台Web SDK等效项： <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### 视频概述

以下视频概述了Adobe Experience Platform Web SDK和Adobe Experience Platform Edge Network。

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

现在，您已了解at.js与Platform Web SDK之间的高级别差异，接下来可以 [规划迁移](plan-migration.md).

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).