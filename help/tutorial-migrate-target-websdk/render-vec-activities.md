---
title: 渲染VEC活动 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何通过Adobe Target的Web SDK实施来检索和应用可视化体验编辑器活动。
feature: Visual Experience Composer (VEC),Implement Client-side,APIs/SDKs,at.js,AEP Web SDK, Web SDK,Implementation
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 8%

---

# 呈现Adobe Target可视化体验编辑器(VEC)活动

Target活动是使用可视化体验编辑器(VEC)或基于表单的编辑器来设置的。 平台Web SDK可以像at.js一样，检索基于VEC的活动并将其应用到页面。 对于迁移的这一部分，您将：

* 如有需要，请安装Visual Editing Helper浏览器扩展
* 执行 `sendEvent` 使用Platform Web SDK调用以请求活动。
* 更新来自您的at.js实施的任何引用，这些引用使用 `getOffers()` 执行目标 `pageLoad` 请求。

## Visual Editing Helper浏览器扩展

借助适用于Google Chrome的Adobe Experience Cloud可视化编辑助手浏览器扩展，您可以在Adobe Target可视化体验编辑器(VEC)内可靠地加载网站，以快速创作和QA Web体验。

可视化编辑助手浏览器扩展可以与使用at.js或Platform Web SDK的网站配合使用。

>[!IMPORTANT]
>
>新的Visual Editing Helper扩展取代了 [Target VEC助手浏览器扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). 如果安装了旧版VEC助手扩展，则在使用可视化编辑助手扩展之前，应删除或禁用该扩展。

### 获取并安装可视化编辑助手

1. 导航到 [Adobe Experience Cloud Chrome网上应用店中的Visual Editing Helper浏览器扩展](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. 单击添加到 **铬黄** > **添加扩展**.
1. 在Target中打开VEC。
1. 要使用该扩展，请单击Visual Editing Helper浏览器扩展图标 ![“可视化编辑扩展”图标](assets/VEC-Helper.png) 在VEC或QA模式下，在Chrome浏览器的工具栏中显示。

当在目标 Target 中打开网站以进行创作时，会自动启用可视化编辑帮助程序。该扩展不具有任何有条件的设置。该扩展会自动处理所有设置，包括 SameSite cookie 设置。

有关 [Visual Editing Helper扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) 和 [可视化体验编辑器故障诊断](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

## 自动请求和应用内容

在页面上配置Platform Web SDK后，您可以从Target请求内容。 与at.js不同，Platform Web SDK要求您明确执行命令，at.js可配置为在库加载时自动请求内容。

如果您的at.js实施具有 `pageLoadEnabled` 设置为 `true` 这样可以自动渲染基于VEC的活动，然后您将执行以下操作 `sendEvent` 命令：

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TIP]
>
> 使用标记功能（以前称为Launch）实施Web SDK时，可以在规则中使用 [!UICONTROL 发送事件] 包含的操作类型 [!UICONTROL 呈现可视化个性化决策] 选项。

当平台Web SDK向页面呈现活动时， `renderDecisions` 设置为 `true`，则会自动触发额外的通知调用以增加展示次数并将访客归因于活动。 此调用使用具有值的事件类型 `decisioning.propositionDisplay`.

![平台Web SDK调用会增加Target展示次数](assets/target-impression-call.png)

## 按需请求和应用内容

某些Target at.js实施可能具有 `pageLoadEnabled` 设置为 `false` 而是使用 `getOffers()` 执行函数 `pageLoad` 请求。 如果您的实施需要对 `getOffers()` 响应，然后再将内容应用到页面或在一次调用中请求多个位置的内容。

以下代码使用 `getOffers()` 和 `applyOffers()` 以根据需要应用基于VEC的活动，而不是在库加载时自动应用。

```JavaScript
adobe.target.getOffers({
  request: {
    execute: {
      pageLoad: {}
    }
  }
}).
then(response => adobe.target.applyOffers({ response: response }));
```

平台Web SDK没有特定的 `pageLoad` 事件。 所有对Target内容的请求都通过 `decisionScopes` 选项 `sendEvent` 命令。 的 `__view__` 范围的目的 `pageLoad` 请求。 等效的平台Web SDK `sendEvent` 方法是：

1. 执行 `sendEvent` 命令，其中包括 `__view__` 决策范围
1. 将返回的内容应用到具有 `applyPropositions` 命令
1. 执行 `sendEvent` 命令 `decisioning.propositionDisplay` 用于增加展示次数的事件类型和建议详细信息

```Javascript
alloy("sendEvent", {
  // Request the special "__view__" scope for target-global-mbox / pageLoad
  decisionScopes: ["__view__"]
}).then(function(result) {
  // Check if content (propositions) were returned
  if (result.propositions) {
    var retrievedPropositions = result.propositions;
    // Apply propositions to the page
    return alloy("applyPropositions", {
      propositions: retrievedPropositions
    }).then(function(applyPropositionsResult) {
      var renderedPropositions = applyPropositionsResult.propositions;
      // Send a display notification with the sendEvent command
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
  }
});
```

>[!NOTE]
>
>可以 [手动渲染修改](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) 在可视化体验编辑器中创建。 手动渲染基于VEC的修改并不常见。 检查您的at.js实施是否使用 `getOffers()` 手动执行Target的函数 `pageLoad` 请求而不使用 `applyOffers()` 以将内容应用到页面。

Platform Web SDK为开发人员提供了在请求和渲染内容方面的极大灵活性。 请参阅 [有关渲染个性化内容的详细文档](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) 以了解其他选项和详细信息。

## 实施示例

基础平台Web SDK实施现已完成。 我们启用了自动Target内容渲染的基本示例页面应当如下所示：

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
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    
    // Send an event to the Adobe edge network and render Target content automatically 
    alloy("sendEvent", {
      "renderDecisions": true
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

>[!TIP]
>
> 使用标记功能（以前称为Launch）实施Web SDK时，标记嵌入代码会替换上面的“Platform Web SDK基本代码”、“异步加载的Platform Web SDK”和“配置Platform Web SDK”部分。 在规则中使用 [!UICONTROL 发送事件] 包含的操作类型 [!UICONTROL 呈现可视化个性化决策] 选项。

## 使用可视化编辑助手浏览器扩展构建活动

借助适用于Google Chrome的Adobe Experience Cloud可视化编辑助手浏览器扩展，您可以在Adobe Target可视化体验编辑器(VEC)内可靠地加载网站，以快速创作和QA Web体验。

可视化编辑助手浏览器扩展可以与使用at.js或Platform Web SDK的网站配合使用。

>[!IMPORTANT]
>
>新的Visual Editing Helper扩展取代了 [Target VEC助手浏览器扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). 如果安装了旧版VEC助手扩展，则在使用可视化编辑助手扩展之前，应删除或禁用该扩展。

### 获取并安装可视化编辑助手

1. 导航到 [Adobe Experience Cloud Chrome网上应用店中的Visual Editing Helper浏览器扩展](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. 单击添加到 **铬黄** > **添加扩展**.
1. 在Target中打开VEC。
1. 要使用扩展，请在 VEC 或 QA 模式下，单击 Chrome 浏览器工具栏中的可视化编辑帮助程序浏览器扩展图标（可视化编辑扩展图标）。

当在Target VEC中打开网站以支持创作时，会自动启用可视化编辑助手。 该扩展不具有任何有条件的设置。该扩展会自动处理所有设置，包括 SameSite cookie 设置。

有关 [Visual Editing Helper扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) 和 [可视化体验编辑器故障诊断](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

接下来，了解如何请求和 [渲染基于表单的Target活动](render-form-based-activities.md).

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
