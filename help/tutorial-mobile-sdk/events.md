---
title: 使用Platform Mobile SDK跟踪移动应用程序中的事件数据
description: 了解如何跟踪移动应用程序中的事件数据。
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---

# 跟踪事件数据

了解如何跟踪移动应用程序中的事件。

Edge Network扩展提供了一个将Experience事件发送到PlatformEdge Network的API。 体验事件是一个对象，其中包含符合XDM ExperienceEvent架构定义的数据。 更简单地说，它们捕获用户在您的移动应用程序中的操作。 平台Edge Network收到数据后，可以将其转发到数据流中配置的应用程序和服务，如Adobe Analytics和Experience Platform。 在产品文档中了解有关[体验事件](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/)的更多信息。

## 先决条件

* 所有包依赖项都已存在于您的Xcode项目中。
* 已在&#x200B;**[!UICONTROL AppDelegate]**&#x200B;中注册扩展。
* 已将MobileCore扩展配置为使用开发`appId`。
* 导入的SDK。
* 通过上述更改成功构建并运行应用程序。

## 学习目标

在本课程中，您将执行以下操作

* 了解如何基于架构构建XDM数据。
* 基于标准字段组发送XDM事件。
* 基于自定义字段组发送XDM事件。
* 发送XDM购买事件。
* 使用保障进行验证。

## 构建体验事件

Adobe Experience Platform Edge扩展可以将遵循之前定义的XDM架构的事件发送到Adobe Experience PlatformEdge Network。

这个过程是这样的……

1. 识别您尝试跟踪的移动应用程序交互。

1. 检查您的架构并确定相应的事件。

1. 查看您的架构并确定应用于描述事件的任何其他字段。

1. 构造和填充数据对象。

1. 创建并发送事件。

1. 验证。


### 标准字段组

对于标准字段组，此过程如下所示：

* 在您的架构中，识别您尝试收集的事件。 在此示例中，您正在跟踪商务体验事件，例如产品查看(**[!UICONTROL productViews]**)事件。

  ![产品视图架构](assets/datacollection-prodView-schema.png)

* 要在应用程序中构建包含体验事件数据的对象，您可以使用以下代码：

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

   * `eventType`：描述发生的事件，尽可能使用[已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values)。
   * `commerce.productViews.value`：事件的数值或布尔值。 如果它是一个布尔值(在Adobe Analytics中为“计数器”)，则该值始终设置为1。 如果是数值或货币事件，该值可以大于1。

* 在您的架构中，标识与商业产品查看事件关联的任何其他数据。 在此示例中，包括&#x200B;**[!UICONTROL productListItems]**，它是用于任何商业相关事件的标准字段集：

  ![产品列表项架构](assets/datacollection-prodListItems-schema.png)
   * 请注意，**[!UICONTROL productListItems]**&#x200B;是一个数组，因此可以提供多个产品。

* 要添加此数据，请展开`xdmData`对象以包含补充数据：

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

* 您现在可以使用此数据结构创建`ExperienceEvent`：

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* 并使用`sendEvent` API将事件和数据发送到PlatformEdge Network：

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API是AEP Mobile SDK等效于[`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction)和[`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate) API调用。 有关详细信息，请参阅[从Analytics移动扩展迁移到Adobe Experience PlatformEdge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/)。

现在，您即将在您的Xcode项目中实际实施此代码。
您的应用程序中有不同的商业产品相关操作，并且您要根据用户执行的以下操作发送事件：

* 视图：在用户查看特定产品时发生，
* 添加到购物车：用户点击时 产品详细信息屏幕中的<img src="assets/addtocart.png" width="20" />，
* 暂存：用户点击时 产品详细信息屏幕中的<img src="assets/saveforlater.png" width="15" />，
* 购买：用户点击时 产品详细信息屏幕中的<img src="assets/purchase.png" width="20" />。

要以可重用方式实施与商业相关的体验事件的发送，请使用专用函数：

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**，并将以下内容添加到`func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`函数。

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
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
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   此函数将商务体验事件类型和产品作为参数和

   * 将XDM有效负载设置为词典，使用函数中的参数，
   * 使用词典设置体验事件，
   * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API发送体验事件。

1. 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]**，并将各种调用添加到`sendCommerceExperienceEvent`函数：

   1. 在`.task`修饰符处，在`ATTrackingManager.trackingAuthorizationStatus`结束处。 在初始化并显示产品视图时调用此`.task`修饰符，以便您想要在该特定时刻发送产品视图事件。

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. 对于每个按钮(<img src="assets/saveforlater.png" width="15" />， <img src="assets/addtocart.png" width="20" />和 <img src="assets/purchase.png" width="20" />)，在`ATTrackingManager.trackingAuthorizationStatus == .authorized`结束位置内添加相关调用：

      1. 对象 <img src="assets/saveforlater.png" width="15" />：

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. 对象 <img src="assets/addtocart.png" width="20" />：

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. 对象 <img src="assets/purchase.png" width="20" />：

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TIP]
>
>如果您正在针对Android™进行开发，请使用映射(`java.util.Map`)作为构建XDM有效负载的基础接口。


