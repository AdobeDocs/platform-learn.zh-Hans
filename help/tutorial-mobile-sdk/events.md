---
title: 活动
description: 了解如何在移动应用程序中收集事件数据。
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# 活动

了解如何跟踪移动应用程序中的事件。

>[!INFO]
>
> 2023年11月下旬，本教程将替换为使用新示例移动应用程序的新教程

Edge Network扩展提供了一个用于将Experience事件发送到Platform Edge Network的API。 体验事件是一个对象，其中包含符合XDM ExperienceEvent架构定义的数据。 更简单地说，它们捕获用户在您的移动应用程序中的操作。 Platform Edge Network收到数据后，可以将其转发到数据流中配置的应用程序和服务，如Adobe Analytics和Experience Platform。 了解关于 [体验事件](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) 在产品文档中。

## 先决条件

* 更新了包含所需SDK的PodFile。
* 在AppDelegate中注册的扩展。
* 已将MobileCore配置为使用开发AppId。
* 导入的SDK。
* 通过上述更改已成功构建和运行应用程序。

## 学习目标

在本课程中，您将执行以下操作：

* 了解如何基于架构构建XDM数据。
* 基于标准字段组发送XDM事件。
* 基于自定义字段组发送XDM事件。
* 发送XDM购买事件。
* 使用保障进行验证。

## 构建体验事件

Adobe Experience Platform Edge扩展可以将遵循之前定义的XDM架构的事件发送到Adobe Experience Platform Edge Network。

这个过程是这样的……

1. 识别您尝试跟踪的移动应用程序交互。

1. 检查您的架构并确定相应的事件。

1. 查看您的架构并确定应用于描述事件的任何其他字段。

1. 构造和填充数据对象。

1. 创建并发送事件。

1. 验证.

我们来看几个例子。

### 示例#1 — 标准字段组

请查看以下示例，而无需尝试在示例应用程序中实施它：

1. 在您的架构中，识别您尝试收集的事件，在本例中，我们跟踪的是产品查看。
   ![产品视图架构](assets/mobile-datacollection-prodView-schema.png)

1. 开始构建对象：

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
       "commerce": [
           "productViews": [
           "value": 1
           ]
       ]
   ]
   ```

   * eventType：描述发生的事件，使用 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) 如果可能。
   * commerce.productViews.value：提供事件的数字值。 如果它是一个布尔值(在Adobe Analytics中为“计数器”)，则该值将始终为1。 如果是数值或货币事件，该值可以大于1。

1. 在您的架构中，识别与事件关联的任何其他数据。 在此示例中，包括 `productListItems` 这是一组用于商业相关事件的标准字段：
   ![产品列表项架构](assets/mobile-datacollection-prodListItems-schema.png)
   * 请注意 `productListItems` 是一个数组，因此可以提供多个产品。

1. 展开xdmData对象以包含补充数据：

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
           "commerce": [
           "productViews": [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name":  productName,
               "SKU": sku,
               "priceTotal": priceString,
               "quantity": 1
           ]
       ]
   ]
   ```

1. 使用数据结构创建 `ExperienceEvent`：

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. 将事件和数据发送到Platform Edge Network：

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### 示例#2 — 自定义字段组

请查看以下示例，而无需尝试在示例应用程序中实施它：

1. 在您的架构中，识别您尝试收集的事件。 在此示例中，跟踪由应用程序操作事件和名称组成的“应用程序交互”。
   ![应用程序交互模式](assets/mobile-datacollection-appInteraction-schema.png)

1. 开始构建对象。

   >[!NOTE]
   >
   >  标准字段组始终以对象根开头。
   >
   >  自定义字段组始终以Experience Cloud组织特有的对象“_techmarketingdemos”开头（在本例中）。

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
                   ]
               ]
           ]
       ]
   ]
   ```

   或者……

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. 使用数据结构创建 `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. 将事件和数据发送到Platform Edge Network。

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### 向Luma应用程序添加屏幕视图跟踪

以上示例有望解释在构建XDM数据对象时的思维过程。 接下来，我们将在Luma应用程序中添加屏幕视图跟踪。

1. 导航到 `Home.swift`。
1. 将以下代码添加到 `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
               "appInformation": [
                   "appStateDetails": [
                       "screenType": "App",
                       "screenName": stateName,
                       "screenView": [
                           "value": 1
                       ]
                   ]
               ]
           ]
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. 对应用程序中的每个屏幕重复执行上述操作，正在更新 `stateName` 随你去。



### 验证

1. 查看 [设置说明](assurance.md) 并将模拟器或设备连接到Assurance。
1. 执行该操作并查找 `hitReceived` 来自的事件 `com.adobe.edge.konductor` 供应商。
1. 选择事件并在以下位置查看XDM数据： `messages` 对象。
   ![数据收集验证](assets/mobile-datacollection-validation.png)

### 示例#3 — 购买

在此示例中，假设用户成功进行了以下购买：

* 产品#1 — 瑜伽垫。
   * 49.99美元x1
   * SKU：5829
* 产品#2 — 水瓶。
   * 10.00美元x3
   * SKU： 9841
* 订单合计：79.99美元
* 唯一订单Id：298234720
* 付款类型：Visa信用卡
* 唯一付款交易记录ID：847361

#### 架构

以下是要使用的相关架构字段：

* eventType： &quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails（自定义）

>[!TIP]
>
>自定义字段组始终位于您的Experience Cloud组织标识符下。
>
>“_techmarketingdemos”被替换为您的组织的唯一值。

![购买模式](assets/mobile-datacollection-purchase-schema.png)


#### 代码

下面是如何在应用程序中构建和发送XDM对象的。

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
  "appInformation": [
    "appStateDetails": [
      "screenType": "App",
      "screenName": stateName,
      "screenView": [
        "value": 1
      ]
    ]
  ]
]
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>为清楚起见，所有值都进行了硬编码。 在现实世界中，这些值会动态填充。


### 在Luma应用程序中实施

您应该拥有所有工具，以便开始将数据收集添加到Luma示例应用程序。 以下是您可以遵循的假设性跟踪要求列表。

* 跟踪每个屏幕视图。
   * 架构字段： screenType、screenName、screenView
* 跟踪非商业操作。
   * 架构字段： appInteraction.name、appAction
* 商务操作：
   * 产品页面：产品查看次数
   * 添加到购物车： productListAdds
   * 从购物车中删除： productListRemovals
   * 开始结帐：结帐
   * 查看购物车： productListViews
   * 添加到愿望清单： saveForLaters
   * 采购：采购、订单

>[!TIP]
>
>查看 [完全实施的应用程序](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 以了解更多示例。

### 验证

1. 查看 [设置说明](assurance.md) 并将模拟器或设备连接到Assurance。

1. 执行该操作并查找 `hitReceived` 来自的事件 `com.adobe.edge.konductor` 供应商。

1. 选择事件并在以下位置查看XDM数据： `messages` 对象。
   ![数据收集验证](assets/mobile-datacollection-validation.png)

## 将事件发送到Analytics和Platform

现在您已收集事件并将它们发送到Platform Edge Network，将它们发送到中配置的应用程序和服务。 [数据流](create-datastream.md). 在后面的课程中，您会将此数据映射到 [Adobe Analytics](analytics.md) 和 [Adobe Experience Platform](platform.md).

下一步： **[WebViews](web-views.md)**

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)