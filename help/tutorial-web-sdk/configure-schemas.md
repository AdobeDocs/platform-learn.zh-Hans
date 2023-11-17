---
title: 为Web数据创建XDM架构
description: 了解如何在数据收集界面中为Web数据创建XDM架构。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Web SDK,Tags,Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 5%

---

# 为Web数据创建XDM架构

了解如何在数据收集界面中为Web数据创建XDM架构。

体验数据模型(XDM)架构是在Adobe Experience Platform中构成架构的构建块、原则和最佳实践。

Platform Web SDK使用您的架构来标准化Web事件数据，将其发送到Platform Edge Network，并最终将数据转发到数据流中配置的任何Experience Cloud应用程序。 此步骤至关重要，因为它定义了将客户体验数据提取到Experience Platform中所需的标准数据模型，并支持基于这些标准构建的下游服务和应用程序。

>[!NOTE]
>
> 出于演示目的，本课程中的练习构建了一个示例架构，用于捕获客户在中查看的内容和购买的产品。 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html). 虽然您可以使用这些步骤创建不同的架构以满足您自己的目的，但建议您首先在创建示例架构的同时学习架构编辑器的功能。

要了解有关XDM架构的更多信息，请参加课程»[使用XDM对您的客户体验数据进行建模](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)”或查看 [XDM系统概述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en).

## 学习目标

在本课程结束后，您将能够：

* 从数据收集界面中创建XDM架构
* 将字段组添加到XDM架构
* 使用最佳实践为Web事件数据创建XDM架构

## 先决条件

有关数据收集和Adobe Experience Platform的所有必要配置和用户权限，请参见 [配置权限](configure-permissions.md) 上课。

## 创建 XDM 架构

XDM架构是描述Experience Platform数据的标准方式，允许与架构匹配的所有数据在组织内重复使用，而不会产生冲突，甚至可以在多个组织之间共享。 要了解更多信息，请参阅 [架构组合基础](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans).

在本练习中，您将使用建议的基线字段组创建一个XDM架构，以便捕获 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}：

1. 打开 [数据收集界面](https://launch.adobe.com/){target="_blank"}
1. 确保您在正确的沙盒中

   >[!NOTE]
   >
   >如果您是基于Platform的应用程序(如Real-Time CDP)的客户，我们建议您在本教程中使用开发沙盒。 如果不是，请使用 **[!UICONTROL Prod]** 沙盒。

1. 转到 **[!UICONTROL 架构]** 在左侧导航中
1. 选择 **[!UICONTROL 创建架构]** 右上角的按钮
1. 从下拉菜单中，选择 **[!UICONTROL XDM ExperienceEvent]**

![架构体验事件](assets/schema-XDM-experience-event.jpg)

## 添加字段组

如前所述，XDM是通过提供在下游Adobe Experience Platform服务中使用的通用结构和定义来标准化客户体验数据的核心框架。 通过遵守XDM标准， _所有客户体验数据_ 可以并入共同表示法中。 通过这种方法，您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并使用来自多个来源的数据表示客户属性以进行个性化。 请参阅 [数据建模的最佳实践](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) 以了解更多信息。

如果可能，建议使用现有字段组并遵守与产品无关的模型和命名约定。 对于特定于您的组织、不适合上述预定义字段组的任何数据，您可以创建自定义字段组。 请参阅 [使用架构编辑器创建架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) 有关自定义架构的更多详细步骤。

>[!TIP]
> 
>在本练习中，您将为Web数据收集添加推荐的预定义字段组： _**[!UICONTROL AEP Web SDK ExperienceEvent]**_、和 _**[!UICONTROL 使用者体验事件]**_.

1. 在 **[!UICONTROL 字段组]** 部分，选择 **[!UICONTROL 添加]**
1. 搜索 [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. 选中框
1. 搜索 [!UICONTROL `Consumer Experience Event`]
1. 选中框
1. 选择 **[!UICONTROL 添加字段组]**

   ![添加字段组](assets/schema-add-field-group.jpg)

选择字段组后，您就可以命名架构了。 XDM架构的常见命名惯例是按数据源命名架构：

1. 在**中[!UICONTROL 合成**] 面板，选择 `Untitled schema name`
1. 在 **[!UICONTROL 架构属性]** 面板，输入 **[!UICONTROL 显示名称]** `Luma Web Event Data`
1. 选择除以下项之外的任何项： **[!UICONTROL 显示名称]** 字段以激活 **[!UICONTROL 保存]** option
1. 选择 **[!UICONTROL 保存]**

![Luma Web事件数据](assets/schema-luma-web-event-data.png)

对于这两个字段组，请注意，您有权访问Web上数据收集所需的最常用键值对。 此 [!UICONTROL 显示名称] 的区段生成器界面中向营销人员显示的每个字段的显示名称，您可以根据自己的需求更改标准字段的显示名称。 您还可以删除不需要的字段。 单击任一字段组名称时，界面会突出显示属于它的键值对分组。 在下面的示例中，您可以看到哪些组属于 **[!UICONTROL 使用者体验事件]**.

![架构字段组](assets/schema-consumer-experience-event.jpg)

这个课程只是一个起点。 在构建您自己的Web事件架构时，您必须探索并记录您的业务要求。 此过程与创建 [业务要求文档](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html) 和 [解决方案设计参考](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) 适用于Adobe Analytics实施，但应包括以下要求 _所有下游数据收件人_ 例如，平台、Target和事件转发目标。


### identityMap对象

识别Web用户需要一组特殊的数据，其名称为 `[!UICONTROL identityMap]`.

![Luma Web事件数据](assets/schema-identityMap.png)

它是任何与Web相关的数据收集所必需的Experience Cloud对象，因为它包含识别Web上的用户所需的用户ID。 此外，它还是为经过身份验证的用户设置内部客户ID的关键。 `[!UICONTROL identityMap]` 在中详细讨论 [配置身份](configure-identities.md) 上课。 它自动包含在使用 **[!UICONTROL XDM ExperienceEvent]** 类。


>[!IMPORTANT]
>
> 可以启用 **[!UICONTROL 个人资料]** ，然后再保存架构。 **不要** 此时启用它。 为配置文件启用架构后，无法禁用或删除该架构。 此外，此后无法从架构中删除字段。 在生产环境中使用您自己的数据时，请务必牢记这些含义。
>
>此设置将在以下过程中详细讨论 [设置Experience Platform](setup-experience-platform.md) 上课。
>![配置文件架构](assets/schema-profile.png)

现在，当您将Web SDK扩展添加到标记属性时，便能够引用此架构。


[下一步： ](configure-identities.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
