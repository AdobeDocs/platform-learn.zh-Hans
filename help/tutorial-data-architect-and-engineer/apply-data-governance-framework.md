---
title: 应用数据治理框架
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 应用数据治理框架
description: 在本课程中，您会将数据管理框架应用到已摄取到沙盒中的数据。
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# 应用数据治理框架

<!--15min-->

在本课程中，您会将数据管理框架应用到已摄取到沙盒中的数据。

Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。 它在各个级别的Experience Platform中发挥着关键作用，包括控制数据的使用。

在开始练习之前，请观看这些关于数据管理的简短视频：
>[!VIDEO](https://video.tv.adobe.com/v/36653?learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## 业务方案

Luma向其忠诚度计划的成员承诺，忠诚度数据不会与任何第三方共享。 我们将在课程的其余部分实施此方案。

## 应用数据管理标签

数据管理流程的第一步是将管理标签应用于您的数据。 在执行此操作之前，让我们快速了解一下哪些标签可用：

1. 在平台用户界面中，选择 **[!UICONTROL 策略]** 在左侧导航中
1. 转到 **[!UICONTROL 标签]** 选项卡，以查看帐户中的所有标签。

现在提供了许多现成的标签，此外，您还可以通过 [!UICONTROL 创建标签] 按钮。 有三种主要类型： [!UICONTROL 合同标签]， [!UICONTROL 身份标签]、和 [!UICONTROL 敏感标签] 对应于可能限制数据常见原因。 每个标签都有一个 [!UICONTROL 友好名称] 和短整数 [!UICONTROL 名称] 这只是类型和数字的缩写。 例如， [!DNL C1] 标签用于“无第三方导出”，这正是我们的忠诚度政策所需的内容。

![“数据管理”标签](assets/governance-policies.png)

现在该标记要限制其使用的数据了：

1. 在平台用户界面中，选择 **[!UICONTROL 数据集]** 在左侧导航中
1. 打开 `Luma Loyalty Dataset`
1. 转到 **[!UICONTROL 数据管理]** 选项卡
1. 您可以将标签应用于单个字段或将其应用于整个数据集。 我们会将标签应用于整个数据集。 单击铅笔图标。 如果未看到图标，请尝试使浏览器变宽或向右滚动中间面板。
   ![数据管理](assets/governance-dataset.png)
1. 在该模式中，展开 **[!UICONTROL 合同标签]** 部分并检查 **[!UICONTROL C2]** 标签
1. 选择 **[!UICONTROL 保存更改]** 按钮
   ![数据管理](assets/governance-applyLabel.png)
1. 返回主页面 [!UICONTROL 数据管理] 屏幕，带有 **[!UICONTROL 显示继承的标签]** 启用切换后，您可以看到标签已应用于数据集中的所有字段的方式。
   ![数据管理](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## 创建数据治理策略

现在，我们的数据已标记，我们可以创建一个策略。

1. 在平台用户界面中，选择 **[!UICONTROL 策略]** 在左侧导航中
1. 在“浏览”选项卡上，已经有名为“第三方导出限制”的开箱即用策略，该策略将C2标签与营销操作相关联 [!UICONTROL 导出到第三方]正是我们需要的！
1. 选择策略，然后通过 **[!UICONTROL 策略状态]** 切换
   ![数据管理](assets/governance-enablePolicy.png)

您可以通过选择 **[!UICONTROL 创建策略]** 按钮。 这将打开一个向导，通过该向导可组合多个标签和营销操作限制。

## 强制实施治理策略

执行治理政策显然是该框架的一个关键组成部分。 当数据被激活并从Platform中发送时，将会在下游强制执行，尤其是当您使用Real-time Customer Data Platform时，您可能正在授权也可能不授权。 无论如何，它都不在本教程的涵盖范围内。 但您不会手忙脚乱，您可以在这段视频中了解更多如何实施策略，我已排队观看相关部分。 它还会向您显示违反策略时会发生什么情况。

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## 其他资源

* [“数据管理”文档](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)
* [数据集服务API参考](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [治理策略服务API参考](https://www.adobe.io/experience-platform-apis/references/policy-service/)

现在，让我们转到 [查询服务](run-queries.md).
