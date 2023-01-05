---
title: 启用跨域支持 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Web SDK将Adobe Target配置为跨域和移动设备应用程序到Web浏览器方案。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 启用跨域访客配置文件

Platform Web SDK支持访客ID共享功能，这些功能使客户能够在您的域中更准确地提供个性化体验。 此功能允许您跨域提供一致的个性化，并增强访客活动报表的准确性，而无需依赖第三方Cookie。

## 先决条件

要使用跨域ID共享，您必须使用Platform Web SDK版本2.11.0或更高版本。 此功能还与VisitorAPI.js版本1.7.0或更高版本兼容。

跨域ID共享通过附加一个特殊的 `adobe_mc` 查询字符串参数。 此参数用于指定访客ID，而不是生成新ID或使用现有ID。

目标域必须使用其中任一库进行跨域ID共享，才能处理 `adobe_mc` 参数并正确共享访客ID。

## 方法比较

在实施之前，请首先确定您的现有实施是否使用 `visitor.appendVisitorIDsTo()` 函数。 使用此函数的任何自定义代码都应更新，以使用新 `appendIdentityToUrl` Web SDK命令。

| VisitorAPI.js | 平台Web SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## 使用 `appendIdentityToURL` 命令

对于跨域ID共享，Web SDK版本2.11.0增加了对 `appendIdentityToUrl` 命令。 使用时，此命令会生成 `adobe_mc` 查询字符串参数。

该命令接受具有一个属性的对象， `url`，并返回具有属性url的对象。

此命令不会等待任何同意更新。 如果未提供同意，则返回的URL将保持不变。

如果未提供ECID，则 `/acquire` 端点被调用以生成ECID。

以下是如何实施跨域ID共享的示例。

此代码会为页面上的所有点击添加事件侦听器。 如果点击指向匹配域的链接，则在此示例中为adobe.com或behance.com，它会将标识添加到URL并将用户重定向到该URL。

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>使用标记功能（以前称为Launch）实施Web SDK时，无需自定义代码，即可实现跨域ID共享。 请参阅 [专用文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) 以了解更多详细信息。

>[!NOTE]
>
>Platform Web SDK还支持在本机移动设备应用程序用例中进行移动到Web ID共享。 有关更多信息，请参阅关于 [移动到Web和跨域ID共享](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

接下来，了解如何 [更新受众和配置文件脚本](update-audiences.md) 以确保与平台Web SDK兼容。

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).