---
title: 将使用Platform Mobile SDK收集的数据映射到Adobe Analytics
description: 了解如何在移动应用程序中收集和映射Adobe Analytics的数据。
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 3186788dfb834f980f743cef82942b3cf468a857
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---

# 收集和映射Analytics数据

了解如何将移动数据映射到Adobe Analytics。

此 [事件](events.md) 您在之前的课程中收集并发送到Platform Edge Network的数据将转发到您在数据流中配置的服务，包括Adobe Analytics。 您可以将数据映射到报表包中的正确变量。

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

要将XDM数据从Edge Network发送到Adobe Analytics，请将Adobe Analytics服务配置为包含在中设置的数据流 [创建数据流](create-datastream.md).

1. 在数据收集UI中，选择 **[!UICONTROL 数据流]** 和您的数据流。

1. 然后选择 ![添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 添加服务]**.

1. 添加 **[!UICONTROL Adobe Analytics]** 从 [!UICONTROL 服务] 列表，

1. 输入Adobe Analytics中要在其中使用的报表包的名称 **[!UICONTROL 报表包ID]**.

1. 通过切换启用服务 **[!UICONTROL 已启用]** 打开。

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![将Adobe Analytics添加为数据流服务](assets/datastream-service-aa.png)


## 自动映射

许多标准XDM字段会自动映射到Analytics变量。 请在[此处](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)查看完整列表。

### 示例#1 - s.products

一个很好的示例是 [products变量](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 无法使用处理规则填充的部分。 对于XDM实施，您会将所有必需的数据传入 `productListItems` 和 `s.products` 通过Analytics映射自动填充。

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
s.products = ";5829,1,49.99;9841,3,30.00"
```

>[!NOTE]
>
>如果 `productListItems[].SKU` 和 `productListItems[].name` 两者都包含数据，值位于 `productListItems[].SKU` 已使用。 请参阅 [Analytics Experience Edge中的Adobe变量映射](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en) 以了解更多信息。


### 示例#2 - scAdd

仔细查看，所有事件都有两个字段 `value` （必需）和 `id` （可选）。 此 `value` 字段用于递增事件计数。 此 `id` 字段用于序列化。

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

## 使用保障进行验证

使用 [Assurance](assurance.md) 您可以确认正在发送体验事件，XDM数据正确，并且Analytics映射按预期进行。

1. 查看 [设置说明](assurance.md#connecting-to-a-session) 部分以将模拟器或设备连接到Assurance。

1. 发送 **[!UICONTROL productListAdd]** 活动（向购物篮中添加产品）。

1. 查看ExperienceEvent点击。

   ![analytics xdm点击](assets/analytics-assurance-experiencevent.png)

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

1. 查看 **[!UICONTROL analytics.mapping]** 事件。

   ![analytics xdm点击](assets/analytics-assurance-mapping.png)

在Analytics映射中注意以下事项：

* **[!UICONTROL 事件]** 填充了 `scAdd` 基于 `commerce.productListAdds`.
* **[!UICONTROL pl]** （产品变量）填充了一个拼接值，该拼接值基于 `productListItems`.
* 此事件中还有其它有趣的信息，包括所有上下文数据。


## 与上下文数据映射

转发到Analytics的XDM数据将转换为 [上下文数据](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) 包括标准和自定义字段。

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
>`_techmarketingdemos` 将被替换为您的组织的唯一值。



要将此XDM上下文数据映射到报表包中的Analytics数据，您可以：

### 使用字段组

* 添加 **[!UICONTROL Adobe Analytics ExperienceEvent完整扩展]** 字段组添加到您的架构。

  ![Analytics ExperienceEvent FullExtension字段组](assets/schema-analytics-extension.png)

* 在应用程序中构建XDM负载，与Adobe Analytics ExperienceEvent Full Extension字段组保持一致，类似于在中完成的工作 [跟踪事件数据](events.md) 课程，或
* 在Tags属性中生成规则，这些规则使用规则操作将数据附加或修改到Adobe Analytics ExperienceEvent Full Extension字段组。 有关更多详细信息，请参阅 [将数据附加到SDK事件](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) 或 [修改SDK事件中的数据](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### 使用处理规则

以下是使用此数据的处理规则的外观：

* 您 **[!UICONTROL 覆盖值]** (1) **[!UICONTROL 应用程序屏幕名称(eVar2)]** (2)具有下列值： **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3)如果 **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL 已设置]** （五）。

* 您 **[!UICONTROL 设置事件]** (6) **[!UICONTROL 添加到愿望清单（事件3）]** (7)至 **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8)如果 **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL 已设置]** (10)。

![analytics处理规则](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>某些自动映射的变量在处理规则中可能不可用。
>
>
>首次映射到处理规则时，界面不会显示XDM对象中的上下文数据变量。 要修复该错误，请选择任意值，请保存并返回进行编辑。 此时应会显示所有XDM变量。


可找到有关处理规则和上下文数据的其他信息 [此处](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>与以前的移动应用程序实施不同，页面/屏幕查看次数与其他事件之间没有区别。 相反，您可以递增 **[!UICONTROL 页面查看]** 量度，方法是设置 **[!UICONTROL 页面名称]** 处理规则中的维度。 由于您正在收集自定义 `screenName` 字段，强烈建议将屏幕名称映射到 **[!UICONTROL 页面名称]** 在处理规则中。


>[!SUCCESS]
>
>您已设置应用程序，将Experience Edge XDM对象映射到Adobe Analytics变量，以在您的数据流中启用Adobe Analytics服务并在适用的情况下使用处理规则。<br/> 感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[将数据发送到Experience Platform](platform.md)**
