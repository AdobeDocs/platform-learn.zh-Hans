---
title: 为Platform Web SDK创建数据元素
description: 了解如何在标记中创建XDM对象并将数据元素映射到该对象。 本课程是《使用 Web SDK 实施 Adobe Experience Cloud》教程的一部分。
feature: Tags
jira: KT-15401
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 2%

---

# 创建数据元素

了解如何在标记中创建数据元素，以在上的内容、商业和身份数据 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html). 然后，使用Adobe Experience Platform Web SDK扩展变量数据元素类型填充XDM架构中的字段。

## 学习目标

在本课程结束时，您能够：

* 了解将数据层映射到XDM的不同方法
* 创建数据元素以捕获数据
* 将数据元素映射到XDM对象


## 先决条件

您已了解数据层是什么，并完成了本教程中之前的课程：

* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)


>[!IMPORTANT]
>
>本课程的数据来自 `[!UICONTROL digitalData]` Luma网站的数据层。 要查看数据层，请打开您的开发人员控制台并键入 `[!UICONTROL digitalData]` 以查看完整的数据层。![digitalData数据层](assets/data-element-data-layer.png)


## 数据层方法

使用Adobe Experience Platform的标记功能，可通过多种方式将数据从数据层映射到XDM。 以下是三种不同方法的一些优点和缺点。 如果需要，可以合并方法：

1. 在数据层中实施XDM
1. 在标记中映射到XDM
1. 在数据流中映射到XDM

>[!NOTE]
>
>本教程中的示例遵循标记中映射到XDM的方法。


### 在数据层中实施XDM

此方法涉及使用完全定义的XDM对象作为数据层的结构。 然后，将整个数据层映射到标记中的XDM对象数据元素。 如果您的实施不使用标签管理器，则此方法可能是理想的，因为您可以使用将数据直接从应用程序发送到XDM [XDM sendEvent命令](https://experienceleague.adobe.com/en/docs/experience-platform/edge/fundamentals/tracking-events#sending-xdm-data). 如果您确实使用标记，则可以创建一个自定义代码数据元素，它将整个数据层作为传递到XDM的JSON对象进行捕获。 然后，将传递JSON映射到发送事件操作中的XDM对象字段。

以下是使用Adobe客户端数据层格式时数据层的外观示例：

数据层中的+++XDM示例

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

优点

* 无需重新映射到数据层变量到XDM的其他步骤
* 如果您的Web开发团队也拥有标记数字行为，则部署可能会更快

缺点

* 完全依靠开发团队和开发周期来更新要传输到XDM的数据
* XDM从数据层接收确切的有效负载时灵活性有限
* 无法使用内置标记功能（例如刮擦功能、持久性功能和快速部署功能）
* 将数据层用于第三方像素比较困难(但您可能希望将这些像素移动到 [事件转发](setup-event-forwarding.md)！
* 无法转换数据层和XDM之间的数据

### 在标记中映射数据层

此方法包括将单独的数据层变量或数据层对象映射到标记中的数据元素，并最终映射到XDM。 这是使用标签管理系统实施的传统方法。

#### 优点

* 最灵活的方法，因为您可以控制单个变量并在数据进入XDM之前转换数据
* 可以使用Adobe标记触发器和刮取功能将数据传递到XDM
* 可以将数据元素映射到客户端的第三方像素

#### 缺点

* 将数据层重构为数据元素需要时间


>[!TIP]
>
> Google Data Layer
> 
> 如果您的组织已经使用Google Analytics，并且网站上具有传统的Google dataLayer对象，则可以使用 [Google数据层扩展](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/google-data-layer/overview) 在标记中。 这使您能够更快地部署Adobe技术，而无需请求IT团队的支持。 将Google数据层映射到XDM将遵循与上述相同的步骤。

### 在数据流中映射到XDM

此方法使用数据流配置中内置的功能，称为 [为数据收集准备数据](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/data-prep) 和跳过将数据层变量映射到标记中的XDM。

#### 优点

* 灵活，因为您可以将各个变量映射到XDM
* 能够 [计算新值](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/functions) 或 [转换数据类型](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/data-handling) 从Data Layer转到XDM
* 利用 [映射Ui](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/data-prep#create-mapping) 使用点击UI将源数据中的字段映射到XDM

#### 缺点

* 不能将数据层变量用作客户端第三方像素的数据元素，但可以将它们用于事件转发
* 无法使用Adobe Experience Platform的标记功能的刮擦功能
* 如果在标记和数据流中同时映射数据层，则维护复杂性会增加



>[!IMPORTANT]
>
>如前所述，本教程中的示例遵循标记中映射到XDM的方法。

## 创建数据元素以捕获数据层

在创建XDM对象之前，请为 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 数据层：

1. 转到 **[!UICONTROL 数据元素]** 并选择 **[!UICONTROL 添加数据元素]** (或 **[!UICONTROL 创建新数据元素]** 如果标记属性中没有现有的数据元素)

   ![创建数据元素](assets/data-element-create.png)

1. 将数据元素命名为 `page.pageInfo.pageName`
1. 使用 **[!UICONTROL JavaScript变量]** **[!UICONTROL 数据元素类型]** 指向Luma数据层中的值： `digitalData.page.pageInfo.pageName`

1. 选中复选框 **[!UICONTROL 强制使用小写值]** 和 **[!UICONTROL 清除文本]** 标准化大小写并删除无关空格

1. 离开 `None` 作为 **[!UICONTROL 存储持续时间]** 设置，因为该值在每个页面上都不相同

1. 选择 **[!UICONTROL 保存]**

   ![Page Name数据元素](assets/data-element-pageName.png)

按照以下相同步骤创建这些附加数据元素：

* **`page.pageInfo.server`**  已映射到
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  已映射到
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  已映射到
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** 已映射到
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`product.productInfo.sku`** 已映射到 `digitalData.product.0.productInfo.sku`
<!--digitalData.product.0.productInfo.sku
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.sku;
    });
    return cartItem;
    ```
    -->
* **`product.productInfo.title`** 已映射到 `digitalData.product.0.productInfo.title`
* **`cart.orderId`** 已映射到 `digitalData.cart.orderId`
<!--
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.title;
    });
    return cartItem;
    ```
    -->
* **`product.category`** 使用 **[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素类型]** 和以下自定义代码来解析顶级类别的网站URL：

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`cart.productInfo`** 使用以下自定义代码：

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  cartItem.push({
  "SKU": item.sku
  });
  });
  return cartItem; 
  ```

* **`cart.productInfo.purchase`** 使用以下自定义代码：

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  var qty = parseInt(item.qty);
  var price = parseInt(item.price);
  cartItem.push({
  "SKU": item.sku,
  "quantity": qty,
  "priceTotal": price
  });
  });
  return cartItem; 
  ```



