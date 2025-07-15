---
title: 发送参数 — 将移动应用程序中的Adobe Target实施迁移到Offer Decisioning和Target扩展
description: 了解如何使用Experience Platform Web SDK将mbox、配置文件和实体参数发送到Adobe Target。
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 使用Offer Decisioning and Target扩展将参数发送到Target

由于应用程序架构、业务要求和使用的功能，Target实施在移动应用程序之间有所不同。 大多数Target实施都包括传递上下文信息、受众和内容推荐的各种参数。

对于Target扩展，使用`TargetParameters`函数传递所有Target参数。

使用Offer Decisioning和Target扩展：

* 可在XDM对象中传递用于多个Adobe应用程序的参数
* 可以在`data.__adobe.target`对象中传递仅用于Target的参数


>[!IMPORTANT]
>
> 使用Decisioning扩展时，在请求中发送的参数将应用于请求中的所有范围。 如果需要为不同的范围设置不同的参数，则必须发出其他请求。

## 自定义参数

自定义mbox参数是将数据传递到Target的最基本方式，可以在`xdm`或`data.__adobe.target`对象中传递。

## 轮廓参数

配置文件参数会在用户的Target配置文件中存储较长时间的数据，并且必须在`data.__adobe.target`对象中传递。

## 实体参数

[实体参数](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/entity-attributes)用于传递Target Recommendations的行为数据和补充目录信息。 与配置文件参数类似，大多数实体参数应在`data.__adobe.target`对象下传递。 唯一的例外是`xdm.productListItems`数组存在，然后使用第一个`SKU`值作为`entity.id`。

特定项的实体参数必须以`entity.`为前缀，才能正确捕获数据。 不应为推荐算法保留的`cartIds`和`excludedIds`参数添加前缀，每个参数的值都必须包含以逗号分隔的实体ID列表。

## 购买参数

成功完成订单后，采购参数会在订单确认页面上传递，并用于Target转化和优化目标。 通过使用Offer Decisioning和Target扩展的Platform Mobile SDK实施，这些参数和会自动从作为`commerce`字段组的一部分传递的XDM数据进行映射。

当`commerce`字段组的`purchases.value`设置为`1`时，购买信息将传递到Target。 订单ID和订单总计自动从`order`对象映射。 如果`productListItems`数组存在，则`SKU`值将用于`productPurchasedId`。

如果未在`commerce`对象中传递`xdm`字段，则可以使用`data.__adobe.target.orderId`、`data.__adobe.target.orderTotal`和`data.__adobe.target.productPurchasedId`字段将订单详细信息传递给Target。

## 客户ID (mbox3rdPartyId)

Target允许使用单个客户ID跨设备和系统同步配置文件。 此客户ID应在XDM对象的`identityMap`字段中传递，并映射到数据流中的目标第三方ID字段。

## 表

| 示例at.js参数 | Platform Web SDK选项 | 注释 |
| --- | --- | --- |
| `at_property` | 不适用 | 属性令牌在[数据流](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure#target)中配置，无法在`sendEvent`调用中设置。 |
| `pageName` | `xdm.web.webPageDetails.name`或<br> `data.__adobe.target.pageName` | 目标mbox参数可以作为`xdm`对象的一部分或`data.__adobe.target`对象的一部分进行传递。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target配置文件参数都必须作为`data`对象的一部分进行传递，并以为前缀`profile.`，才能正确映射。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用于Target的类别亲和度功能的保留参数，必须作为`data`对象的一部分传递。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或<br> `xdm.productListItems[0].SKU` | 实体ID用于Target Recommendations行为计数器。 这些实体ID可以作为`data`对象的一部分传递，也可以自动从`xdm.productListItems`数组中的第一个项进行映射（如果您的实施使用该字段组）。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 实体类别ID可作为`data`对象的一部分传递。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自定义实体参数用于更新推荐产品目录。 这些自定义参数必须作为`data`对象的一部分进行传递。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用于Target基于购物车的推荐算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用于防止特定实体ID在推荐设计中返回。 |
| `mbox3rdPartyId` | 在`xdm.identityMap`对象中设置 | 用于跨设备和客户属性同步Target配置文件。 必须在数据流[的](https://experienceleague.adobe.com/en/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid)Target配置中指定用于客户ID的命名空间。 |
| `orderId` | `xdm.commerce.order.purchaseID`<br> （当`commerce.purchases.value`设置为`1`时）<br>或<br> `data.__adobe.target.orderId` | 用于标识Target转化跟踪的唯一订单。 |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> （当`commerce.purchases.value`设置为`1`时）<br>或<br> `data.__adobe.target.orderTotal` | 用于跟踪Target转化和优化目标的订单总计。 |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> （当`commerce.purchases.value`设置为`1`时） <br>OR<br> `data.__adobe.target.productPurchasedId` | 用于Target转化跟踪和推荐算法。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用于[自定义评分](https://experienceleague.adobe.com/en/docs/target/using/activities/success-metrics/capture-score)活动目标。 |

{style="table-layout:auto"}


## 传递参数的示例

我们通过一个简单的示例来演示在将参数传递到Target时扩展之间的差异。

### Android

>[!BEGINTABS]

>[!TAB 优化SDK]

```Java
final Map<String, Object> data = new HashMap<>();
final Map<String, String> targetParameters = new HashMap<>();
 
// Mbox parameters
targetParameters.put("status", "platinum");
 
// Profile parameters - prefix with profile.
targetParameters.put("profile.gender", "male");
 
// Product parameters
targetParameters.put("productId", "pId1");
targetParameters.put("categoryId", "cId1");
 
// Order parameters
targetParameters.put("orderId", "id1");
targetParameters.put("orderTotal", "1.0");
targetParameters.put("purchasedProductIds", "ppId1");
 
data.put("__adobe", new HashMap<String, Object>() {
  {
    put("target", targetParameters);
  }
});
 
// Target location (or mbox)
final DecisionScope decisionScope = DecisionScope("myTargetLocation")
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope);
 
Optimize.updatePropositions(decisionScopes, null, data);
```

>[!TAB 定位SDK]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB 优化SDK]

```Swift
var data: [String: Any] = [:]
var targetParameters: [String: String] = [:]
 
// Mbox parameters
targetParameters["status"] = "platinum"
 
// Profile parameters - prefix with profile.
targetParameters["profile.gender"] = "make"
 
// Product parameters
targetParameters["productId"] = "pId1"
targetParameters["categoryId"] = "cId1"
 
// Add order parameters
targetParameters["orderId"] = "id1"
targetParameters["orderTotal"] = "1.0"
targetParameters["purchasedProductIds"] = "ppId1"
 
data["__adobe"] = [
  "target": targetParameters
]
 
// Target location (or mbox)
let decisionScope = DecisionScope(name: "myTargetLocation")
Optimize.updatePropositions(for: [decisionScope] withXdm: nil andData: data)
```

>[!TAB 定位SDK]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






接下来，了解如何使用Platform Web SDK [跟踪Target转化事件](track-events.md)。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Offer Decisioning和Target扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625)中发帖让我们知道。
