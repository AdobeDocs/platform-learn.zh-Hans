---
title: 验证Decisioning扩展实施并进行故障排除
description: 了解如何使用Decisioning扩展验证Adobe Target Mobile实施并为其排除故障。
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: a4fe85580776e5d84f6deaf3c0224f0513ba8415
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 验证Decisioning扩展实施并进行故障排除

将Target实施从Target扩展迁移到Decisioning扩展后，请务必先验证所有功能是否正常运行，然后再将任何更改发布到生产应用程序。 Adobe建议执行以下操作，本页将详细介绍这些内容：

* 执行技术验证，以确保基本实施以及Platform Mobile SDK请求和响应看起来正确
* 确保Target活动已正确交付和呈现
* 检查报表是否正常工作
* 重新访问受众和配置文件脚本，以确保它们与Platform Mobile SDK和Optimie扩展兼容
* 确保与Adobe或第三方应用程序的集成正常工作

每个Target实施都因使用的站点架构和功能而异。 您可以使用下表作为起点，并添加任何特定于您的实施的项目。

## 技术验证和故障排除

Platform Mobile SDK和Decisioning扩展的技术验证和故障排除功能在Assurance中得到了显着增强。 请参阅以下文档页面以了解此基本工具：

* [在Assurance中设置Decisioning插件](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [正在验证优化SDK设置](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [审阅请求并模拟不同的体验](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

执行上述验证步骤后，您可以放心，带有Decisioning扩展的Platform Mobile SDK实施已准备好投入生产。

恭喜，您已到达本教程的结尾！ 祝您顺利将Adobe Target实施迁移到Decisioning扩展！

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
