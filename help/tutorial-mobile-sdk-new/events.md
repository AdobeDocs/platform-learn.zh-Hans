---
title: 活动
description: 了解如何在移动应用程序中收集事件数据。
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# 活动

了解如何跟踪移动应用程序中的事件。

Edge Network扩展提供了一个用于将Experience事件发送到Platform Edge Network的API。 体验事件是一个对象，其中包含符合XDM ExperienceEvent架构定义的数据。 更简单地说，它们捕获用户在您的移动应用程序中的操作。 Platform Edge Network收到数据后，可以将其转发到数据流中配置的应用程序和服务，如Adobe Analytics和Experience Platform。 了解关于 [体验事件](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) 在产品文档中。

## 先决条件

* Xcode项目中的所有包依赖项均已准备就绪。
* 在AppDelegate中注册的扩展。
* 已将MobileCore配置为使用开发appId。
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


### 标准字段组

对于标准字段组，此过程如下所示：

* 在您的架构中，识别您尝试收集的事件。 在此示例中，您跟踪的是商业体验事件，例如产品视图(**[!UICONTROL 产品视图]**)事件。

  ![产品视图架构](assets/datacollection-prodView-schema.png)

* 要在应用程序中构建包含体验事件数据的对象，您可以使用以下代码：

  ```swift {highlight="2-8"}
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`：描述发生的事件，使用 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) 如果可能。
   * `commerce.productViews.id`：表示产品SKU的字符串值
   * `commerce.productViews.value`：提供事件的数字值。 如果它是一个布尔值(在Adobe Analytics中为“计数器”)，则该值始终设置为1。 如果是数值或货币事件，该值可以大于1。

* 在您的架构中，标识与商业产品查看事件关联的任何其他数据。 在此示例中，包括 `productListItems` 这是用于任何商业相关事件的标准字段集：

  ![产品列表项架构](assets/datacollection-prodListItems-schema.png)
   * 请注意 `productListItems` 是一个数组，因此可以提供多个产品。

* 要添加此数据，请展开 `xdmData` 要包含补充数据的对象：

```swift {highlight="9-16"}
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* 然后，使用数据结构创建 `ExperienceEvent`：

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* 并使用sendEvent API将事件和数据发送到Platform Edge Network：

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

现在，让我们在您的Xcode项目中实际实施此代码。
您的应用程序中确实有不同的商业产品相关操作（查看、添加到购物车、保存以供稍后使用、购买），并且您希望根据用户执行的这些操作发送事件。

1. 要构建发送体验事件，请转到 `MobileSDK`，并将以下内容添加到 `sendCommerceExperienceEvent` 函数。 此函数将商务体验事件和产品作为参数：

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
     let xdmData: [String: Any] = [
         "eventType": "commerce." + commerceEventType,
         "commerce": [
             commerceEventType: [
                 "id": product.sku,
                 "value": 1
             ]
         ],
         "productListItems": [
             [
                 "name": product.name,
                 "priceTotal": product.price,
                 "SKU": product.sku
             ]
         ]
     ]
   
     Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
     let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   }
   ```

1. 在 `ProductView` 将各种调用添加到 `sendCommerceExperienceEvent` 函数：

   1. 在 `.task` 中的修饰符 `ATTrackingManager.trackingAuthorizationStatus` 结束。 此 `.task` 在初始化和显示产品视图时，将调用修饰符，这样您就要在特定时刻发送产品视图事件。

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. 对于产品视图中工具栏中的每个按钮（保存以供稍后使用、添加到购物车和购买），添加相关调用。

      * 对于保存以供稍后使用/添加到愿望清单：

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * 对于添加到购物车：

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * 对于购买：

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### 自定义字段组

假设您想跟踪应用程序本身中的屏幕查看次数和交互次数。 请记住，您已为此类型事件定义了自定义字段组。

* 在您的架构中，识别您尝试收集的事件。
  ![应用程序交互模式](assets/datacollection-appInteraction-schema.png)

