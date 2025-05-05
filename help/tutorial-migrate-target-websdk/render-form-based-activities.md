---
title: 将Target从at.js 2.x迁移到Web SDK
description: 了解如何将Adobe Target实施从at.js 2.x迁移到Adobe Experience Platform Web SDK。 主题包括库概述、实施差异和其他值得注意的标注。
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# 呈现使用基于表单的编辑器的Target活动

某些Target实施可能使用区域mbox（现在称为“范围”）来交付使用基于表单的体验编辑器的活动中的内容。 如果您的at.js Target实施使用mbox，则需要执行以下操作：

* 将来自使用`getOffer()`或`getOffers()`的at.js实现的任何引用更新为等效的Platform Web SDK方法。
* 添加代码以触发`propositionDisplay`事件，从而计入展示次数。

## 按需请求和应用内容

使用Target基于表单的编辑器创建并交付到区域mbox的活动无法由Platform Web SDK自动呈现。 与at.js类似，交付给特定Target位置的选件需要按需渲染。


+++at.js使用`getOffer()`和`applyOffer()`的示例：

1. 执行`getOffer()`以请求位置的选件
1. 执行`applyOffer()`以将选件呈现给指定的选择器
1. 活动展示次数在`getOffer()`请求时自动递增

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++使用`applyPropositions`命令的Platform Web SDK等效项：

1. 执行`sendEvent`命令以请求一个或多个位置（范围）的选件（建议）
1. 使用元数据对象执行`applyPropositions`命令，元数据对象提供有关如何将内容应用于每个作用域的页面的说明
1. 执行事件类型为`decisioning.propositionDisplay`的`sendEvent`命令以跟踪展示

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": renderedPropositions
          }
        }
      }
    });
  });
});
```

+++

Platform Web SDK为使用指定了`actionType`的`applyPropositions`命令将基于表单的活动应用到页面提供了更好的控制：

| `actionType` | 描述 | at.js `applyOffer()` | 平台Web SDK `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | 清除容器的内容，然后将选件添加到容器 | 是（始终使用） | 是 |
| `replaceHtml` | 移除容器并将其替换为选件 | 否 | 是 |
| `appendHtml` | 在指定的选择器后附加选件 | 否 | 是 |

请参阅有关使用Platform Web SDK渲染内容的[专用文档](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hans)，以获取其他渲染选项和示例。

## 实施示例

下面的示例页面基于上一节中概述的实现，只是它向`sendEvent`命令添加了其他范围。

+++具有多个范围的Platform Web SDK示例

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous deployment-->
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
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
          "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
              "decisioning": {
                "propositions": renderedPropositions
              }
            }
          }
        });
      });
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

接下来，了解如何使用Platform Web SDK[传递Target参数](send-parameters.md)。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
