---
title: 发送参数 — 将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Experience PlatformWeb SDK将mbox、配置文件和实体参数发送到Adobe Target。
exl-id: 7916497b-0078-4651-91b1-f53c86dd2100
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 0%

---

# 使用Platform Web SDK将参数发送到Target

由于站点架构、业务要求和使用的功能，Target实施在各个网站之间有所不同。 大多数Target实施都包括传递上下文信息、受众和内容推荐的各种参数。

我们使用简单的产品详细信息页面和订单确认页面来演示在将参数传递到Target时这两个库之间的差异。

假定以下两个使用at.js的示例页面：

“产品详细信息”页面上的+++at.js：

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Mbox parameters
        "pageName": "product detail",
        // Profile parameters
        "profile.gender": "male",
        "user.categoryId": "clothing",
        // Entity parameters for Target Recomendations
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL",
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++


订单确认页面上的+++at.js：

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Order confirmation parameters
        "orderId": "ABC123",
        "productPurchasedId": "SKU-00002,SKU-00003",
        "orderTotal": 1337.89,
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++


## 参数映射摘要

使用Platform Web SDK发送这些页面的Target参数的方式有所不同。 可以使用at.js通过多种方法将参数传递到Target：

- 为页面加载事件使用`targetPageParams()`函数设置（在此页面的示例中使用）
- 为页面上的所有Target请求使用`targetPageParamsAll()`函数设置
- 使用单个位置的`getOffer()`函数直接发送参数
- 直接使用`getOffers()`函数为一个或多个位置发送参数


Platform Web SDK提供了一种统一的数据发送方式，而无需使用额外的功能。 必须使用`sendEvent`命令在有效负载中传递所有参数，并且这些参数属于两个类别：

- 自动从`xdm`对象映射
- 使用`data.__adobe.target`对象手动传递

下表概述了如何使用Platform Web SDK重新映射示例参数：

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

必须使用`sendEvent`命令将自定义mbox参数作为XDM数据传递。 请务必确保XDM架构包含Target实施所需的所有字段。

at.js使用`targetPageParams()`的示例：

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

使用`sendEvent`命令的Platform Web SDK JavaScript示例：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "name": "product detail"
      }
    }
  }
});
```

>[!TAB 标记]

在标记中，首先使用[!UICONTROL XDM对象]数据元素映射到XDM字段：

![映射到XDM对象数据元素中的XDM字段](assets/params-tags-pageName.png){zoomable="yes"}

然后，将您的[!UICONTROL XDM对象]包含在您的[!UICONTROL 发送事件] [!UICONTROL 操作]中（多个[!UICONTROL XDM对象]可以[合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在发送事件中包含XDM对象数据元素](assets/params-tags-sendEvent.png){zoomable="yes"}

>[!ENDTABS]


>[!NOTE]
>
>由于自定义mbox参数是`xdm`对象的一部分，因此您需要更新任何受众、活动或使用新名称引用这些mbox参数的配置文件脚本。 有关更多信息，请参阅本教程的[更新Target受众和配置文件脚本以了解Platform Web SDK兼容性](update-audiences.md)页面。


## 配置文件参数

必须在Platform Web SDK `sendEvent`命令有效负载中的`data.__adobe.target`对象下传递目标配置文件参数。

与at.js类似，所有配置文件参数也必须添加前缀`profile.`，以便将该值正确存储为永久性Target配置文件属性。 Target的类别亲和度功能保留的`user.categoryId`参数带有前缀`user.`。

at.js使用`targetPageParams()`的示例：

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

使用`sendEvent`命令的Platform Web SDK示例：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "male",
        "user.categoryId": "clothing"
      }
    }
  }
});
```

>[!TAB 标记]

在标记中，首先创建一个数据元素以定义`data.__adobe.target`对象：

![在数据元素中定义数据对象](assets/params-tags-dataObject.png){zoomable="yes"}