>[!CAUTION]
>
>此 [!UICONTROL JavaScript变量] 数据元素类型将数组引用视为圆点而不是方括号，因此引用username数据元素为 `digitalData.user[0].profile[0].attributes.username` **不起作用**.

## 为XDM和数据对象创建变量数据元素

您刚刚创建的数据元素将用于构建XDM对象（适用于Platform应用程序）和数据对象(适用于Analytics、Target和Audience Manager)。 这些对象具有属于自己的特殊数据元素，称为 **[!UICONTROL 变量]** 很容易创建的数据元素。

要为XDM创建Variable数据元素，请将其绑定到您在 [配置架构](configure-schemas.md) 教训：

1. 选择 **[!UICONTROL 添加数据元素]**
1. 命名数据元素 `xdm.variable.content`. 建议您为特定于XDM的数据元素添加“xdm”前缀，以便更好地组织标记属性
1. 选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 作为 **[!UICONTROL 扩展名]**
1. 选择 **[!UICONTROL 变量]** 作为 **[!UICONTROL 数据元素类型]**
1. 选择 **[!UICONTROL XDM]** 作为 **[!UICONTROL 属性]**
1. 选择 **[!UICONTROL 沙盒]** 在其中创建了架构
1. 选择适当的 **[!UICONTROL 架构]**，在本例中 `Luma Web Event Data`
1. 选择 **[!UICONTROL 保存]**

   ![XDM的变量数据元素](assets/analytics-tags-data-element-xdm-variable.png)

接下来，为数据对象创建变量数据元素：

1. 选择 **[!UICONTROL 添加数据元素]**
1. 命名数据元素 `data.variable`. 建议您在数据对象的特定数据元素中添加“data”作为前缀，以更好地组织标记属性
1. 选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 作为 **[!UICONTROL 扩展名]**
1. 选择 **[!UICONTROL 变量]** 作为 **[!UICONTROL 数据元素类型]**
1. 选择 **[!UICONTROL 数据]** 作为 **[!UICONTROL 属性]**
1. 在本教程中，选择要实施的Experience Cloud解决方案
1. 选择 **[!UICONTROL 保存]**

   ![数据对象的变量数据元素](assets/data-element-data-variable.png.png)


在这些步骤结束时，您应该创建以下数据元素：

| 核心扩展数据元素 | Platform Web SDK扩展数据元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `xdm.variable.content` |
| `cart.productInfo.purchase` | |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

>[!TIP]
>
>在未来 [创建标记规则](create-tag-rule.md) 课程，您学习如何 **[!UICONTROL 变量]** 数据元素允许您使用 **[!UICONTROL 更新变量操作类型]**.

设置这些数据元素后，您就可以开始使用标记规则将数据发送到PlatformEdge Network。 但首先，了解如何使用Web SDK收集身份。

[下一步： ](create-identities.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
