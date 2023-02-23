---
title: 初始设置 |将Target从at.js 2.x迁移到Web SDK
description: 了解并设置实施Platform Web SDK所需的重要基础元素
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# 执行初始数据收集设置

从at.js迁移到Platform Web SDK需要初始设置，才能正确捕获Platform Web SDK的数据、特性和功能。 从 [平台Web SDK实施教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans) 必须在网站实施发生任何更改之前完成：

- [配置相应的权限](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target="_blank"} 在用于数据收集的Adobe Admin Console中
- [配置XDM架构](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} 用于将结构化数据传递到边缘网络
- [配置身份命名空间](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} 用于跨设备个性化和mbox3rdPartyId功能
- [创建数据流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} 以启用来自边缘网络的数据转发
- [配置数据流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} 启用数据转发到Adobe Target

>[!CAUTION]
>
>请记住，应当在Target、Analytics和Audience Manager迁移中协调这些设计方面。

完成初始配置后，应使用Adobe Experience Platform边缘网络启用Target功能。

接下来，了解如何 [替换at.js库并设置基本的Platform Web SDK实施](replace-library.md).

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
