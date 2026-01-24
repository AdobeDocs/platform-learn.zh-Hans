---
title: 跟踪转化事件 — 将移动设备应用程序中的Adobe Target实施迁移到Offer Decisioning和Target扩展
description: 了解如何使用Adobe Target和Offer Decisioning Mobile扩展跟踪Target转化事件
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 使用Decisioning移动扩展跟踪Target转化事件

大多数Target活动的目标是让用户在您的应用程序中执行有价值的操作，例如购买、注册、点击等等。 Target实施通常使用自定义转化事件来跟踪这些操作，通常包含有关转化的其他详细信息。 可以使用与Target SDK类似的“优化SDK”来跟踪Target的转化事件。 需要调用特定API来跟踪转化事件，如下表所示：

| 活动目标 | 目标扩展 | Offer Decisioning和Target扩展 |
|---|---|---|
| 跟踪mbox位置（范围）的视图转换事件 | 查看mbox位置时调用[displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API | 查看mbox位置的选件时，调用[displayed](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} API。 这会向Experience Edge网络发送一个事件类型为decisioning.propositionDisplay的事件。 **这对于增加Target活动中的访客数至关重要，并且必须在同时提供常规和默认Target选件时完成。** |
| 跟踪mbox位置（范围）的点击转化事件 | 单击mbox位置时，在中调用[clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API | 单击mbox位置的选件时，调用[taped](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} API。 这会向Experience Edge网络发送一个事件类型为decisioning.propositionInteract的事件。 |
| 跟踪可能还包括其他数据的自定义转化事件，如Target配置文件参数和订单详细信息 | 在[displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank}和[clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API提供的TargetParameters字段中传递其他数据 | 使用选件中为mbox位置提供的公共方法[generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank}和[generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} API生成用于查看和单击的XDM格式数据。 然后调用Edge SDK [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} API以将此跟踪XDM数据以及任何其他XDM和自由格式数据发送到Experience Edge网络。 |


接下来，了解如何[更新受众和配置文件脚本](update-audiences.md)以确保与Offer Decisioning和Target扩展兼容。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Offer Decisioning和Target扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=zh-Hans#M463)中发帖让我们知道。
