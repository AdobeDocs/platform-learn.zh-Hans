---
title: 替换库 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何将Adobe Target实施从at.js 2.x迁移到Adobe Experience Platform Web SDK。 主题包括库概述、实施差异和其他值得注意的标注。
source-git-commit: 51958a425c946fc806d38209ac4b0b4fa17945e8
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 1%

---

# 将at.js库替换为Platform Web SDK

了解如何替换页面上的Adobe Target实施，以便从at.js迁移到Platform Web SDK。 基本替换包括以下步骤：

* 查看Target管理设置并记下IMS组织ID
* 将at.js库替换为Platform Web SDK
* 更新同步库实施的预隐藏代码片段
* 在页面上配置Platform Web SDK

>[!NOTE]
>
>提供的示例仅供说明之用，实际的Target实施可能会有所不同。 如果您现有的Target实施使用Adobe的数据收集标签管理器，则您还可以参阅 [平台Web SDK Target实施教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) 以了解其他信息。


## 查看Target管理设置

将Target迁移到Platform Web SDK的第一步是，在Target界面的 **[!UICONTROL 管理]** 中。

### [!UICONTROL 实施]

#### [!UICONTROL 帐户详细信息]

* **[!UICONTROL IMS组织Id]**  — 请注意此值，因为需要配置Platform Web SDK。
* **[!UICONTROL 设备内决策]**  — 平台Web SDK不支持此功能。 在迁移后以及不再在任何网站上使用at.js或者有任何服务器端用例来实施设备决策时，可以禁用此设置。

#### [!UICONTROL 实施方法]

在 **[!UICONTROL 实施方法]** 部分仅适用于at.js。 这些设置用于为您的实施生成自定义的at.js库。 查看这些设置以检查您是否具有任何自定义代码，或是否为跨域用例设置第一方和第三方Cookie。

的 **[!UICONTROL 配置文件生命周期]** 设置只能由Adobe客户关怀部门更改。 您的实施方法不会影响Target访客配置文件生命周期。 at.js和Platform Web SDK都使用相同的访客配置文件生命周期。

#### [!UICONTROL Privacy]

* **[!UICONTROL 模糊处理访客IP地址]**  — 此设置会影响地理定位功能。 at.js和Platform Web SDK都使用相同的后端IP模糊设置来进行地理定位。

### [!UICONTROL 环境]

Platform Web SDK使用数据流配置，该配置允许您明确定义 [!UICONTROL 环境ID] 用于单独的开发、暂存和生产数据流。 此配置的主要用例适用于不存在URL的移动设备应用程序实施，以便轻松区分环境。 该设置是可选的，但可用于确保所有请求都与指定的环境正确关联。 这与at.js实施的不同之处在于，在at.js实施中，您必须根据域和主机组规则来分配Target环境。

>[!NOTE]
>
>如果未在数据流配置中指定环境ID，则Target会按照 **主机** 中。

