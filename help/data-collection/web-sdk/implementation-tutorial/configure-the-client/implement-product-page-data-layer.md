---
title: 在产品页面上实施数据层
description: 在产品页面上实施数据层
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 在产品页面上实施数据层

在本教程中，您将为典型的电子商务网站实施Adobe客户端数据层。 如果您尚未这样做，请阅读 [如何使用Adobe客户端数据层](how-to-use-the-adobe-client-data-layer.md) 首先了解Adobe客户端数据层的运行方式。

假设用户浏览您的产品并单击泡沫辊以了解详情。 用户登陆泡沫辊产品详细信息页面。

以下是您的简单产品详细信息页面的HTML：

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

正如你所注意到的那样 `<head>` 标记有一个 `<script>` 标记之前。 您将在此处放置JavaScript代码。 无需放置 `<script>` 标记范围 `<head>`，但尽快将数据推送到数据层有助于确保营销人员在用户离开页面之前可以快速将数据发送到Adobe Experience Platform。

内部 `<script>` 标记之前，请先创建 `adobeDataLayer` 数组，然后将相应的事件和数据信息推入数组。 数据符合XDM架构 [您之前已创建](../configure-the-server/create-a-schema.md).

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

在本例中，您向数据层进行了两次推送，每次都包含 `event` 键。 包括 `event` key不仅可以传达页面上发生了什么事件，而且还可以简化营销人员在Adobe Experience Platform Tags中创建相应规则的过程。

第一次推送到数据层会通知侦听器（标记规则）用户已查看页面。 它还会将页面名称和网站区域添加到数据层。

第二次推送到数据层会通知侦听器（标记规则）用户已查看产品。 它还会将产品信息添加到数据层。

## 添加到购物车

您可能还希望跟踪用户何时单击 [!UICONTROL 添加到购物车] 按钮。

要实现此目的，请创建一个在用户单击 [!UICONTROL 添加到购物车] 按钮。

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

调用此函数时，将首先检查某个用户是否已存在购物车。 通常，可以通过检查特定Cookie或变量是否存在来完成此操作。 如果购物车不存在，您将推送 `cartOpened` 事件移入数据层。 随后，您将 `productAddedToCart` 事件移入数据层。 产品信息已存在于Data Layer中，因此您无需再次添加。

添加 `onclick` 归因于 [!UICONTROL 添加到购物车] 用于调用您的新的 `onAddToCartClick` 函数。

HTML页的结果应如下所示：

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

最后要做的一件事是跟踪用户何时单击 _[!UICONTROL 下载应用程序]_ 链接。

要实现此目的，请创建一个在用户单击 _[!UICONTROL 下载应用程序]_ 链接。

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

在这种情况下，有关链接的信息将封装在 `eventInfo` 键。 如中所述 [如何使用Adobe客户端数据层](how-to-use-the-adobe-client-data-layer.md)，这会告知数据层将此数据与事件进行通信，但 _非_ 将数据保留在数据层中。 对于链接点击，将有关已点击链接的信息添加到数据层没有用处，因为它与页面整体无关，并且不适用于可能发生的其他事件。

添加 `onclick` 归因于 [!UICONTROL 下载应用程序] 调用您的新的 `onDownloadAppClick` 函数。

HTML页的结果应如下所示：

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
