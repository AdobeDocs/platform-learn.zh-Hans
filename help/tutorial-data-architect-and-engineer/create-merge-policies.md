---
title: 创建合并策略
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建合并策略
description: 在本课程中，您将创建合并策略以确定数据合并到用户档案中的方式。
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# 创建合并策略

<!--20 min-->

在本课程中，您将创建合并策略以优先考虑如何将多个数据源合并到配置文件中。

通过Adobe Experience Platform，您可以将来自多个来源的数据整合在一起，并将这些数据合并起来以查看每个客户的完整视图。 在汇总此数据时，合并策略将确定数据的优先顺序以及合并哪些数据以创建该统一视图。

在本课程中，我们将坚持使用用户界面，但也可以使用API选项创建合并策略。

**数据架构师** 将需要在本教程之外创建合并策略。

在开始练习之前，请观看此简短视频，了解有关合并策略的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## 所需的权限

在 [配置权限](configure-permissions.md) 在本课程中，您将设置完成本课程所需的所有访问控制。

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 关于合并策略和合并架构

您可能还记得，在关于批量摄取的课程中，我们为同一客户上传了两条信息稍有不同的记录。 在 [!DNL Loyalty] 数据，客户的名字是 `Daniel` 他住在 `New York City`，但在CRM数据中，客户的名字却是 `Danny` 他住在 `Portland`. 客户数据会随着时间的推移而改变。 也许他搬走了 `Portland` 到 `New York City`. 其他条件也会改变，例如电话号码和电子邮件地址。 当两个数据源为同一用户提供不同的信息时，合并策略可帮助您确定如何处理这些类型的冲突。

那么，为什么会 `Danny` 以名字取胜吗？ 我们来看一下：

1. 在Platform用户界面中，选择 **[!UICONTROL 配置文件]** 在左侧导航中
1. 转到 **[!UICONTROL 合并策略]** 选项卡
1. 默认合并策略按时间戳排序。 由于您在会员数据后上传CRM数据， `Danny` 作为名字在个人资料中胜出：

![“合并策略”屏幕](assets/mergepolicies-default.png)

为配置文件启用多个架构时， [!UICONTROL 合并架构] 自动为所有启用了配置文件的记录架构创建，记录架构共享基类。 您可以查看 [!UICONTROL 合并架构] 通过转到 **[!UICONTROL 合并架构]** 选项卡。

![“合并策略”屏幕](assets/mergepolicies-unionSchema.png)

请注意，ExperienceEvent类没有合并架构。 虽然ExperienceEvent数据仍然位于配置文件中（因为它基于时间序列），但每个事件都包含一个时间戳和ID，因此不存在冲突。

现在，如果您不喜欢该默认合并策略，该怎么办？ 如果Luma决定在发生冲突时，他们的CRM系统应该成为事实来源，该怎么办？ 为此，我们将创建一个合并策略。

## 在UI中创建合并策略

1. 在合并策略屏幕上，选择 **[!UICONTROL 创建合并策略]** 按钮
1. 作为 **[!UICONTROL 名称]**，输入 `Loyalty Prioritized`
1. 作为 **[!UICONTROL 架构]**，选择 **[!UICONTROL XDM配置文件]** （请注意，由于自定义类是记录数据，因此也可用于合并策略）
1. 对象 **[!UICONTROL Id拼接]**，选择 **[!UICONTROL 专用图]**
1. 对象 **[!UICONTROL 属性合并]**，选择 **[!UICONTROL 数据集优先级]**
1. 拖放 `Luma Loyalty Dataset` 和 `Luma CRM Dataset` 到 **[!UICONTROL 数据集]** 面板。
1. 确保 `Luma Loyalty Dataset` 通过将其拖放到顶部的 `Luma CRM Dataset`
1. 选择 **[!UICONTROL 保存]** 按钮
   <!--do i need to explain Private Graph? Is that GA?-->
   ![合并策略](assets/mergepolicies-newPolicy.png)

## 验证合并策略

让我们看看合并策略是否正在按预期执行：

