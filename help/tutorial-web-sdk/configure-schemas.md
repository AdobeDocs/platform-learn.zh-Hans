---
title: 为Web数据创建XDM模式
description: 了解如何在数据收集界面中为Web数据创建XDM模式。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 5%

---

# 为Web数据创建XDM模式

了解如何在数据收集界面中为Web数据创建XDM模式。

体验数据模型(XDM)架构是在Adobe Experience Platform中构建架构的构建基块、原则和最佳实践。

Platform Web SDK使用您的模式来标准化您的Web事件数据，将其发送到Platform Edge Network，并最终将数据转发到数据流中配置的任何Experience Cloud应用程序。 此步骤至关重要，因为它定义了将客户体验数据引入Experience Platform所需的标准数据模型，并支持基于这些标准构建的下游服务和应用程序。

>[!NOTE]
>
> 出于演示目的，本课程中的练习将构建一个示例模式，用于捕获 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html). 虽然您可以使用这些步骤为自己创建不同的模式，但建议您先创建示例模式，以了解模式编辑器的功能。

要进一步了解XDM模式，请参加课程“[使用XDM为您的客户体验数据建模](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)“或查看 [XDM系统概述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh_Hans).

## 学习目标

在本课程结束后，您将能够：

* 从数据收集界面中创建XDM架构
* 将字段组添加到XDM架构
* 使用最佳实践为Web事件数据创建XDM模式

## 先决条件

数据收集和Adobe Experience Platform的所有必要配置和用户权限，如 [配置权限](configure-permissions.md) 课程。

## 创建 XDM 架构

XDM架构是描述Experience Platform中数据的标准方式，它允许符合架构的所有数据在组织内重复使用，而不会发生冲突，甚至在多个组织之间共享。 要了解更多信息，请参阅 [架构组合基础知识](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans).

在本练习中，您将使用推荐的基线字段组创建XDM模式，以在 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}:

1. 打开 [数据收集界面](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. 确保您位于正确的沙盒中

   >[!NOTE]
   >
   >如果您是基于平台的应用程序(如Real-Time CDP)的客户，我们建议在本教程中使用开发沙盒。 如果没有，请使用 **[!UICONTROL 生产]** 沙盒。

1. 转到 **[!UICONTROL 模式]** 在左侧导航中
1. 选择 **[!UICONTROL 创建架构]** 按钮
1. 从下拉菜单中，选择 **[!UICONTROL XDM ExperienceEvent]**

![架构体验事件](assets/schema-XDM-experience-event.jpg)

## 添加字段组

如前所述，XDM是核心框架，通过提供用于下游Adobe Experience Platform服务的通用结构和定义来标准化客户体验数据。 通过遵守XDM标准， _所有客户体验数据_ 可以纳入共同的代表。 此方法允许您从客户操作中获得有价值的洞察，通过区段定义客户受众，以及使用多个来源的数据表达客户属性以实现个性化。 请参阅 [数据建模最佳实践](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) 以了解更多信息。

如果可能，建议使用现有字段组并遵守与产品无关的模型和命名约定。 对于任何特定于贵组织的数据，如果这些数据不适合上述预定义字段组，您可以创建自定义字段组。 请参阅 [使用模式编辑器创建模式](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) 有关自定义模式的更多详细步骤。

>[!TIP]
> 
>在本练习中，您为Web数据收集添加了建议的预定义字段组： _**[!UICONTROL AEP Web SDK ExperienceEvent]**_&#x200B;和 _**[!UICONTROL 消费者体验事件]**_.

1. 在 **[!UICONTROL 字段组]** 选择 **[!UICONTROL 添加]**
1. 搜索 [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. 选中框
1. 搜索 [!UICONTROL `Consumer Experience Event`]
1. 选中框
1. 选择 **[!UICONTROL 添加字段组]**

   ![添加字段组](assets/schema-add-field-group.jpg)

选择字段组后，即可命名架构。 XDM架构的常见命名约定是在数据源之后命名架构：

1. 在**[!UICONTROL 合成**] 面板，选择 `Untitled schema name`
1. 在 **[!UICONTROL 架构属性]** 面板，输入 **[!UICONTROL 显示名称]** `Luma Web Event Data`
1. 选择 **[!UICONTROL 显示名称]** 字段来激活 **[!UICONTROL 保存]** 选项
1. 选择 **[!UICONTROL 保存]**

![Luma Web事件数据](assets/schema-luma-web-event-data.png)

使用这两个字段组，请注意您有权访问Web上数据收集所需的最常用键值对。 的 [!UICONTROL 显示名称] 在基于平台的应用程序的区段生成器界面中，每个字段的显示名称都会向营销人员显示，您可以根据自己的需求更改标准字段的显示名称。 您还可以删除您不希望的字段。 单击任一字段组名称时，界面会突出显示该字段组所属的键值对组。 在以下示例中，您可以看到哪些组属于 **[!UICONTROL 消费者体验事件]**.

![架构字段组](assets/schema-consumer-experience-event.jpg)

这堂课只是一个起点。 在构建您自己的Web事件模式时，您必须探索并记录您的业务要求。 此过程与创建 [业务需求文档](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html) 和 [解决方案设计参考](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) Adobe Analytics实施，但应包括 _所有下游数据收件人_ 例如平台、Target和事件转发目标。


### identityMap对象

需要一组特殊的数据来识别名为 `[!UICONTROL identityMap]`.

![Luma Web事件数据](assets/schema-identityMap.png)

它是任何与Web相关的数据收集的必备对象，因为它包含在Web上标识用户所需的Experience CloudID。 它还是为经过身份验证的用户设置内部客户ID的键。 `[!UICONTROL identityMap]` 在 [配置标识](configure-identities.md) 课程。 它会使用 **[!UICONTROL XDM ExperienceEvent]** 类。


>[!IMPORTANT]
>
> 可以启用 **[!UICONTROL 用户档案]** ，然后保存架构。 **不要** 此时启用它。 为配置文件启用架构后，便无法禁用或删除该架构。 此外，在此时间点之后，无法从架构中删除字段。 当您在生产环境中处理自己的数据时，请务必记住以后要考虑的这些影响。
>
>在 [设置Experience Platform](setup-experience-platform.md) 课程。
>![用户档案架构](assets/schema-profile.png)

现在，在将Web SDK扩展添加到标记属性时，您可以引用此模式。


[下一个： ](configure-identities.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