然后，将数据对象包含在[!UICONTROL 发送事件] [!UICONTROL 操作]中（多个[!UICONTROL 对象]可以[合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在发送事件中包含数据对象](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

## 实体参数

实体参数用于为Target Recommendations传递行为数据和补充目录信息。 at.js支持的所有[实体参数](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html)也受Platform Web SDK支持。 与配置文件参数类似，所有实体参数都应在Platform Web SDK `sendEvent`命令有效负载中的`data.__adobe.target`对象下传递。

特定项的实体参数必须以`entity.`为前缀，才能正确捕获数据。 不应为推荐算法保留的`cartIds`和`excludedIds`参数添加前缀，每个参数的值都必须包含以逗号分隔的实体ID列表。

at.js使用`targetPageParams()`的示例：

```JavaScript
targetPageParams = function() {
  return {
    "entity.id": "SKU-00001-LARGE",
    "entity.categoryId": "clothing,shirts",
    "entity.customEntity": "some value",
    "cartIds": "SKU-00002,SKU-00003",
    "excludedIds": "SKU-00001-SMALL"
  };
};
```

使用`sendEvent`命令的Platform Web SDK示例：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

>[!TAB 标记]

在标记中，首先创建一个数据元素以定义`data.__adobe.target`对象：

![在数据元素中定义数据对象](assets/params-tags-dataObject-entities.png){zoomable="yes"}

然后，将数据对象包含在[!UICONTROL 发送事件] [!UICONTROL 操作]中（多个[!UICONTROL 对象]可以[合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在发送事件中包含数据对象](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
>如果使用`commerce`字段组并且XDM有效负载中包含`productListItems`数组，则此数组中的第一个`SKU`值将映射到`entity.id`，以便递增产品视图。


## 购买参数

成功完成订单后，采购参数会在订单确认页面上传递，并用于Target转化和优化目标。 通过Platform Web SDK实施，这些参数和自动从作为`commerce`字段组的一部分传递的XDM数据进行映射。

at.js使用`targetPageParams()`的示例：

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

当`commerce`字段组的`purchases.value`设置为`1`时，购买信息将传递到Target。 订单ID和订单总计自动从`order`对象映射。 如果`productListItems`数组存在，则`SKU`值将用于`productPurchasedId`。

使用`sendEvent`命令的Platform Web SDK示例：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "ABC123",
        "priceTotal": 1337.89
      },
      "purchases": {
        "value": 1
      }
    },
    "productListItems": [{
      "SKU": "SKU-00002"
    }, {
      "SKU": "SKU-00003"
    }]
  }
});
```

>[!TAB 标记]

在标记中，首先使用[!UICONTROL XDM对象]数据元素映射到XDM字段：

![映射到XDM对象数据元素中的XDM字段](assets/params-tags-purchase.png){zoomable="yes"}

然后，将您的[!UICONTROL XDM对象]包含在您的[!UICONTROL 发送事件] [!UICONTROL 操作]中（多个[!UICONTROL XDM对象]可以[合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在发送事件中包含XDM对象数据元素](assets/params-tags-sendEvent-purchase.png){zoomable="yes"}

>[!ENDTABS]


>[!NOTE]
>
>`productPurchasedId`值还可以作为`data`对象下以逗号分隔的实体ID列表传递。


## 客户ID (mbox3rdPartyId)

Target允许使用单个客户ID跨设备和系统同步配置文件。 使用at.js时，可以将其设置为Target请求中的`mbox3rdPartyId`，或设置为发送到Experience CloudIdentity服务的第一个客户ID。 与at.js不同，Platform Web SDK实施允许您指定在存在多个客户ID时用作`mbox3rdPartyId`的客户ID。 例如，如果贵企业有一个全局客户ID，并且不同业务线的客户ID各不相同，则可以配置Target应使用哪个ID。

要为Target跨设备和客户属性用例设置ID同步，需要执行几个步骤：

1. 在Data Collection或Platform的&#x200B;**[!UICONTROL 标识]**&#x200B;屏幕中为客户ID创建&#x200B;**[!UICONTROL 标识命名空间]**
1. 确保客户属性中的&#x200B;**[!UICONTROL 别名]**&#x200B;与命名空间中的&#x200B;**[!UICONTROL 身份符号]**&#x200B;匹配
1. 在数据流的Target配置中将&#x200B;**[!UICONTROL identity符号]**&#x200B;指定为&#x200B;**[!UICONTROL Target第三方ID命名空间]**
1. 使用`identityMap`字段组执行`sendEvent`命令

at.js使用`targetPageParams()`的示例：

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

使用`sendEvent`命令的Platform Web SDK示例：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated"
      }]
    }
  }
});
```

>[!TAB 标记]

[!UICONTROL ID]值、[!UICONTROL 身份验证状态]和[!UICONTROL 命名空间]已在[!UICONTROL 标识映射]数据元素中捕获：
![标识映射数据元素捕获客户ID](assets/params-tags-customerIdDataElement.png){zoomable="yes"}

然后使用[!UICONTROL 标识映射]数据元素设置[!UICONTROL XDM对象]数据元素中的[!UICONTROL identityMap]字段：
![在XDM对象数据元素中使用的标识映射数据元素](assets/params-tags-customerIdInXDMObject.png){zoomable="yes"}

然后，[!UICONTROL XDM对象]将包含在规则的[!UICONTROL 发送事件]操作中：

![在发送事件中包含XDM对象数据元素](assets/params-tags-sendEvent-xdm.png){zoomable="yes"}

在数据流的Adobe Target服务中，确保将[!UICONTROL Target第三方ID命名空间]设置为[!UICONTROL 标识映射]数据元素中使用的相同命名空间：
![在数据流中设置目标第三方ID命名空间](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable="yes"}

>[!ENDTABS]

## 平台Web SDK示例

现在，您已了解如何使用Platform Web SDK映射不同的Target参数，接下来可以将我们的两个示例页面从at.js迁移到Platform Web SDK，如下所示。 示例页面包括：

- 用于异步库实施的Target预隐藏代码片段
- Platform Web SDK基础代码
- Platform Web SDK JavaScript库
- 用于初始化库的`configure`命令
- 用于发送数据和请求渲染目标内容的`sendEvent`命令

产品详细信息页面上的+++Web SDK：

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "renderDecisions": true,
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "pageName": "product detail"
          }
        }
      },
      "data": {
        "__adobe": {
          "target": {
            "profile.gender": "male",
            "user.categoryId": "clothing",
            "entity.id": "SKU-00001-LARGE",
            "entity.categoryId": "clothing,shirts",
            "entity.customEntity": "some value",
            "cartIds": "SKU-00002,SKU-00003",
            "excludedIds": "SKU-00001-SMALL"
          }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++

订单确认页面上的+++Web SDK：

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>


  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->

  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->

  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>
  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "commerce": {
          "order": {
            "purchaseID": "ABC123",
            "priceTotal": 1337.89
          },
          "purchases": {
            "value": 1
          }
        },
        "productListItems": [{
          "SKU": "SKU-00002"
        }, {
          "SKU": "SKU-00003"
        }]
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++

接下来，了解如何使用Platform Web SDK [跟踪Target转化事件](track-events.md)。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
