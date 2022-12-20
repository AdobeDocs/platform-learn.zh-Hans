---
title: 创建合并策略
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建合并策略
description: 在本课程中，您将创建合并策略以确定数据如何合并到用户档案中。
role: Data Architect, Data Engineer
feature: Profiles
kt: 4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# 创建合并策略

<!--20 min-->

在本课程中，您将创建合并策略，以优先处理如何将多个数据源合并到用户档案中。

Adobe Experience Platform允许您从多个来源将数据合并在一起，以查看每个客户的完整视图。 将此数据整合在一起时，合并策略会确定数据的优先级，以及合并哪些数据以创建统一视图。

我们将坚持使用本课程的用户界面，但API选项也可用于创建合并策略。

**数据架构师** 将需要在本教程之外创建合并策略。

在开始练习之前，请观看此简短视频，了解有关合并策略的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 关于合并策略和合并模式

您可能会记得，在关于批量摄取的课程中，我们为同一客户上传了两个信息略有不同的记录。 在 [!DNL Loyalty] 数据，客户的名字是 `Daniel` 他住在 `New York City`，但在CRM数据中，客户的名字是 `Danny` 他住在 `Portland`. 客户数据会随着时间的推移而发生更改。 也许他从 `Portland` to `New York City`. 其他事情也在变，如电话号码和电子邮件地址。 当两个数据源为同一用户提供不同的信息时，合并策略可帮助您确定如何处理这些类型的冲突。

那为什么 `Danny` 以名取胜？ 让我们看看：

1. 在Platform用户界面中，选择 **[!UICONTROL 用户档案]** 在左侧导航中
1. 转到 **[!UICONTROL 合并策略]** 选项卡
1. 默认的合并策略是按时间戳顺序排列的。 由于您在上传忠诚度数据之后， `Danny` 在配置文件中取名为名字：

![“合并策略”屏幕](assets/mergepolicies-default.png)

为用户档案启用多个架构后， [!UICONTROL 并集架构] 将自动为所有启用了配置文件的记录架构创建共享基类。 您可以查看 [!UICONTROL 合并模式] 通过 **[!UICONTROL 并集架构]** 选项卡。

![“合并策略”屏幕](assets/mergepolicies-unionSchema.png)

请注意，ExperienceEvent类没有并集架构。 虽然ExperienceEvent数据仍然登录到配置文件中，但由于它基于时间序列，因此每个事件都包含时间戳和ID，并且冲突不会出现问题。

如果您不喜欢默认合并策略，该怎么办？ 如果Luma决定，在发生冲突时，他们的CRM系统应该是真相的来源，那该怎么办？ 为此，我们将创建合并策略。

## 在UI中创建合并策略

1. 在“Merge Policies（合并策略）”屏幕上，选择 **[!UICONTROL 创建合并策略]** 按钮
1. 作为 **[!UICONTROL 名称]**，输入 `Loyalty Prioritized`
1. 作为 **[!UICONTROL 架构]**，选择 **[!UICONTROL XDM配置文件]** (请注意，自定义类（因为它是记录数据）也可用于合并策略)
1. 对于 **[!UICONTROL Id拼合]**，选择 **[!UICONTROL 专用图]**
1. 对于 **[!UICONTROL 属性合并]**，选择 **[!UICONTROL 数据集优先级]**
1. 拖放 `Luma Loyalty Dataset` 和 `Luma CRM Dataset` 到 **[!UICONTROL 数据集]** 的上界。
1. 确保 `Luma Loyalty Dataset` 在顶部，将其拖放到 `Luma CRM Dataset`
1. 选择 **[!UICONTROL 保存]** 按钮
<!--do i need to explain Private Graph? Is that GA?-->
![合并策略](assets/mergepolicies-newPolicy.png)

## 验证合并策略

让我们看看合并策略是否正在做我们预期的事情：

