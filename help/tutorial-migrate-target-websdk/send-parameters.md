---
title: 发送参数 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Experience PlatformWeb SDK将mbox、配置文件和实体参数发送到Adobe Target。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 1%

---

# 使用Platform Web SDK将参数发送到Target

Target实施因站点架构、业务需求和所使用的功能而异。 大多数Target实施包括为上下文信息、受众和内容推荐传递各种参数。

让我们使用简单的产品详细信息页面和订单确认页面来演示库在将参数传递到Target时之间的差异。

假定以下两个使用at.js的示例页面：

+++产品详细信息页面上的at.js:

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


+++订单确认页面上的at.js:

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

使用Platform Web SDK会以不同方式发送这些页面的Target参数。 使用at.js可通过多种方式将参数传递到Target:

- 设置为 `targetPageParams()` 函数（在本页的示例中使用）
- 设置为 `targetPageParamsAll()` 函数
- 直接使用 `getOffer()` 函数
- 直接使用 `getOffers()` 用于一个或多个位置


Platform Web SDK提供了一种发送数据的一致方式，无需额外的功能。 所有参数都必须在有效负载中通过 `sendEvent` 命令和属于两类：

- 自动从 `xdm` 对象
- 使用手动传递 `data.__adobe.target` 对象

下表概述了如何使用Platform Web SDK重新映射示例参数：

