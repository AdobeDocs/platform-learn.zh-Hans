---
title: 启用跨域支持 — 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解如何使用Experience Platform Web SDK为跨域和移动应用程序到Web浏览器方案配置Adobe Target。
exl-id: 1dc78771-b85c-4127-8d1b-6558509f9db8
source-git-commit: 18f0190881d2a997491d4d6ce367add74cc30288
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# 启用跨域访客配置文件

Platform Web SDK支持访客ID共享功能，使客户能够在您的域中更准确地提供个性化体验。 此功能允许您跨域提供一致的个性化，并提高访客活动报告的准确性，而无需依赖第三方Cookie。

## 先决条件

要使用跨域ID共享，您必须使用Platform Web SDK版本2.11.0或更高版本。 此功能还与VisitorAPI.js版本1.7.0或更高版本兼容。

跨域ID共享的工作方式是将特殊的`adobe_mc`查询字符串参数附加到目标域的URL。 此参数用于指定访客ID，而不是生成新ID或使用现有ID。

目标域必须使用任一跨域ID共享库来处理`adobe_mc`参数并正确共享访客ID。

## 方法比较

在实施之前，请先确定现有实施是否使用`visitor.appendVisitorIDsTo()`函数。 应更新使用此函数的任何自定义代码，以使用新的`appendIdentityToUrl` Web SDK命令。

| VisitorAPI.js | Platform Web SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## 使用`appendIdentityToURL`命令

对于跨域ID共享，Web SDK版本2.11.0添加了对`appendIdentityToUrl`命令的支持。 使用此命令时，会生成`adobe_mc`查询字符串参数。

该命令接受具有一个属性`url`的对象，并返回具有属性URL的对象。

此命令不等待任何同意更新。 如果未提供同意，则返回的URL将保持不变。

如果未提供ECID，则调用`/acquire`端点以生成ECID。

以下是如何实施跨域ID共享的示例。

此代码会为页面上的所有点击添加一个事件侦听器。 如果单击位于匹配域的链接上(在本例中为adobe.com或behance.com)，则会将标识添加到URL并将用户重定向到该处。

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
>使用标记功能（以前称为Launch）实施Web SDK时，无需自定义代码即可实现跨域ID共享。 有关详细信息，请参阅[专用文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension)。

>[!NOTE]
>
>Platform Web SDK还支持在本机移动设备应用程序用例中进行移动设备到Web ID共享。 有关详细信息，请参阅有关[移动到Web和跨域ID共享](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html)的专用文档。

接下来，了解如何[更新受众和配置文件脚本](update-audiences.md)以确保与Platform Web SDK兼容。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
