---
title: 规划迁移 — 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解at.js与Platform Web SDK之间的主要区别，以及如何规划您的迁移工作。
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# 规划迁移

从Target扩展迁移到Decisioning扩展的工作量级别取决于当前实施的复杂性和使用的产品功能。

无论您的实施是多么简单或复杂，在迁移之前充分了解您的当前状态都非常重要。 本指南可帮助您划分当前实施的组件，并制定可管理的计划来迁移每个组件。

迁移过程涉及以下关键步骤：

1. 评估您当前的实施并确定迁移方法
1. 设置初始组件以连接到Adobe Experience PlatformEdge Network
1. 更新基础实施以替换Target扩展和Decisioning扩展
1. 针对您的特定用例，增强优化SDK实施。 这可能涉及传递其他参数、使用响应令牌等。
1. 更新Target界面中的对象，例如配置文件脚本、活动和受众定义
1. 在生产环境中进行切换之前，请验证最终实施

## Target扩展和Decisioning扩展之间的主要区别

在开始迁移过程之前，请务必了解Target扩展和Decisioning扩展之间的差异。

### 操作差异

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 进程 | 对Target实施所做的更改可能会遵循与其他应用程序（如Analytics）相比节奏或QA要求不同的流程。 | 对Decisioning扩展实施的更改应考虑所有下游应用程序，并应相应地调整QA和发布流程。 |
| 协作 | 可以在Target调用中直接传递特定于Target的数据。 如果Target报表源是Adobe Analytics，则在为Target内容显示和交互调用Target扩展中的相应跟踪方法时，特定于Target的数据也可以传递到Adobe Analytics。 | 如果Target报表源是Adobe Analytics，并且在数据流中启用了Adobe Analytics，并且显示Target内容并与之交互时，调用了Decisioning扩展中的相应跟踪方法，则在Decisioning扩展调用中传递的数据可以转发到Target和Analytics。 |

### 技术差异

| | 目标扩展 | Decisioning扩展 |
|---|---|---|
| 依赖关系 | 仅依赖于Mobile Core SDK | 依赖于Mobile Core和Edge NetworkSDK |
| 库功能 | 仅支持从Adobe Target获取内容 | 支持从Adobe Target和Offer decisioning获取内容 |
| 请求 | Target调用基本上独立于其他网络调用 | Target网络调用与其他基于Edge的解决方案(如Edge SDK中的消息传送)的网络调用一起排入队列，并连续执行。 |
| Edge Network | 使用在数据收集UI中的[Target配置](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)中指定的Target服务器值或带有客户端代码(clientcode.tt.omtrdc.net)的Adobe Experience CloudEdge Network | 在数据收集UI中使用Adobe Experience Platform [Edge Network配置](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)中指定的Edge网络域。 |
| 基本术语 | mbox， TargetParameters | 目标参数的DecisionScope、映射(Android)/词典(iOS) |
| 默认内容 | 允许在TargetRequest中传递客户端默认内容，如果网络调用失败或导致错误，将返回此内容。 | 不允许传递客户端默认内容。 如果网络调用失败或导致错误，则不返回任何内容。 |
| Target参数 | 允许为每个请求传递全局TargetParameters，并为每个mbox传递不同的TargetParameters | 仅允许每个请求传递全局TargetParameters |

接下来，查看Target扩展与Decisioning扩展的[详细比较](detailed-comparison.md)，以更好地了解技术差异，并确定需要额外关注的领域。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