| at.js参数示例 | 平台Web SDK选项 | 注释 |
| --- | --- | --- |
| `at_property` | 不适用 | 属性令牌在 [数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) 和无法在中设置 `sendEvent` 呼叫。 |
| `pageName` | `xdm.web.webPageDetails.name` | 所有Target mbox参数都必须作为 `xdm` 对象，并使用XDM ExperienceEvent类符合架构。 Mbox参数不能作为 `data` 对象。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target配置文件参数都必须作为 `data` 对象和前缀为 `profile.` 以正确映射。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用于Target类别亲和度功能的保留参数，该功能必须作为 `data` 对象。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或者<br> `xdm.productListItems[0].SKU` | 实体ID用于Target Recommendations行为计数器。 这些实体ID可以作为 `data` 对象或自动从 `xdm.productListItems` 数组（如果您的实施使用该字段组）。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 实体类别ID可作为 `data` 对象。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自定义实体参数用于更新Recommendations产品目录。 这些自定义参数必须作为 `data` 对象。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用于Target基于购物车的推荐算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用于阻止特定实体ID在推荐设计中返回。 |
| `mbox3rdPartyId` | 在 `xdm.identityMap` 对象 | 用于跨设备和客户属性同步Target配置文件。 必须在 [数据流的目标配置](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | 用于识别Target转化跟踪的唯一顺序。 |
| `orderTotal` | `xdm.commerce.order.priceTotal` | 用于跟踪Target转化和优化目标的订单总计。 |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>或者<br> `xdm.productListItems[0-n].SKU` | 用于Target转化跟踪和推荐算法。 请参阅 [实体参数](#entity-parameters) 部分以了解详细信息。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用于 [自定义评分](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) 活动目标。 |

{style=&quot;table-layout:auto&quot;}

## 自定义参数

自定义mbox参数必须作为XDM数据传递，并且 `sendEvent` 命令。 请务必确保XDM架构包含Target实施所需的所有字段。

at.js示例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

平台Web SDK JavaScript示例(使用 `sendEvent` 命令：

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

在标记中，首先使用 [!UICONTROL XDM对象] 要映射到XDM字段的数据元素：

![映射到XDM对象数据元素中的XDM字段](assets/params-tags-pageName.png){zoomable=&quot;yes&quot;}

然后，将 [!UICONTROL XDM对象] 在 [!UICONTROL 发送事件] [!UICONTROL 操作] (多个 [!UICONTROL XDM对象] 可以 [合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在发送事件中包含XDM对象数据元素](assets/params-tags-sendEvent.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]


>[!NOTE]
>
>因为自定义mbox参数是 `xdm` 对象，您需要使用新名称更新引用这些mbox参数的任何受众、活动或配置文件脚本。 请参阅 [为兼容Platform Web SDK更新Target受众和配置文件脚本](update-audiences.md) 页面以了解更多信息。


## 配置文件参数

必须在 `data.__adobe.target` 平台Web SDK中的对象 `sendEvent` 命令负载。

与at.js类似，所有配置文件参数也必须带有前缀 `profile.` ，以将该值正确存储为永久性Target配置文件属性。 保留 `user.categoryId` Target类别亲和度功能的参数带有前缀 `user.`.

at.js示例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

平台Web SDK示例使用 `sendEvent` 命令：

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

在标记中，首先创建一个数据元素以定义 `data.__adobe.target` 对象：

![在数据元素中定义数据对象](assets/params-tags-dataObject.png){zoomable=&quot;yes&quot;}

然后，将您的数据对象包含在 [!UICONTROL 发送事件] [!UICONTROL 操作] (多个 [!UICONTROL 对象] 可以 [合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在发送事件中包含数据对象](assets/params-tags-sendEvent-withData.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

## 实体参数

实体参数用于传递Target Recommendations的行为数据和补充目录信息。 全部 [实体参数](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) 平台Web SDK也支持at.js支持。 与配置文件参数类似，所有实体参数都应在 `data.__adobe.target` 平台Web SDK中的对象 `sendEvent` 命令负载。

特定项目的实体参数必须带有前缀 `entity.` 以获取正确的数据。 保留 `cartIds` 和 `excludedIds` recommendations算法的参数不应添加前缀，且每个算法的值必须包含以逗号分隔的实体ID列表。

at.js示例使用 `targetPageParams()`:

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

平台Web SDK示例使用 `sendEvent` 命令：

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

在标记中，首先创建一个数据元素以定义 `data.__adobe.target` 对象：

![在数据元素中定义数据对象](assets/params-tags-dataObject-entities.png){zoomable=&quot;yes&quot;}

然后，将您的数据对象包含在 [!UICONTROL 发送事件] [!UICONTROL 操作] (多个 [!UICONTROL 对象] 可以 [合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在发送事件中包含数据对象](assets/params-tags-sendEvent-withData.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

>[!NOTE]
>
>如果 `commerce` 字段组，并且 `productListItems` 阵列包含在XDM有效负载中，然后是 `SKU` 此数组中的值映射到 `entity.id` ，以增加产品视图。


## 购买参数

成功订单后，购买参数会在订单确认页面上传递，并用于Target转化和优化目标。 通过平台Web SDK实施，这些参数和会自动从作为 `commerce` 字段组。

at.js示例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

购买信息会在 `commerce` 字段组具有 `purchases.value` 设置为 `1`. 订单ID和订单总计会自动从 `order` 对象。 如果 `productListItems` 数组存在，则 `SKU` 值用于 `productPurchasedId`.

平台Web SDK示例使用 `sendEvent` 命令：

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

在标记中，首先使用 [!UICONTROL XDM对象] 要映射到XDM字段的数据元素：

![映射到XDM对象数据元素中的XDM字段](assets/params-tags-purchase.png){zoomable=&quot;yes&quot;}

然后，将 [!UICONTROL XDM对象] 在 [!UICONTROL 发送事件] [!UICONTROL 操作] (多个 [!UICONTROL XDM对象] 可以 [合并](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在发送事件中包含XDM对象数据元素](assets/params-tags-sendEvent-purchase.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]


>[!NOTE]
>
>的 `productPurchasedId` 值也可以作为以逗号分隔的实体ID列表(位于 `data` 对象。


## 客户ID(mbox3rdPartyId)

Target允许使用单个客户ID跨设备和系统同步配置文件。 使用at.js，可以将此参数设置为 `mbox3rdPartyId` 作为发送到Experience CloudIdentity Service的第一个客户ID。 与at.js不同，Platform Web SDK实施允许您指定要用作 `mbox3rdPartyId` 如果有多个。 例如，如果您的企业具有全局客户ID，并且为不同的业务线分隔了客户ID，则您可以配置Target应使用的ID。

要为Target跨设备和客户属性用例设置ID同步，需执行以下几步：

1. 创建 **[!UICONTROL 标识命名空间]** (在 **[!UICONTROL 标识]** 数据收集或平台屏幕
1. 确保 **[!UICONTROL 别名]** 在客户属性中，匹配 **[!UICONTROL 身份符号]** 的
1. 指定 **[!UICONTROL 标识符号]** 作为 **[!UICONTROL Target第三方ID命名空间]** 在数据流的Target配置中
1. 执行 `sendEvent` 命令 `identityMap` 字段组

at.js示例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

平台Web SDK示例使用 `sendEvent` 命令：

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

的 [!UICONTROL ID] 值， [!UICONTROL 已验证状态] 和 [!UICONTROL 命名空间] 在 [!UICONTROL 身份映射] 数据元素：
![捕获客户ID的身份映射数据元素](assets/params-tags-customerIdDataElement.png){zoomable=&quot;yes&quot;}

的 [!UICONTROL 身份映射] 然后，使用数据元素设置 [!UICONTROL identityMap] 字段 [!UICONTROL XDM对象] 数据元素：
![XDM对象数据元素中使用的身份映射数据元素](assets/params-tags-customerIdInXDMObject.png){zoomable=&quot;yes&quot;}

的 [!UICONTROL XDM对象] 之后， [!UICONTROL 发送事件] 规则的操作：

![在发送事件中包含XDM对象数据元素](assets/params-tags-sendEvent-xdm.png){zoomable=&quot;yes&quot;}

在您的数据流的Adobe Target服务中，确保将 [!UICONTROL Target第三方ID命名空间] 到 [!UICONTROL 身份映射] 数据元素：
![在数据流中设置Target第三方ID命名空间](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

## 平台Web SDK示例

现在，您已了解如何使用Platform Web SDK映射不同的Target参数，接下来可以将我们的两个示例页面从at.js迁移到Platform Web SDK，如下所示。 示例页面包括：

- 异步库实施的Target预隐藏代码片段
- 平台Web SDK基础代码
- 平台Web SDK JavaScript库
- A `configure` 初始化库的命令
- A `sendEvent` 命令发送数据并请求要渲染的Target内容

+++产品详细信息页面上的Web SDK:

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

+++订单确认页面上的Web SDK:

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

接下来，了解如何 [跟踪Target转化事件](track-events.md) 与平台Web SDK集成。

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