1. 转到 **[!UICONTROL 浏览]** 选项卡
1. 更改 **[!UICONTROL 合并策略]** 新 `Loyalty Prioritized` 策略
1. 作为 **[!UICONTROL 身份命名空间]**，使用 `Luma CRM Id`
1. 作为 **[!UICONTROL 标识值]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. 选择 **[!UICONTROL 显示用户档案]** 按钮
1. `Daniel` 回来了！

![查看具有不同合并策略的用户档案](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 创建包含有限数据集的合并策略

使用数据集优先级创建合并策略时，配置文件中只包含您在右侧所包含的相同基类的数据集。 让我们再设置一个合并策略

1. 在“Merge Policies（合并策略）”屏幕上，选择 **[!UICONTROL 创建合并策略]** 按钮
1. 作为 **[!UICONTROL 名称]**，输入  `Loyalty Only`
1. 作为 **[!UICONTROL 架构]**，选择 **[!UICONTROL XDM配置文件]**
1. 对于 **[!UICONTROL Id拼合]**，选择 **[!UICONTROL 无]**
1. 对于 **[!UICONTROL 属性合并]**，选择 **[!UICONTROL 数据集优先级]**
1. 只拖放 `Luma Loyalty Dataset` to **[!UICONTROL 选定的数据集]** 的上界。
1. 选择 **[!UICONTROL 保存]** 按钮

![仅限忠诚度合并策略](assets/mergepolicies-loyaltyOnly.png)

## 验证合并策略

现在，让我们看一下此合并策略的用途：

1. 转到 **[!UICONTROL 浏览]** 选项卡
1. 更改 **[!UICONTROL 合并策略]** 新 `Loyalty Only` 策略
1. 作为 **[!UICONTROL 身份命名空间]**，使用 `Luma CRM Id`
1. 作为 **[!UICONTROL 标识值]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. 选择 **[!UICONTROL 显示用户档案]** 按钮
1. 确认未找到用户档案：
   ![仅忠诚度，无CRM Id查找。](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID是 `Luma Loyalty Dataset`，但只能使用主标识来查找用户档案。 那么，让我们用主身份查找用户档案， `Luma Loyalty Id`&quot;

1. 更改 **[!UICONTROL 身份命名空间]** to `Luma Loyalty Id`
1. 作为 **[!UICONTROL 标识值]** use `5625458`
1. 选择 **[!UICONTROL 显示用户档案]** 按钮
1. 选择用户档案ID以打开用户档案
1. 转到 **[!UICONTROL 属性]** 选项卡
1. 请注意，CRM数据集中的其他配置文件详细信息（如手机号码和电子邮件地址）不可用，因为我们仅
   ![CRM数据在“仅忠诚度”策略中不可见](assets/mergepolicies-loyaltyOnly-attributes.png)
1. 转到 **[!UICONTROL 事件]** 选项卡
1. 尽管未将ExperienceEvent数据明确包含在合并策略数据集中，但仍可用：
   ![可在“仅忠诚度”策略中查看事件](assets/mergepolicies-loyaltyOnly-events.png)

## 有关合并策略的更多信息

在用户档案搜索中，将使用的合并策略更改回 `Default Timebased` ，然后选择 **[!UICONTROL 显示用户档案]** 按钮。 丹尼回来了！

![查看具有不同合并策略的用户档案](assets/mergepolicies-backToDanny.png)

这是怎么回事？ 好吧，档案合并不是一回事。 实时客户用户档案会根据各种因素（包括使用哪些合并策略）动态组合。 您可以创建多个合并策略以在不同的上下文中使用，具体取决于您需要的客户视图。

合并策略的一个关键用例用于数据管理。 例如，假设您将第三方数据摄取到平台，该平台不能用于个性化用例，但 _can_ 用于广告用例。 您可以创建一个合并策略来排除此第三方数据集，并使用此合并策略为广告用例构建区段。

## 其他资源

* [合并策略文档](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [合并策略API（实时客户配置文件API的一部分）参考](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

现在，我们继续 [数据管理框架](apply-data-governance-framework.md).
