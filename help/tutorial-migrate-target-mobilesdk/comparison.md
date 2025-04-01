---
title: Target扩展与Decisioning扩展的比较
description: 了解Target扩展与Decisioning扩展之间的差异，包括功能、功能、设置和数据流。
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 24effdb0905c6fd146a80031e0a39eed9672306d
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# Target扩展与Decisioning扩展的比较

Adobe Journey Optimizer - Decisioning扩展不同于适用于移动应用程序的Adobe Target扩展。 下表可供参考，以帮助您评估在迁移过程中可能需要重点实施的各个方面。

在查看以下信息并评估您当前的技术性Target扩展实施情况后，您应该能够了解以下内容：

- Adobe Journey Optimizer支持哪些Target功能 — Decisioning
- 哪些Adobe Target扩展函数具有Adobe Journey Optimizer — 决策等效项
- 如何将Target设置应用于Adobe Journey Optimizer - Decisioning
- 使用Adobe Journey Optimizer - Decisioning扩展时的数据流动方式

## 操作差异

| | 目标扩展 | Decisioning扩展 |
|---|---|---|
| 进程 | 对Target实施所做的更改可能会遵循与其他应用程序（如Analytics）相比节奏或QA要求不同的流程。 | 对Decisioning扩展实施的更改应考虑所有下游应用程序，并应相应地调整QA和发布流程。 |
| 协作 | 可以在Target调用中直接传递特定于Target的数据。 如果Target报表源是Adobe Analytics (A4T)，则当在Target扩展中调用适当的跟踪方法来进行Target内容显示和交互时，特定于Target的数据也可以传递到Adobe Analytics。 | 如果Target报表源是Adobe Analytics (A4T)，并且在数据流中启用了Adobe Analytics，并且在显示Target内容并与之交互时，可以将在Decisioning扩展调用中传递的数据转发到Target和Analytics。 |

## 基本差异

| | 目标扩展 | Decisioning扩展 |
|---|---|---|
| 依赖关系 | 仅依赖于Mobile Core SDK | 依赖于Mobile Core和Edge Network SDK |
| 库功能 | 仅支持从Adobe Target获取内容 | 支持从Adobe Target和Offer Decisioning获取内容 |
| 请求 | Target调用基本上独立于其他网络调用 | Target网络调用与其他基于Edge的解决方案(如Edge SDK中的消息传送)的网络调用一起排入队列，并连续执行。 |
| Edge Network | 使用Target服务器值或带有客户端代码(clientcode.tt.omtrdc.net)的Adobe Experience Cloud Edge Network，两者在数据收集UI的[Target配置](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)中指定 | 在数据收集UI中使用Adobe Experience Platform [Edge Network配置](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)中指定的Edge网络域。 |
| 基本术语 | mbox， TargetParameters | DecisionScope， Map (Android)/dictionary (iOS) for Target参数 |
| 默认内容 | 允许在TargetRequest中传递客户端默认内容，如果网络调用失败或导致错误，将返回此内容。 | 不允许传递客户端默认内容。 如果网络调用失败或导致错误，则不返回任何内容。 |
| Target参数 | 允许为每个请求传递全局TargetParameters，并为每个mbox传递不同的TargetParameters | 仅允许每个请求传递全局TargetParameters |



## 功能比较

| 功能 | 目标扩展 | Decisioning扩展(通过Edge的Target) |
|---|---|---|
| 预取模式 | 支持 | 支持 |
| 执行模式 | 支持 | 不支持 |
| 自定义参数 | 支持 | 支持* |
| 轮廓参数 | 支持 | 支持* |
| 实体参数 | 支持 | 支持* |
| 目标受众 | 支持 | 支持 |
| Real-Time CDP受众 | 不支持 | 支持 |
| Real-Time CDP属性 | 不支持 | 支持 |
| 生命周期量度 | 支持 | 通过数据收集规则支持 |
| thirdPartyId (mbox3rdPartyId) | 支持 | 通过数据流中的身份映射和Target第三方ID命名空间支持 |
| 通知（显示、点击） | 支持 | 支持 |
| 响应令牌 | 支持 | 支持 |
| 移动设备预览（QA模式） | 支持 | Assurance有限支持 |

>[!IMPORTANT]
>
> \*在请求中发送的参数适用于请求中的所有范围。 如果需要为不同的范围设置不同的参数，则必须发出其他请求。



## 值得注意的标注

>[!NOTE]
>
>即使在将应用程序代码迁移到Decisioning扩展后，仍应保持Target扩展标记配置和设置不变。 这有助于确保尚未将应用程序更新到新版本的客户能够继续使用Target。
>
>如果您使用Analytics for Target集成(A4T)，则在将Target实施迁移到Decisioning扩展时，请务必同时使用Edge Bridge扩展迁移Analytics实施。





>[!IMPORTANT]
>
> 即使将应用程序代码迁移到Decisioning扩展，Target扩展设置仍保持不变。 这有助于确保Target继续适用于尚未更新应用程序的用户。

## Decisioning扩展系统图

下图应该可以帮助您了解使用Adobe Journey Optimizer - Decisioning扩展的数据流。

使用客户端Mobile SDK的![Adobe Target Edge Decisioning](assets/diagram.png)


>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
