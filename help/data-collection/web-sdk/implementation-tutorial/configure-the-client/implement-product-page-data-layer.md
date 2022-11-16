---
title: 在产品页面上实施数据层
description: 在产品页面上实施数据层
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 在产品页面上实施数据层

在本教程中，您将为典型的电子商务网站实施Adobe客户端数据层。 如果您尚未执行此操作，请阅读 [如何使用Adobe客户端数据层](how-to-use-the-adobe-client-data-layer.md) 首先了解Adobe客户端数据层的操作方式。

假设用户浏览您的产品并点击泡沫辊以了解更多信息。 用户登陆泡沫辊产品详细信息页面。

以下是您的简单产品详细信息页面的HTML:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

如您所注意， `<head>` 标记存在 `<script>` 标记。 您将在此处放置JavaScript代码。 不必将 `<script>` 标记 `<head>`，但是尽快将数据推送到数据层有助于确保营销人员在用户离开页面之前可以快速将数据发送到Adobe Experience Platform。

内部 `<script>` 标记，您首先会创建 `adobeDataLayer` 数组，然后将相应的事件和数据信息推送到数组中。 数据符合XDM架构 [您之前创建的](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

在此示例中，您向数据层进行了两次推动，每次推动都包含 `event` 键。 包括 `event` 键不仅可告知页面上发生了什么事件，而且使营销人员在Adobe Experience Platform标记中创建适当规则更加简单。

首次向数据层推送消息会通知侦听器（标记规则）用户已查看页面。 它还会将页面名称和网站区域添加到数据层。

第二次向数据层推送时，会通知侦听器（标记规则）用户已查看产品。 它还会将产品信息添加到数据层。

## 添加到购物车

您可能还希望跟踪用户在 [!UICONTROL 添加到购物车] 按钮。

为此，请创建一个在用户单击 [!UICONTROL 添加到购物车] 按钮。

```js
window.onAddToCartClick = function() {
  // In a real implementation, you would change this condition to 
  // only pass if a cart doesn't already exist. You would typically 
  // do this by checking a cookie or variable value.
  if (true) {
    window.adobeDataLayer.push({
      "event": "cartOpened",
    });
  }
  window.adobeDataLayer.push({
    "event": "productAddedToCart"
  });
};
```

调用此函数时，首先会检查用户是否已存在购物车。 通常，可通过检查特定Cookie或变量是否存在来完成此操作。 如果购物车不存在，您将推送 `cartOpened` 事件。 随后，您将 `productAddedToCart` 事件。 产品信息已在数据层中存在，因此无需再次添加。

添加 `onclick` 属性 [!UICONTROL 添加到购物车] 按钮 `onAddToCartClick` 函数。

HTML页面的结果应如下所示：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## 下载应用程序

最后要执行的一项操作是跟踪用户何时单击 _[!UICONTROL 下载应用程序]_ 链接。

为此，请创建一个在用户单击 _[!UICONTROL 下载应用程序]_ 链接。

```js
window.onDownloadAppClick = function(event) {
  window.adobeDataLayer.push({
    "event": "downloadAppClicked",
    "eventInfo": {
      "web": {
        "webInteraction": {
          "URL": "https://example.com/download",
          "name": "App Download",
          "type": "download"
        }
      }
    }
  });
};
```

在这种情况下，有关链接的信息将封装在 `eventInfo` 键。 如 [如何使用Adobe客户端数据层](how-to-use-the-adobe-client-data-layer.md)，这会告知数据层将此数据与事件一起通信，但是 _not_ 在数据层中保留数据。 对于链接点击，将有关已点击链接的信息添加到数据层将没有用处，因为它与整个页面无关，也不适用于可能发生的其他事件。

添加 `onclick` 属性 [!UICONTROL 下载应用程序] 调用新 `onDownloadAppClick` 函数。

HTML页面的结果应如下所示：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
        window.adobeDataLayer.push({
          "event": "downloadAppClicked",
          "eventInfo": {
            "web": {
              "webInteraction": {
                "URL": "https://example.com/download",
                "name": "App Download",
                "type": "download"
              }
            }
          }
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
