---
title: 将使用Platform Mobile SDK收集的数据映射到Adobe Analytics
description: 了解如何在移动应用程序中收集和映射Adobe Analytics的数据。
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 30dd0142f1f5220f30c45d58665b710a06c827a8
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# 收集和映射Analytics数据

了解如何将移动数据映射到Adobe Analytics。

您在前面的课程中收集并发送到PlatformEdge Network的[event](events.md)数据将转发到您在数据流中配置的服务，包括Adobe Analytics。 您可以将数据映射到报表包中的正确变量。

![架构](assets/architecture-aa.png)

## 先决条件

* 了解ExperienceEvent跟踪。
* 在示例应用程序中成功发送XDM数据。
* 可用于本课程的Adobe Analytics报表包。

## 学习目标

在本课程中，您将执行以下操作：

* 使用Adobe Analytics服务配置数据流。
* 了解Analytics变量的自动映射。
* 设置处理规则以将XDM数据映射到Analytics变量。

## 添加Adobe Analytics数据流服务

要将XDM数据从Edge Network发送到Adobe Analytics，请将Adobe Analytics服务配置为您在[创建数据流](create-datastream.md)过程中设置的数据流。

1. 在数据收集UI中，选择&#x200B;**[!UICONTROL 数据流]**&#x200B;和您的数据流。

1. 然后选择![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加服务]**。

1. 从[!UICONTROL 服务]列表中添加&#x200B;**[!UICONTROL Adobe Analytics]**，

1. 在Adobe Analytics中输入要在&#x200B;**[!UICONTROL 报表包ID]**&#x200B;中使用的报表包名称。

1. 通过将&#x200B;**[!UICONTROL 已启用]**&#x200B;切换为开启来启用服务。

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![将Adobe Analytics添加为数据流服务](assets/datastream-service-aa.png)


## 自动映射

许多标准XDM字段会自动映射到Analytics变量。 请在[此处](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)查看完整列表。

### 示例#1 - s.products

无法使用处理规则填充的[products变量](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)就是一个很好的示例。 对于XDM实施，您传递了`productListItems`中的所有必需数据，并且`s.products`通过Analytics映射自动填充。

此对象：

```swift
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
```

结果位于：

```
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>如果`productListItems[].SKU`和`productListItems[].name`都包含数据，则使用`productListItems[].SKU`中的值。 有关详细信息，请参阅AdobeExperience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)中的[Analytics变量映射。


### 示例#2 - scAdd

如果仔细查看，则所有事件都有两个字段`value`（必需）和`id`（可选）。 `value`字段用于递增事件计数。 `id`字段用于序列化。

此对象：

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

结果位于：

```
s.events = "scAdd"
```

此对象：

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

结果位于：

```
s.events = "scAdd:321435"
```

## 使用保证功能进行验证

使用[保证](assurance.md)，您可以确认正在发送体验事件，XDM数据正确，并且Analytics映射按预期发生。

1. 查看[设置说明](assurance.md#connecting-to-a-session)部分以将模拟器或设备连接到Assurance。

1. 发送&#x200B;**[!UICONTROL productListAdds]**&#x200B;事件（向购物篮中添加产品）。

1. 查看ExperienceEvent点击。

   ![分析xdm点击](assets/analytics-assurance-experiencevent.png)

1. 查看JSON的XDM部分。

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "value" : 1
     }
   }
   // ...
   ```

1. 查看&#x200B;**[!UICONTROL analytics.mapping]**&#x200B;事件。

   ![分析xdm点击](assets/analytics-assurance-mapping.png)

在Analytics映射中注意以下事项：

* 已基于`commerce.productListAdds`使用`scAdd`填充&#x200B;**[!UICONTROL 事件]**。
* **[!UICONTROL pl]** （产品变量）已使用基于`productListItems`的串联值填充。
* 此事件中还有其它有趣的信息，包括所有上下文数据。


## 与上下文数据映射

转发到Analytics的XDM数据将转换为[上下文数据](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en)，包括标准字段和自定义字段。

上下文数据键按以下语法构建：

```
a.x.[xdm path]
```

例如：

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>自定义字段放在Experience Cloud组织标识符下。
>
>`_techmarketingdemos`被替换为您的组织的唯一值。



要将此XDM上下文数据映射到报表包中的Analytics数据，您可以：

### 使用字段组

* 将&#x200B;**[!UICONTROL Adobe Analytics ExperienceEvent完整扩展]**&#x200B;字段组添加到您的架构中。

  ![Analytics ExperienceEvent FullExtension字段组](assets/schema-analytics-extension.png)

* 在应用程序中构建XDM负载，与Adobe Analytics ExperienceEvent Full Extension字段组一致，类似于您在[跟踪事件数据](events.md)课程中所执行的操作，或者
* 在Tags属性中生成规则，这些规则使用规则操作将数据附加或修改到Adobe Analytics ExperienceEvent Full Extension字段组。 查看更多详细信息[将数据附加到SDK事件](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/)或[修改SDK事件中的数据](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/)。


### 促销eVar

如果您在Analytics设置中使用[促销eVar](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars.html?lang=en)，例如为了捕获产品（如`&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`）的颜色，您必须扩展您在[跟踪事件数据](events.md)中定义的XDM有效负载以捕获该促销信息。

* 在JSON中：

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* 在代码中：

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### 使用处理规则

以下是使用此数据的处理规则的外观：

* 如果设置了&#x200B;**[!UICONTROL a.x._techmarketingdemo.appstatedetails.screenname]** (4) **[!UICONTROL (5)，则您**[!UICONTROL &#x200B;用值&#x200B;**[!UICONTROL a.x._techmarketingdemo.appstatedetails.appstatedetails.screenname]** (3)覆盖&#x200B;]**(1)的值**[!UICONTROL &#x200B;应用程序屏幕名称(eVar2)]**(2)]** (5)。

* 如果设置了&#x200B;**[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **** (10)，则您&#x200B;**[!UICONTROL 将event]** (6) **[!UICONTROL Add to Wishlist (Event 3)]** (7)设置为&#x200B;**[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8)。

![分析处理规则](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>某些自动映射的变量在处理规则中可能不可用。
>
>
>首次映射到处理规则时，界面不会显示XDM对象中的上下文数据变量。 要修复该错误，请选择任意值，请保存并返回进行编辑。 此时应会显示所有XDM变量。


可在[此处](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en)找到有关处理规则和上下文数据的其他信息。

>[!TIP]
>
>与以前的移动应用程序实施不同，页面/屏幕查看次数与其他事件之间没有区别。 相反，您可以通过在处理规则中设置&#x200B;**[!UICONTROL 页面名称]**&#x200B;维度来递增&#x200B;**[!UICONTROL 页面查看]**&#x200B;量度。 由于您正在教程中收集自定义`screenName`字段，因此强烈建议在处理规则中将屏幕名称映射到&#x200B;**[!UICONTROL 页面名称]**。


>[!SUCCESS]
>
>您已设置应用程序，以将您的Experience Edge XDM对象映射到在您的数据流中启用Adobe Analytics服务的Adobe Analytics变量，并在适用的情况下使用处理规则。<br/>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望共享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上共享它们。

下一步： **[将数据发送到Experience Platform](platform.md)**