* 开始构建对象。

  >[!NOTE]
  >
  >  标准字段组始终以对象根开头。
  >
  >  自定义字段组始终以Experience Cloud组织特有的对象开头， `_techmarketingdemos` 在此示例中。

  对于应用程序交互事件，您可以构建如下对象：

  ```swift
  let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
      "appInformation": [
          "appInteraction": [
              "name": "login",
              "appAction": [
                  "value": 1
                  ]
              ]
          ]
      ]
  ]
  ```

  对于屏幕跟踪事件，您可以构建如下对象：

  ```swift
  var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                    "screenName": "luma: content: ios: us: en: login",
                    "screenView": [
                        "value": 1
                    ]
                ]
            ] 
        ]
  ]
  ```


* 然后使用数据结构创建 `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* 将事件和数据发送到Platform Edge Network。

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


再次重申，让我们在您的Xcode项目中实际实施此代码。

1. 为方便起见，您在中定义了两个函数 `MobileSDK`.

   一个用于应用程序交互。 将突出显示的代码添加到 `sendAppInteractionEvent(actionName)` 函数位于 **[!UICONTROL MobileSDK]**：

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
        let xdmData: [String: Any] = [
           "eventType": "application.interaction",
           tenant : [
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
       let appInteractionEvent = ExperienceEvent(xdm: xdmData)
       Edge.sendEvent(experienceEvent: appInteractionEvent)
   }
   ```

   还有一个用于屏幕跟踪。 将高亮显示的代码添加到 `sendTrackScreenEvent(stateName)` 函数位于 **[!UICONTROL MobileSDK]**：

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
      let xdmData: [String: Any] = [
          "eventType": "application.scene",
          tenant : [
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
      ]
      let trackScreenEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: trackScreenEvent)
   }
   ```

1. 导航到 **[!UICONTROL 登录表]**.

   * 在“登录”按钮结尾处添加以下高亮显示的代码：

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * 将以下高亮显示的代码添加到 `onAppear` 修饰符：

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### 验证

1. 查看 [设置说明](assurance.md) 并将模拟器或设备连接到Assurance。
1. 运行应用程序以登录并与产品交互。

   1. 将“Assurance（保证）”图标向左移动。
   1. 选择 **[!UICONTROL 主页]** 在选项卡栏中。
   1. 选择 **[!UICONTROL 登录]** 按钮以打开“登录”工作表。
   1. 选择 **[!UICONTROL A|]** 按钮以插入随机电子邮件和客户id。
   1. 选择 **[!UICONTROL 登录]**.
   1. 选择 **[!UICONTROL 产品]** 在选项卡栏中。
   1. 选择产品。
   1. 选择 **[!UICONTROL 保存供以后使用]**.
   1. 选择 **[!UICONTROL 添加到购物车]**.
   1. 选择 **[!UICONTROL 购买]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. 查找 **[!UICONTROL hitReceived]** 来自的事件 **[!UICONTROL com.adobe.edge.konductor]** 供应商。
1. 选择事件并在以下位置查看XDM数据： **[!UICONTROL 消息]** 对象。
   ![数据收集验证](assets/datacollection-validation.png)


### 在Luma应用程序中实施

您现在应该拥有所有工具，能够开始将数据收集添加到Luma应用程序。 您可以为用户与产品的交互方式添加更多智能，还可以向应用程序添加更多应用程序交互和屏幕跟踪调用：

* 在应用程序中实施订单、结帐、空购物篮和其他功能，并将相关的商务体验事件添加到此功能。
* 重复呼叫 `sendAppInteractionEvent` ，以便通过相应的参数跟踪用户在应用程序中的其他应用程序交互。
* 重复呼叫 `sendTrackScreenEvent` ，以便在应用程序中跟踪用户查看的每个屏幕。

>[!TIP]
>
>查看 [完全实施的应用程序](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 以了解更多示例。


## 将事件发送到Analytics和Platform

现在，您已收集事件并将它们发送到Platform Edge Network，将它们发送到在中配置的应用程序和服务。 [数据流](create-datastream.md). 在后续课程中，您可以将此数据映射到 [Adobe Analytics](analytics.md) 和 [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>现在，您已设置应用程序，以跟踪与Adobe Experience Platform Edge Network以及您在数据流中定义的所有服务的商务、应用程序交互和屏幕跟踪事件。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[WebViews](web-views.md)**
