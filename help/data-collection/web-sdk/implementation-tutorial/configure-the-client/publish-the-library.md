---
title: 发布库
description: 发布库
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2fc072df-24f2-4fea-848f-0a973deca2f8
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 4%

---

# 发布库

现在可以将标记库部署到您的网站上。

## 创建库

首先，您必须创建一个库，其中包含已创建的扩展、规则和数据元素。 要创建库，请选择 [!UICONTROL 发布流] 在左侧菜单中。

选择 [!UICONTROL 添加库].

您应会看到库创建视图。

![标记库创建](../../../assets/implementation-strategy/tags-library-creation.png)

为库命名，例如 _演示_. 选择 [!UICONTROL 开发] 在 [!UICONTROL 环境] 下拉菜单。 然后单击 [!UICONTROL 添加所有更改的资源].

现在，您应会看到所有扩展、规则和数据元素都列在下 [!UICONTROL 资源更改]. 单击 [!UICONTROL 保存并构建到开发环境].

## 将嵌入代码添加到HTML

现在，您必须向产品页面HTML添加脚本标记，以加载新构建的标记库。

首先，单击 [!UICONTROL 环境] 在左侧菜单中。 您应该会看到列出的三个不同的环境。

![标记环境](../../../assets/implementation-strategy/tags-environments.png)

单击上的包图标 [!UICONTROL 开发] 环境行。 您应会看到有关将Launch库脚本安装到页面上的说明。

![标记安装说明](../../../assets/implementation-strategy/tags-installation-instructions.png)

复制脚本标记（为方便起见，提供了一个复制到剪贴板按钮）。 打开您的产品页面HTML，并将脚本标记插入到 `</head>` 标记之前。 最终HTML应如下所示：

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
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

查看 [发布标记文档](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) 如果您想了解有关发布过程的更多信息。

接下来，您将测试新实施！