1. 转到 **[!UICONTROL 浏览]** 选项卡
1. 更改 **[!UICONTROL 合并策略]** 到您的新的 `Loyalty Prioritized` 策略
1. 作为 **[!UICONTROL 身份命名空间]**，使用您的 `Luma CRM Id`
1. 作为 **[!UICONTROL 标识值]** 使用 `112ca06ed53d3db37e4cea49cc45b71e`
1. 选择 **[!UICONTROL 显示配置文件]** 按钮
1. `Daniel` 回来了！

![查看使用其他合并策略的配置文件](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 创建具有有限数据集的合并策略

使用数据集优先级创建合并策略时，配置文件中只会包含您在右侧包含的相同基类的数据集。 让我们设置另一个合并策略

1. 在合并策略屏幕上，选择 **[!UICONTROL 创建合并策略]** 按钮
1. 作为 **[!UICONTROL 名称]**，输入  `Loyalty Only`
1. 作为 **[!UICONTROL 架构]**，选择 **[!UICONTROL XDM配置文件]**
1. 对象 **[!UICONTROL Id拼接]**，选择 **[!UICONTROL 无]**
1. 对象 **[!UICONTROL 属性合并]**，选择 **[!UICONTROL 数据集优先级]**
1. 仅拖放 `Luma Loyalty Dataset` 到 **[!UICONTROL 选定的数据集]** 面板。
1. 选择 **[!UICONTROL 保存]** 按钮

![仅忠诚度合并策略](assets/mergepolicies-loyaltyOnly.png)

## 验证合并策略

现在，我们来看看此合并策略的作用：

1. 转到 **[!UICONTROL 浏览]** 选项卡
1. 更改 **[!UICONTROL 合并策略]** 到您的新的 `Loyalty Only` 策略
1. 作为 **[!UICONTROL 身份命名空间]**，使用您的 `Luma CRM Id`
1. 作为 **[!UICONTROL 标识值]** 使用 `112ca06ed53d3db37e4cea49cc45b71e`
1. 选择 **[!UICONTROL 显示配置文件]** 按钮
1. 确认未找到配置文件：
   ![仅忠诚度无CRM Id查找。](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID是 `Luma Loyalty Dataset`，但只能使用主要身份查找用户档案。 让我们用主要身份查找配置文件， `Luma Loyalty Id`”

1. 更改 **[!UICONTROL 身份命名空间]** 到 `Luma Loyalty Id`
1. 作为 **[!UICONTROL 标识值]** 使用 `5625458`
1. 选择 **[!UICONTROL 显示配置文件]** 按钮
1. 选择配置文件ID以打开配置文件
1. 转到 **[!UICONTROL 属性]** 选项卡
1. 请注意，CRM数据集中的其他配置文件详细信息（如手机号码和电子邮件地址）不可用，因为仅
   ![CRM数据在“仅忠诚度”策略中不可查看](assets/mergepolicies-loyaltyOnly-attributes.png)
1. 转到 **[!UICONTROL 事件]** 选项卡
1. ExperienceEvent数据可用，尽管未明确将其包含在合并策略数据集中：
   ![可以在“仅忠诚度”策略中查看事件](assets/mergepolicies-loyaltyOnly-events.png)

## 有关合并策略的更多信息

在配置文件搜索中，将使用的合并策略改回 `Default Timebased` 并选择 **[!UICONTROL 显示配置文件]** 按钮。 丹尼回来了！

![查看使用其他合并策略的配置文件](assets/mergepolicies-backToDanny.png)

这是怎么回事？ 嗯，配置文件合并不是一次性操作。 根据多种因素（包括使用哪种合并策略），动态组合实时客户用户档案。 您可以创建要在不同上下文中使用的多个合并策略，具体取决于所需的客户视图。

合并策略的一个关键用例是数据治理。 例如，假设您将第三方数据摄取到Platform，这些数据不能用于个性化用例，但是 _可以_ 用于广告用例。 您可以创建一个排除此第三方数据集的合并策略，并使用此合并策略为您的广告用例生成区段。

## 其他资源

* [“合并策略”文档](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [合并策略API（实时客户个人资料API的一部分）参考](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

现在，让我们转到 [数据治理框架](apply-data-governance-framework.md).
