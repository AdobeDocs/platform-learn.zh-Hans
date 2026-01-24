---
title: 更新受众和配置文件脚本 — 将Target从at.js 2.x迁移到Web SDK
description: 了解如何更新Adobe Target受众和配置文件脚本，以便与Experience PlatformWeb SDK兼容。
exl-id: 2c0f85f7-6e8c-4d0b-8ed5-53897d06e563
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 更新Target受众和配置文件脚本以确保Platform Web SDK兼容性

完成将Target迁移到Platform Web SDK的技术更新后，您可能需要更新某些受众、配置文件脚本和活动以确保顺利过渡。

必须在Platform Web SDK实施中以XDM格式传递所有Target mbox参数。 在将更改发布到生产环境之前，您应：

* 更新使用mbox参数的受众
* 更新使用mbox参数的配置文件脚本
* 更新任何选件和活动可使用mbox参数令牌替换（例如，`${mbox.parameter_name}`）

## 调整受众

应更新任何使用自定义mbox参数的受众，以使用新的XDM参数名称。 例如，`page_name`的自定义参数可能会映射到`web.webpagedetails.pageName`。

一种确保与at.js和Platform Web SDK兼容的方法是更新任何相关的受众，以便使用`OR`条件，如下所示：

![如何查看更新Platform Web SDK兼容性的目标受众](assets/target-audience-update.png){zoomable="yes"}

## 编辑配置文件脚本

应更新配置文件脚本以引用新的XDM参数名称，与受众类似。 除了mbox参数名称发生更改之外，at.js与Platform Web SDK实施之间配置文件脚本的工作方式也没有区别。

一种确保兼容性的方法是在配置文件脚本代码中使用`OR`条件。

示例配置文件脚本：

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

更新了用于Platform Web SDK兼容性的配置文件脚本：

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

有关更多信息和最佳实践，请参阅有关[配置文件脚本](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=zh-Hans)的专用文档。

## 更新动态内容的参数令牌

如果您有任何使用[动态内容替换](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html?lang=zh-Hans)的选件、推荐设计或活动，则可能需要对其进行相应更新以考虑新的XDM参数名称。

根据您使用令牌替换mbox参数的方式，您可以增强现有设置以考虑旧参数名和新参数名。 但是，在无法自定义JavaScript代码的情况下（例如在JSON选件中），您应在迁移完成并在生产网站上处于活动状态之后创建副本并进行更新。

JSON选件示例：

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

使用Platform Web SDK参数名称的JSON选件示例：

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

如果您选择在迁移后进行调整以考虑新的XDM mbox参数名称，请确保在迁移事件期间暂停任何受影响的活动，以防止活动向访客显示错误。

接下来，了解如何[验证Target实施](validate.md)。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=zh-Hans#M463)中发帖让我们知道。
