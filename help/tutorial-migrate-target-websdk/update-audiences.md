---
title: 更新受众和配置文件脚本 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何更新Adobe Target受众和配置文件脚本，以与Experience PlatformWeb SDK兼容。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# 为兼容Platform Web SDK更新Target受众和配置文件脚本

完成技术更新以将Target迁移到Platform Web SDK后，您可能需要更新部分受众、配置文件脚本和活动以确保顺利过渡。

所有Target mbox参数都必须通过平台Web SDK实施以XDM格式传递。 在将更改发布到生产环境之前，您应：

* 更新使用mbox参数的受众
* 更新使用mbox参数的配置文件脚本
* 更新任何选件和活动时都会使用mbox参数令牌替换(例如， `${mbox.parameter_name}`)

## 调整受众

任何使用自定义mbox参数的受众都应进行更新，以使用新的XDM参数名称。 例如，的自定义参数 `page_name` 可能会被映射到 `web.webpagedetails.pageName`.

确保与at.js和Platform Web SDK兼容的一种方法是更新任何相关受众，以便 `OR` 条件，如下所示：

![如何查看更新Target受众以实现平台Web SDK兼容性](assets/target-audience-update.png)

## 编辑配置文件脚本

应更新配置文件脚本以引用新的XDM参数名称，与受众类似。 除了更改mbox参数名称之外，配置文件脚本在at.js和Platform Web SDK实施之间的工作方式也没有差异。

确保兼容性的一种方法是 `OR` 配置文件脚本代码中的条件。

配置文件脚本示例：

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

为兼容Platform Web SDK更新了配置文件脚本：

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('page.webpagedetails.pageName') =='Product Details')){
  return true
}
```

有关更多信息和最佳实践，请参阅关于 [配置文件脚本](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## 更新动态内容的参数令牌

如果您有任何选件、推荐设计或活动使用 [动态内容替换](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html)，则可能需要相应地更新它们，以考虑新的XDM参数名称。

根据您对mbox参数使用令牌替换的方式，您可能能够增强现有设置以考虑旧参数和新参数名称。 但是，在自定义JavaScript代码不可能的情况下（例如在JSON选件中），您应当在迁移完成并在生产网站上实时后创建副本并进行更新。

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
  "pageName" : "${mbox.web.webpagedetails.pageName}",
  "layoutVariation" : "grid"
}
```

如果您在迁移后选择进行调整以考虑新的XDM mbox参数名称，请确保在迁移事件期间暂停任何受影响的活动，以防止向访客显示活动错误。

接下来，了解如何 [验证Target实施](validate.md).

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).