---
title: 初始设置 — 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解并设置您的Platform Web SDK实施所需的重要基本元素
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 5%

---

# 执行初始数据收集设置

从Target SDK迁移到优化SDK需要进行初始设置，才能启用优化SDK的正确数据捕获、特性和功能。 在进行任何网站实施更改之前，必须完成以下步骤：

- [在Adobe Admin Console中为数据收集配置适当的权限](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"}
- [配置XDM架构](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"}以将结构化数据传递到Edge Network
- [配置架构](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema)以接收Adobe Target数据
- [为跨设备个性化和mbox3rdPartyId功能配置标识命名空间](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"}
- [创建数据流](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"}以启用从Edge Network转发数据
- [配置数据流](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"}以启用将数据转发到Adobe Target
- [为Decisioning扩展配置Tag属性](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension)

>[!BEGINTABS]

>[!TAB 目标扩展]

使用Target扩展时安装的标记扩展：

1. Mobile Core
1. 轮廓
1. Adobe Target
1. Adobe Analytics (可选，在使用Adobe Analytics作为Adobe Target活动的报表源时需要)

使用Target扩展时安装的![标记扩展](assets/tag-extensions-target.png)


>[!TAB Decisioning扩展]

标记在使用Decisioning扩展时安装的扩展：

1. Mobile Core
1. 轮廓
1. 同意
1. 身份标识
1. Adobe Experience Platform Edge Network
1. Adobe Journey Optimizer - Decisioning
1. AEP Assurance（可选，调试所需）

使用Decisioning扩展时安装的![标记扩展](assets/tag-extensions-decisioning.png)


>[!ENDTABS]

接下来，了解如何[替换at.js库并设置基本的Platform Web SDK实施](replace-library.md)。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
