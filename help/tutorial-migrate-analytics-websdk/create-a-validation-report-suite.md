---
title: 创建验证报表包
description: 在Adobe Analytics中创建一个报表包，以便在从旧实施迁移网站时使用该报表包验证Web SDK数据。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16756
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# 创建验证报表包

在Adobe Analytics中创建一个报表包，以便在从旧实施迁移网站时使用该报表包验证Web SDK数据。

根据Analytics实施的大小和复杂性，迁移到Web SDK可能需要一些时间。 在此期间，您需要验证自己的工作，确保数据正确流入Adobe Analytics报表。 最佳做法是创建一个全新的报表包，您可以将其用于此迁移，而不是将这些数据与生产数据一起推送到报表包中，甚至推送到任何其他开发数据中。 在下一个课程中，我们将为开发、暂存和生产创建和配置新的“数据流”。 执行此操作时，我们需要知道配置的报表包ID。

## 创建新报表包

1. 打开Adobe Analytics并导航到Admin Console中的&#x200B;**报表包**&#x200B;设置

   ![Admin Console](assets/aa-admin-console.jpg)。

1. 选择&#x200B;**[!UICONTROL 添加报表包]**

   ![添加报表包](assets/add-report-suite.jpg)

1. 填写表单以创建新报表包。 虽然您可以选择从模板创建新报表包，即使是一个空白模板，但是最好选择&#x200B;**复制现有报表包**&#x200B;选项，然后选择要迁移到Web SDK的报表包。 这将允许您拥有与测试新迁移数据相同的名称和设置，从而使您在进行验证时更加容易。 填写所有必填字段，并保存新的迁移开发报表包。

   ![新的迁移开发报表包](assets/new-websdk-validation-report-suite.jpg)

1. 记下新报表包的ID，当您为Web SDK实施设置数据流时，将在下一课程中需要此ID。 网站标题也请务必记住，因为您可以在Analysis Workspace中使用它在Analytics项目中选择迁移开发报表包。

>[!TIP]
>
>有关创建报表包的视频演练，请参阅[了解和创建报表包](https://experienceleague.adobe.com/zh-hans/docs/analytics-learn/tutorials/intro-to-analytics/analytics-basics/understanding-and-creating-report-suites){target="_blank"}。