### 自定义字段组

假设您想跟踪应用程序本身中的屏幕查看次数和交互次数。 请记住，您已为此类型事件定义了自定义字段组。

* 在您的架构中，识别您尝试收集的事件。
  ![应用交互架构](assets/datacollection-appInteraction-schema.png)

* 开始构建对象。

  >[!NOTE]
  >
  >* 标准字段组始终以对象根开头。
  >
  >* 自定义字段组始终以Experience Cloud组织`_techmarketingdemos`所独有的对象开头。

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


* 您现在可以使用此数据结构创建`ExperienceEvent`。

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* 将事件和数据发送到PlatformEdge Network。

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


再次重申，让我们在您的Xcode项目中实际实施此代码。

1. 为方便起见，您在&#x200B;**[!UICONTROL MobileSDK]**&#x200B;中定义了两个函数。 在Xcode项目导航器中导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**。

   1. 一个用于应用程序交互。 将此代码添加到`func sendAppInteractionEvent(actionName: String)`函数：

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
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
      ```

      此函数使用操作名称作为参数，并且

      * 将XDM有效负载设置为词典，使用函数中的参数，
      * 使用词典设置体验事件，
      * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API发送体验事件。


   1. 还有一个用于屏幕跟踪。 将此代码添加到`func sendTrackScreenEvent(stateName: String) `函数：

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
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
      ```

      此函数使用状态名称作为参数并

      * 将XDM有效负载设置为词典，使用函数中的参数，
      * 使用词典设置体验事件，
      * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API发送体验事件。

1. 导航到&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登录工作表]**。

   1. 在“登录”按钮结尾处添加以下高亮显示的代码：

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. 将以下高亮显示的代码添加到`onAppear`修饰符：

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## 验证

1. 查看[设置说明](assurance.md#connecting-to-a-session)部分，将模拟器或设备与Assurance连接。

   1. 将“Assurance（保证）”图标向左移动。
   1. 在选项卡栏中选择&#x200B;**[!UICONTROL Home]**，并验证您是否在Home屏幕中看到&#x200B;**[!UICONTROL ECID]**、**[!UICONTROL 电子邮件]**&#x200B;和&#x200B;**[!UICONTROL CRM ID]**。
   1. 在选项卡栏中选择&#x200B;**[!DNL Products]**。
   1. 选择产品。
   1. 选择 <img src="assets/saveforlater.png" width="15" />。
   1. 选择 <img src="assets/addtocart.png" width="20" />。
   1. 选择 <img src="assets/purchase.png" width="15" />。

      <img src="./assets/mobile-app-events-3.png" width="300">


1. 在Assurance UI中，查找来自&#x200B;**[!UICONTROL com.adobe.edge.konductor]**&#x200B;供应商的&#x200B;**[!UICONTROL hitReceived]**&#x200B;事件。
1. 选择事件并查看&#x200B;**[!UICONTROL 消息]**&#x200B;对象中的XDM数据。 或者，您可以使用![复制](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL 复制原始事件]**&#x200B;并使用首选项的文本或代码编辑器粘贴和检查该事件。

   ![数据收集验证](assets/datacollection-validation.png)


## 后续步骤

您现在应该拥有所有工具，能够开始向应用程序添加数据收集。 您可以为用户在应用程序中与产品的交互方式添加更多智能，并为应用程序添加更多应用程序交互和屏幕跟踪调用：

* 在应用程序中实施订单、结帐、空购物篮和其他功能，并将相关的商务体验事件添加到此功能。
* 使用相应的参数重复对`sendAppInteractionEvent`的调用，以跟踪用户进行的其他应用程序交互。
* 使用相应的参数重复对`sendTrackScreenEvent`的调用，以跟踪用户在应用程序中查看的屏幕。

>[!TIP]
>
>有关更多示例，请查看[完成的应用程序](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App)。


## 将事件发送到Analytics和Platform

现在您已收集事件并将它们发送到PlatformEdge Network，将它们发送到[数据流](create-datastream.md)中配置的应用程序和服务。 在以后的课程中，您可以将此数据映射到[Adobe Analytics](analytics.md)、[Adobe Experience Platform](platform.md)以及其他Adobe Experience Cloud解决方案，如[Adobe Target](target.md)和Adobe Journey Optimizer。

>[!SUCCESS]
>
>您现在已设置应用程序，以跟踪与Adobe Experience PlatformEdge Network以及您在数据流中定义的所有服务的商务、应用程序交互和屏幕跟踪事件。
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望共享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上共享它们。

下一步： **[处理WebViews](web-views.md)**
