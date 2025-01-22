---
title: 使用标记将Adobe Analytics迁移到Web SDK
description: 了解在迁移到Web SDK过程中您将采取的步骤，以及在此过程中需要做出的决策。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: 10982e1d5fa61d2f13ec7686f251a4c7cf6a3565
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# 使用标记将Adobe Analytics迁移到Web SDK

了解使用Tags中的Analytics扩展（以前称为Launch）将Adobe Analytics实施迁移到Web SDK的步骤，还可使用Experience Platform中的Web SDK扩展。 在Tags中使用Adobe Analytics扩展时，幕后使用的是“AppMeasurement.js”代码。 因此，您可以将此视为一个将AppMeasurement迁移到Web SDK的教程，但本教程将完全包含在Tags中，并且不包含从JavaScript实施迁移或迁移的过程(在Tags UI中使用的JavaScript代码除外)。 有关迁移JavaScript实施的信息，请参阅[文档](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)。

## 从本教程中学到什么

在我们开始迁移Analytics实施的步骤之前，请务必了解您要执行的操作，即更改/更新Analytics的&#x200B;_实施_。 在本教程的末尾，当您进入您的报告时，当一切都相同时，您可能会问自己，“现在，我为什么要做所有这些事情？” 还有其他文档概述了将Web SDK用于Analytics实施的好处，但以下是几个：

1. 支持第一方设备ID
1. 更好的性能
1. 随着您逐步使用Adobe Experience Platform应用程序（启用新用例），对您的实施进行未来验证

请联系Adobe Analytics代表以了解有关Web SDK如何帮助您的更多信息。 在继续本教程时，我们将重点介绍&#x200B;_如何进行_&#x200B;迁移。

>[!IMPORTANT]
>
>请务必注意，执行此次实施迁移的主要原因之一是准备使用Adobe Experience Platform应用程序，如Customer Journey Analytics、Real-Time CDP或Journey Optimizer(如上#3所述)。 为此，使用您的网站数据将包括本教程中未包含的其他步骤，但本教程无疑将是进一步实施的前提条件。 因此，请先完成本教程，然后您可以继续执行必要的步骤，将此相同的网站数据也发送到Experience Platform。

## 迁移方法

也许有很多方法可以完成此迁移过程，但我们需要在此谈一谈以下两点：

**方法1：**&#x200B;将现有Tags属性更新为Web SDK，创建新数据元素，并对属性中已存在的规则进行更改。

**方法2：**&#x200B;您还可以创建新资产（通过复制现有资产或创建一个全新的资产），然后使用Web SDK而不是Adobe Analytics扩展配置该新资产。

**在本迁移教程中，我们将使用方法1。**&#x200B;这样，与资产关联的嵌入代码便已嵌入到您的开发、暂存和生产站点中，因此无需更改任何嵌入代码。 如果您决定使用方法2，请不要忘记从新资产的&#x200B;**Environments**&#x200B;部分获取每个环境的新嵌入代码，并将其放入网站的head部分。

>[!NOTE]
>
>即使我们只打算在此迁移期间编辑Tags中的现有资产，但最好还是要谨慎。 因此，强烈建议您在开始迁移之前复制当前资产。 这样，您始终可以进入副本，查看内容在更改之前的状态，从中提取代码等。
>小心就是好，以防万一。 请继续并制作资产的副本。 我会在这里等到你回来。

## 将Analytics实施迁移到Web SDK的步骤

在逐步执行这些步骤时，需要了解以下一些重要的注意事项：

1. 首先，您可能需要，也可能不需要所有这些步骤。 例如，有一节关于迁移自定义代码的课程。 如果您的Tags实施不使用自定义代码（包括使用插件），则您无需学习本课程。 我们尝试加入大多数人所需的课程，因此请至少通读这些课程，查看在迁移期间是否需要调整您的网站。
1. 此外，我们根本无法创建涵盖所有人正在使用的全部用例的迁移教程。 如前一项所述，我们试图列入大多数人需要的经验教训，这将涵盖大多数主要用例。 但是，毫无疑问，本教程中未介绍一些用例。 在这种情况下，请查看包含的课程能否让您很好地了解应如何针对用例进行迁移。 您还可以向[Experience League社区的同事询问数据收集](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community)。

迁移过程涉及以下关键步骤：

1. 创建迁移验证报表包。
1. 创建和配置数据流。
1. 在标记中添加和配置Web SDK扩展(以前称为AdobeLaunch)。
1. 创建新数据元素以通过Web SDK发送数据。
1. 迁移默认页面加载规则以使用Web SDK数据元素和操作。
1. 迁移规则或插件中的自定义代码。
1. Publish会更改您的实施。
1. 了解如何调试和验证更改，以及验证默认页面加载规则及其关联的变量。 然后，此验证将在迁移过程中在您进行更改时继续。
1. 迁移其他页面加载规则。
1. 迁移自定义链接规则。
1. 经过完全验证后，将删除对Analytics扩展的引用，并删除该扩展本身。
1. 完成所有更改后，将库推送到暂存环境，然后再推送到生产环境。
1. 完成所有操作后，请再次测试。 此操作是必需的，因为您通过删除对旧Analytics代码的引用进行了更改，并且希望确保一切仍然正常运行。

>[!NOTE]
>
>我们致力于帮助您成功将Analytics迁移到Web SDK。 如果您在迁移时遇到障碍或觉得本指南中缺少重要信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-analytics-to-web-sdk-using/m-p/732308#M604){target="_blank"}中发帖让我们知道。
