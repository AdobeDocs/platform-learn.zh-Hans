---
title: 事件
description: 了解如何在移动设备应用程序中收集事件数据。
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# 事件

了解如何跟踪移动设备应用程序中的事件。

边缘网络扩展提供了一个API，用于将Experience Events发送到Platform Edge Network。 体验事件是一个对象，其中包含符合XDM ExperienceEvent架构定义的数据。 更简单地说，它们会捕获用户在您的移动设备应用程序中的操作。 Platform Edge Network收到数据后，即可将其转发到数据流中配置的应用程序和服务，如Adobe Analytics和Experience Platform。 进一步了解 [体验事件](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk) （在产品文档中）。

## 先决条件

* 已使用所需的SDK更新PodFile。
* AppDelegate中已注册的扩展。
* 已配置MobileCore以使用您的开发AppId。
* 导入的SDK。
* 已成功构建并运行包含上述更改的应用程序。

## 学习目标

在本课程中，您将：

* 了解如何根据模式构建XDM数据。
* 根据标准字段组发送XDM事件。
* 根据自定义字段组发送XDM事件。
* 发送XDM购买事件。
* 通过保证进行验证。

## 构建体验事件

Adobe Experience Platform Edge扩展可以将遵循先前定义的XDM架构的事件发送到Adobe Experience Platform Edge Network。

这个过程是这样……

1. 识别您尝试跟踪的移动设备应用程序交互。

1. 查看您的架构并确定相应的事件。

1. 查看您的架构，并确定应用于描述该事件的任何其他字段。

1. 构建和填充数据对象。

1. 创建和发送事件。

1. 验证.

让我们看几个示例。

### 示例#1 — 标准字段组

查看以下示例，但未尝试在示例应用程序中实施它：

1. 在您的架构中，识别您尝试收集的事件，在本例中，我们将跟踪产品查看。
   ![产品查看模式](assets/mobile-datacollection-prodView-schema.png)

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

   * eventType:描述发生的事件，使用 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) （如果可能）。
   * commerce.productViews.value:提供事件的数值。 如果它是布尔值(或Adobe Analytics中的“计数器”)，则值将始终为1。 如果是数字或货币事件，则值可能大于1。

1. 在您的架构中，识别与事件关联的任何其他数据。 在本例中，包括 `productListItems` 这是与商务相关事件一起使用的标准字段集：
   ![产品列表项目架构](assets/mobile-datacollection-prodListItems-schema.png)
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

1. 使用数据结构创建 `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. 将事件和数据发送到Platform Edge Network:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### 示例#2 — 自定义字段组

查看以下示例，但未尝试在示例应用程序中实施它：

1. 在您的架构中，识别您尝试收集的事件。 在此示例中，跟踪“应用程序交互”，该交互包含应用程序操作事件和名称。
   ![应用程序交互模式](assets/mobile-datacollection-appInteraction-schema.png)

1. 开始构建对象。

   >[!NOTE]
   >
   >  标准字段组始终从对象根中开始。
   >
   >  自定义字段组始终在Experience Cloud组织“_techmarketingdemos”的独特对象下开始。

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

上述示例有望解释构建XDM数据对象时的思路。 接下来，我们将在Luma应用程序中添加屏幕视图跟踪。

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

1. 对应用程序中的每个屏幕重复执行上述步骤，并更新 `stateName` 随你去。



### 验证

1. 查看 [设置说明](assurance.md) 部分，并将您的模拟器或设备连接到“保证”。
1. 执行操作并查找 `hitReceived` 事件 `com.adobe.edge.konductor` 供应商。
1. 选择事件并在 `messages` 对象。
   ![数据收集验证](assets/mobile-datacollection-validation.png)

### 示例#3 — 购买

在此示例中，假设用户成功购买了以下产品：

* 产品#1 — 瑜伽垫。
   * 49.99美元x1
   * SKU:5829
* 产品#2 — 水瓶。
   * $10.00 x3
   * SKU:9841
* 订单合计：US$79.99
* 唯一订单Id:298234720
* 付款类型：签证信用卡
* 唯一付款交易Id:847361

#### 架构

以下是要使用的相关架构字段：

* eventType:&quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails（自定义）

>[!TIP]
>
>自定义字段组始终放在Experience Cloud组织标识符下。
>
>“_techmarketingdemos”已替换为您组织的唯一值。

![购买模式](assets/mobile-datacollection-purchase-schema.png)


#### 代码

以下是如何在应用程序中构建和发送XDM对象。

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
>为清楚起见，所有值都进行了硬编码。 在现实中，这些值将被动态填充。


### 在Luma应用程序中实施

您应该拥有所有工具来开始向Luma示例应用程序添加数据收集。 以下是您可以遵循的假设跟踪要求列表。

* 跟踪每个屏幕视图。
   * 架构字段：screenType， screenName， screenView
* 跟踪非商务操作。
   * 架构字段：appInteraction.name， appAction
* 商务操作：
   * 产品页面：productViews
   * 添加到购物车：productListAdds
   * 从购物车中删除：productListRemuves
   * 开始结帐：结账
   * 查看购物车：productListViews
   * 添加到愿望清单：saveForLaters
   * 购买：购买、订购

>[!TIP]
>
>查看 [完全实施的应用程序](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) ，以了解更多示例。

### 验证

1. 查看 [设置说明](assurance.md) 部分，并将您的模拟器或设备连接到“保证”。

1. 执行操作并查找 `hitReceived` 事件 `com.adobe.edge.konductor` 供应商。

1. 选择事件并在 `messages` 对象。
   ![数据收集验证](assets/mobile-datacollection-validation.png)

## 将事件发送到Analytics和Platform

现在，您已收集事件并将其发送到Platform Edge Network，接下来，这些事件将被发送到您在 [数据流](create-datastream.md). 在以后的课程中，您会将此数据映射到 [Adobe Analytics](analytics.md) 和 [Adobe Experience Platform](platform.md).

下一个： **[WebViews](web-views.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)