有关更多信息，请参阅 [数据流配置](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) 指南和Target [主机](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 文档。

## 部署平台Web SDK

Target功能由at.js和Platform Web SDK提供。 如果同时使用两个库，您可能会遇到渲染和跟踪问题。 要成功迁移到Platform Web SDK，第一步是删除at.js并将其替换为Platform Web SDK(alloy.js)。

假定使用at.js进行简单的Target实施：

* 页面顶部附近的数据层为Target和其他应用程序提供信息
* 一个或多个第三方帮助程序库，其功能可以在Target活动中使用（例如，jQuery）
* 用于缓解闪烁的预隐藏代码片段
* Target at.js库会使用默认设置异步加载，以自动请求和渲染活动：

+++请参阅at.js的示例HTML代码

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
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

要升级Target以使用平台Web SDK，请首先删除at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

并将替换为当前支持的Platform Web SDK(alloy.js)版本：

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

预建独立版本要求直接将“基本代码”添加到页面，该页面将创建一个名为alloy的全局函数。 使用此函数与SDK进行交互。 如果要为全局函数命名其他名称，请更改 `alloy` 名称。

>[!TIP]
>
> 使用标记功能（以前称为Launch）实施Web SDK时，会通过添加Adobe Experience Platform Web SDK扩展，将alloy.js库添加到标记库中。


请参阅 [安装平台Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=zh-Hans) 有关更多详细信息和部署选项的文档。


## 更新内容预隐藏方法

Platform Web SDK实施可能需要预隐藏代码片段，具体取决于库是异步加载还是同步加载。

### 异步实施

与at.js一样，如果异步加载Platform Web SDK库，则页面可能会在Target执行内容交换之前完成渲染。 此行为可能会导致所谓的“闪烁”，在这种情况下，会先短暂显示默认内容，然后再将其替换为Target指定的个性化内容。 如果要避免出现这种闪烁情况，Adobe建议在紧靠异步Platform Web SDK脚本引用之前的位置添加特殊的预隐藏代码片段。

如果您的实施与上面的示例类似，请将at.js预隐藏代码片段替换为与Platform Web SDK兼容的以下版本：

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

预隐藏代码片段会在页面标题中创建一个样式标记，且其中包含您选择的CSS定义。 当收到来自Target的响应或达到超时时，将删除此样式标记。

预隐藏行为由代码片段末尾的两个配置控制。

* `body { opacity: 0 !important }` 指定在Target加载之前要用于预隐藏的CSS定义。 默认情况下，会隐藏整个页面。 您可以将此定义更新为要预隐藏的选择器以及隐藏方式。 您可能包含多个定义，因为此值只是插入预隐藏样式标记中的内容。 如果您有一个封装导航下方内容的易于识别的容器元素，则可以使用此设置将预隐藏限制为该容器元素。

* `3000` 指定预隐藏的超时时间（以毫秒为单位）。 如果在超时前未收到来自Target的响应，则会删除预隐藏样式标记。 达到此超时的情况应该很少。

>[!NOTE]
>
>请务必为Platform Web SDK使用正确的代码片段，因为它使用的样式ID不同 `alloy-prehiding`. 如果使用at.js的预隐藏代码片段，则该代码片段可能无法正常工作。

### 同步实施

Adobe建议异步实施Platform Web SDK，以获得最佳的整体页面性能。 但是，如果库同步加载，则不需要预隐藏代码片段。 而是在Platform Web SDK配置中指定预隐藏样式。

同步实施的预隐藏样式可以使用 [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) 选项。 下一节将介绍平台Web SDK配置。

>[!TIP]
>
> 使用标记功能（以前称为Launch）实施Web SDK时，可以在Adobe Experience Platform Web SDK扩展配置中编辑预隐藏样式。

要进一步了解Platform Web SDK如何管理闪烁，您可以参阅指南部分：  [管理个性化体验中的闪烁](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## 配置平台Web SDK

必须在每次加载页面时配置平台Web SDK。 的 `configure` 命令必须始终是名为的第一个SDK命令。 以下示例假定在单个部署中将整个站点升级到Platform Web SDK:

>[!BEGINTABS]

>[!TAB JavaScript]

的 `edgeConfigId` 是 [!UICONTROL 数据流ID]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB 标记]

在标记实施中，许多字段会自动填充，也可以从下拉菜单中选择。 请注意，不同的平台 [!UICONTROL 沙箱] 和 [!UICONTROL 数据流] 可为每个环境选择。 数据流将根据发布过程中标记库的状态进行更改。

![配置Web SDK标记扩展](assets/tags-config.png)
>[!ENDTABS]

如果您计划逐页从at.js迁移到Platform Web SDK，则需要以下配置选项：


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB 标记]

![配置Web SDK标记扩展迁移选项](assets/tags-config-migration.png)
>[!ENDTABS]

下面概述了与Target相关的值得注意的配置选项：

| 选项 | 描述 | 示例值 |
| --- | --- | --- |
| `edgeConfigId` | 数据流ID | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | Adobe Experience Cloud组织ID | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | 使用此选项可启用Web SDK读写at.js使用的旧版mbox和mboxEdgeCluster Cookie。 这有助于您在从使用Web SDK的页面移动到使用at.js库的页面时保留访客配置文件，但方式相反。 | `true` |
| `idMigrationEnabled` | 如果为true，则SDK会读取并设置旧的AMCV Cookie。 此选项有助于过渡到使用Platform Web SDK，而网站的某些部分可能仍使用Visitor.js。 | `true` |
| `thirdPartyCookiesEnabled` | 启用Adobe第三方Cookie的设置。 SDK可以在第三方上下文中保留访客ID，以便允许在网站之间使用相同的访客ID。 如果您有多个网站，请使用此选项；但是，有时出于隐私原因不需要此选项。 | `true` |
| `prehidingStyle` | 用于创建CSS样式定义，当从服务器加载个性化内容时，该定义会隐藏网页的内容区域。 此操作仅用于SDK的同步部署。 | `body { opacity: 0 !important }` |

>[!NOTE]
>
>`thirdPartyCookiesEnabled` 可以设置为 `true` 以维护跨多个域的一致Target访客配置文件。 此选项应设置为 `false` 或忽略，除非需要多域访客配置文件持久性。

>[!TIP]
>
> 使用标记功能（以前称为Launch）实施Web SDK时，可以在Adobe Experience Platform Web SDK扩展配置中管理这些配置。

有关选项的完整列表，请参阅 [配置平台Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hans) 的双曲余切值。

## 实施示例

正确放置Platform Web SDK后，示例页面将如下所示。

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
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
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
> 使用标记功能（以前称为Launch）实施Web SDK时，标记嵌入代码会替换上面的“Platform Web SDK基本代码”、“异步加载的Platform Web SDK”和“配置Platform Web SDK”部分。

请务必注意，仅按照上面所示包含和配置Platform Web SDK库，不会执行对Adobe Edge网络的任何网络调用。

接下来，了解如何 [请求和应用基于VEC的活动](render-vec-activities.md) 到页面。

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).