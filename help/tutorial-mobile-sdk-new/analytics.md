---
title: Analytics映射
description: 了解如何在移动应用程序中收集Adobe Analytics的数据。
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: 371d71f06796c0f7825217a2ebd87d72ae7e8639
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 3%

---

# Analytics映射

了解如何将移动数据映射到Adobe Analytics。

此 [事件](events.md) 您在之前的课程中收集并发送到Platform Edge Network的数据将转发到您在数据流中配置的服务，包括Adobe Analytics。 您可以将数据映射到报表包中的正确变量。

## 先决条件

* 了解ExperienceEvent跟踪。
* 在示例应用程序中成功发送XDM数据。
* 数据流已配置给Adobe Analytics

## 学习目标

在本课程中，您将执行以下操作：

* 了解Analytics变量的自动映射。
* 设置处理规则以将XDM数据映射到Analytics变量。

## 自动映射

许多标准XDM字段会自动映射到Analytics变量。 请在[此处](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en)查看完整列表。

### 示例#1 - s.products

一个很好的示例是 [products变量](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=zh-Hans) 无法使用处理规则填充的部分。 对于XDM实施，您会将所有必需的数据传入 `productListItems` 和 `s.products` 通过Analytics映射自动填充。

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
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>当前 `productListItems[N].SKU` 被自动映射忽略。


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

使用 [Assurance](assurance.md) 您可以确认正在发送体验事件，XDM数据正确，并且Analytics映射按预期进行。 例如：

1. 发送productListAdds事件。

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
       "id" : "LLWS05.1-XS",
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
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>自定义字段放在Experience Cloud组织标识符下。
>
>`_techmarketingdemos` 将被替换为您的组织的唯一值。


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
>首次映射到处理规则时，UI不会显示XDM对象中的上下文数据变量。 要修复该错误，请选择任意值，请保存并返回进行编辑。 此时应会显示所有XDM变量。


可以找到有关处理规则和上下文数据的其他信息 [此处](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>与以前的移动应用程序实施不同，页面/屏幕查看次数与其他事件之间没有区别。 相反，您可以递增 **[!UICONTROL 页面查看]** 量度，方法是设置 **[!UICONTROL 页面名称]** 处理规则中的维度。 由于您正在收集自定义 `screenName` 字段，强烈建议将屏幕名称映射到 **[!UICONTROL 页面名称]** 在处理规则中。

>[!SUCCESS]
>
>您已设置应用程序，将Experience Edge XDM对象映射到Adobe Analytics变量，以在您的数据流中启用Adobe Analytics服务并在适用的情况下使用处理规则。<br/> 感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[Experience Platform](platform.md)**
