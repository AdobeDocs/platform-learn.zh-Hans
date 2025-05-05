---
title: 初始设置 — 将Target从at.js 2.x迁移到Web SDK
description: 了解并设置Platform Web SDK实施所需的重要基本元素
exl-id: dbf9683b-1cfc-474a-9c38-432cad4d1533
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 执行初始数据收集设置

从at.js迁移到Platform Web SDK需要进行初始设置，以启用Platform Web SDK的正确数据捕获、特性和功能。 在进行任何网站实施更改之前，必须完成[Platform Web SDK实施教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans)中的以下步骤：

- [在Adobe Admin Console中为数据收集配置适当的权限](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"}
- [配置XDM架构](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html?lang=zh-Hans){target="_blank"}以将结构化数据传递到Edge Network
- [为跨设备个性化和mbox3rdPartyId功能配置标识命名空间](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html?lang=zh-Hans){target="_blank"}
- [创建数据流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html?lang=zh-Hans){target="_blank"}以启用从Edge Network转发数据
- [配置数据流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=zh-Hans#configure-the-datastream){target="_blank"}以启用将数据转发到Adobe Target

>[!CAUTION]
>
>请记住，这些设计方面应跨Target、Analytics和Audience Manager迁移进行协调。

初始配置完成后，应使用Adobe Experience PlatformEdge Network启用Target功能。

接下来，了解如何[替换at.js库并设置基本的Platform Web SDK实施](replace-library.md)。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
