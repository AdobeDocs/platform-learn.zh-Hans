---
title: 发送参数 — 将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Experience PlatformWeb SDK将mbox、配置文件和实体参数发送到Adobe Target。
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---

# 使用Platform Web SDK将参数发送到Target

由于站点架构、业务要求和使用的功能，Target实施在各个网站之间有所不同。 大多数Target实施都包括传递上下文信息、受众和内容推荐的各种参数。

我们使用简单的产品详细信息页面和订单确认页面来演示在将参数传递到Target时扩展之间的差异。


| 示例at.js参数 | Platform Web SDK选项 | 注释 |
| --- | --- | --- |
| `at_property` | 不适用 | 属性令牌在[数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target)中配置，无法在`sendEvent`调用中设置。 |
| `pageName` | `xdm.web.webPageDetails.name` | 所有Target mbox参数都必须作为`xdm`对象的一部分进行传递，并且必须符合使用XDM ExperienceEvent类的架构。 Mbox参数不能作为`data`对象的一部分传递。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target配置文件参数都必须作为`data`对象的一部分进行传递，并以为前缀`profile.`，才能正确映射。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用于Target的类别亲和度功能的保留参数，必须作为`data`对象的一部分传递。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或<br> `xdm.productListItems[0].SKU` | 实体ID用于Target Recommendations行为计数器。 这些实体ID可以作为`data`对象的一部分传递，也可以自动从`xdm.productListItems`数组中的第一个项进行映射（如果您的实施使用该字段组）。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 实体类别ID可作为`data`对象的一部分传递。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自定义实体参数用于更新Recommendations产品目录。 这些自定义参数必须作为`data`对象的一部分进行传递。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用于Target基于购物车的推荐算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用于防止特定实体ID在推荐设计中返回。 |
| `mbox3rdPartyId` | 在`xdm.identityMap`对象中设置 | 用于跨设备和客户属性同步Target配置文件。 必须在数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html)的[Target配置中指定用于客户ID的命名空间。 |
| `orderId` | `xdm.commerce.order.purchaseID` | 用于标识Target转化跟踪的唯一订单。 |
| `orderTotal` | `xdm.commerce.order.priceTotal` | 用于跟踪Target转化和优化目标的订单总计。 |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>或<br> `xdm.productListItems[0-n].SKU` | 用于Target转化跟踪和推荐算法。 有关详细信息，请参阅下面的[实体参数](#entity-parameters)部分。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用于[自定义评分](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html)活动目标。 |

{style="table-layout:auto"}

## 自定义参数

必须将自定义mbox参数作为XDM或通过`sendEvent`命令使用数据对象进行传递。 请务必确保XDM架构包含Target实施所需的所有字段。


## 配置文件参数

必须传递目标配置文件参数……

## 实体参数

实体参数用于为Target Recommendations传递行为数据和补充目录信息。 at.js支持的所有[实体参数](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html)也受Platform Web SDK支持。 与配置文件参数类似，所有实体参数都应在Platform Web SDK `sendEvent`命令有效负载中的`data.__adobe.target`对象下传递。

特定项的实体参数必须以`entity.`为前缀，才能正确捕获数据。 不应为推荐算法保留的`cartIds`和`excludedIds`参数添加前缀，每个参数的值都必须包含以逗号分隔的实体ID列表。



## 购买参数

成功完成订单后，采购参数会在订单确认页面上传递，并用于Target转化和优化目标。 通过使用优化扩展的Platform Mobile SDK实施，这些参数和会自动从作为`commerce`字段组的一部分传递的XDM数据进行映射。


当`commerce`字段组的`purchases.value`设置为`1`时，购买信息将传递到Target。 订单ID和订单总计自动从`order`对象映射。 如果`productListItems`数组存在，则`SKU`值将用于`productPurchasedId`。


## 客户ID (mbox3rdPartyId)

Target允许使用单个客户ID跨设备和系统同步配置文件。



接下来，了解如何使用Platform Web SDK [跟踪Target转化事件](track-events.md)。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备从Target扩展迁移到Optimize扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
