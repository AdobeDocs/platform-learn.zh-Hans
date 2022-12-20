---
title: 使用Web SDK将数据流式传输到Adobe Experience Platform
description: 了解如何使用Web SDK将Web数据流式传输到Adobe Experience Platform。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
exl-id: 4d749ffa-e1c0-4498-9b12-12949807b369
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 5%

---

# 使用Web SDK流数据到Experience Platform

了解如何使用Platform Web SDK将Web数据流式传输到Adobe Experience Platform。

Experience Platform是所有新Experience Cloud应用程序(如Adobe Real-time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer)的骨干。 这些应用程序旨在使用Platform Web SDK作为其最佳的Web数据收集方法。

Experience Platform使用之前创建的相同XDM架构从Luma网站中捕获事件数据。 当该数据被发送到Platform Edge Network时，数据流配置可将其转发到Experience Platform。

## 学习目标

在本课程结束后，您将能够：

* 在Adobe Experience Platform中创建数据集
* 配置数据流以将Web SDK数据发送到Adobe Experience Platform
* 为实时客户资料启用流式Web数据
* 验证数据是否已同时登录到Platform数据集和实时客户资料中

## 先决条件

您应该已经完成以下课程：

* 的 **初始配置** 课程：
   * [配置权限](configure-permissions.md)
   * [配置XDM架构](configure-schemas.md)
   * [配置数据流](configure-datastream.md)
   * [配置身份命名空间](configure-identities.md)

* 的 **标记配置** 课程：
   * [安装Web SDK扩展](install-web-sdk.md)
   * [创建数据元素](create-data-elements.md)
   * [创建标记规则](create-tag-rule.md)


## 创建数据集

成功摄取到Adobe Experience Platform的所有数据都将作为数据集保留在数据湖中。 A [数据集](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=en) 是用于数据集合（通常是表）的存储和管理结构，其中包含架构（列）和字段（行）。 数据集还包含描述其存储的数据的各方面特性的元数据。

在本练习中，您将创建一个数据集来跟踪 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!WARNING]
>
>您必须已创建 `Luma Web Event Data` 架构，如上一课中所述， [配置XDM架构](configure-schemas.md).


1. 转到 [Experience Platform界面](https://experience.adobe.com/platform/)
1. 确认您位于在本教程中使用的开发沙盒中
1. 打开 **[!UICONTROL 数据集]** 从左侧导航
1. 选择 **[!UICONTROL 创建数据集]**

   ![创建架构](assets/experience-platform-create-dataset.png)

1. 选择 **[!UICONTROL 从架构创建数据集]** 选项

   ![从架构创建数据集](assets/experience-platform-create-dataset-schema.png)

1. 选择 `Luma Web Event Data` 在中创建的架构 [前课](configure-schemas.md) 然后选择 **[!UICONTROL 下一个]**

   ![数据集，选择架构](assets/experience-platform-create-dataset-schema-selection.png)

1. 提供 **[!UICONTROL 名称]** 可选 **[!UICONTROL 描述]** （对于数据集）。 对于本练习，请使用 `Luma Web Event Data`，然后选择 **[!UICONTROL 完成]**

   ![数据集名称 ](assets/experience-platform-create-dataset-schema-name.png)

数据集现已配置为开始从您的Platform Web SDK实施中收集数据。

## 配置数据流

现在，您可以配置 [!UICONTROL 数据流] 将数据发送到 [!UICONTROL Adobe Experience Platform]. 数据流是您的标记属性、Platform Edge Network和Experience Platform数据集之间的链接。

1. 打开 [数据收集](https://experience.adobe.com/#/data-collection){target=&quot;blank&quot;}接口
1. 选择 **[!UICONTROL 数据流]** 从左侧导航
1. 在 [配置数据流](configure-datastream.md) 课程， `Luma Web SDK`

   ![选择Luma Web SDK数据流](assets/datastream-luma-web-sdk.png)

1. 选择 **[!UICONTROL 添加服务]**

   ![向数据流添加服务](assets/experience-platform-addService.png)
1. 选择 **[!UICONTROL Adobe Experience Platform]** 作为 **[!UICONTROL 服务]**
1. 选择 `Luma Web Event Data` 作为 **[!UICONTROL 事件数据集]**

1. 选择&#x200B;**[!UICONTROL 保存]**。

   ![数据流配置](assets/experience-platform-datastream-config.png)

在 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html) 映射到您的标记属性时，数据将填充Experience Platform集！

## 验证数据集

此步骤对于确保数据已登录数据集至关重要。 验证发送到数据集的数据有两个方面。

* 使用进行验证 [!UICONTROL Experience Platform调试器]
* 使用进行验证 [!UICONTROL 预览数据集]
* 使用进行验证 [!UICONTROL 查询服务]

### Experience Platform Debugger

这些步骤与您在 [Debugger课程](validate-with-debugger.md). 但是，由于数据只有在数据流中启用后才会发送到平台，因此您必须生成一些更多示例数据：

1. 打开 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html) ，然后选择 [!UICONTROL Experience Platform调试器] 扩展图标

1. 配置Debugger以将标记属性映射到 *您的* 开发环境，如 [使用Debugger进行验证](validate-with-debugger.md) 课程

   ![Debugger 中显示的 Launch 开发环境](assets/experience-platform-debugger-dev.png)

1. 使用凭据 `test@adobe.com`/`test` 登录 Luma 网站

1. 返回 [Luma 主页](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 在Debugger显示的Platform Web SDK网络信标中，选择“events”行以在弹出窗口中展开详细信息

   ![Debugger中的Web SDK](assets/experience-platform-debugger-dev-eventType.png)

1. 在弹出窗口中搜索“identityMap”。 在此，您应会看到lumaCrmId，其中包含三个键，即authenticatedState、id和primary
   ![Debugger中的Web SDK](assets/experience-platform-debugger-dev-idMap.png)

现在，数据应填充在 `Luma Web Event Data` 数据集，并准备好进行“预览数据集”验证。

### 预览数据集

要确认数据已登录Platform的数据湖，快速选项是使用 **[!UICONTROL 预览数据集]** 功能。 Web SDK数据会微批量到数据湖，并定期在平台界面中刷新。 可能需要10-15分钟才能查看您生成的数据。

1. 在 [Experience Platform](https://experience.adobe.com/platform/) 界面，选择 **[!UICONTROL 数据集]** 在左侧导航中打开 **[!UICONTROL 数据集]** 功能板。

   功能板列出了贵组织的所有可用数据集。 系统会为每个列出的数据集显示详细信息，包括其名称、数据集所遵循的架构以及最近摄取运行的状态。

1. 选择 `Luma Web Event Data` 数据集以打开其 **[!UICONTROL 数据集活动]** 屏幕。

   ![数据集Luma Web事件](assets/experience-platform-dataset-validation-lumaSDK.png)

   活动屏幕包括一个图形，用于可视化消息使用率，以及成功和失败批次的列表。

1. 从 **[!UICONTROL 数据集活动]** 屏幕，选择 **[!UICONTROL 预览数据集]** 位于屏幕右上角附近，可预览多达100行数据。 如果数据集为空，则会停用预览链接。

   ![数据集预览](assets/experience-platform-dataset-preview.png)

   在预览窗口中，数据集架构的层次视图将显示在右侧。

   ![数据集预览1](assets/experience-platform-dataset-preview-1.png)

>[!INFO]
>
>Adobe Experience Platform的查询服务是一种更可靠的方法，用于验证湖中的数据，但不在本教程的涵盖范围内。 有关更多详细信息，请参阅 [浏览数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=zh-CN) 中的“平台教程”部分。


## 为实时客户配置文件启用数据集和架构

下一步是为实时客户用户档案启用数据集和架构。 来自Web SDK的数据流将是流入Platform的众多数据源之一，您希望将Web数据与其他数据源相连，以构建360度客户配置文件。 要了解有关实时客户资料的更多信息，请观看此简短视频：

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on&captions=eng)

>[!CAUTION]
>
>在使用您自己的网站和数据时，我们建议在启用数据以用于实时客户资料之前，对数据进行更可靠的验证。


**要启用数据集，请执行以下操作：**

1. 打开您创建的数据集， `Luma Web Event Data`

1. 选择 **[!UICONTROL 配置文件切换]** 打开

   ![配置文件切换](assets/setup-experience-platform-profile.png)

1. 确认您要 **[!UICONTROL 启用]** 数据集

   ![配置文件启用切换](assets/setup-experience-platform-profile-enable.png)

**要启用架构，请执行以下操作：**

1. 打开您创建的架构， `Luma Web Event Data`

1. 选择 **[!UICONTROL 配置文件切换]** 打开

   ![配置文件切换](assets/setup-experience-platform-profile-schema.png)

1. 选择 **[!UICONTROL 此架构的数据将在identityMap字段中包含主标识。]**

   >[!IMPORTANT]
   >
   >    发送到实时客户用户档案的每个记录都需要主要身份。 通常，标识字段会在架构中进行标记。 但是，使用身份映射时，标识字段在架构中不可见。 此对话框用于确认您已考虑主身份，并且在发送数据时将在身份映射中指定该身份。 如您所知，Web SDK使用身份映射，而Experience CloudID(ECID)是默认的主标识。


1. 选择 **[!UICONTROL 启用]**

   ![配置文件启用切换](assets/setup-experience-platform-profile-schema-enable.png)

1. 选择 **[!UICONTROL 保存]** 保存更新的架构

现在，还为用户档案启用了架构。

>[!IMPORTANT]
>
>    为配置文件启用架构后，便无法禁用或删除该架构。 此外，在此时间点之后，无法从架构中删除字段。 当您在生产环境中处理自己的数据时，请务必记住以后要考虑的这些影响。 在本教程中，您应该使用一个开发沙盒，该沙盒可随时删除。
>
>   
> 使用您自己的数据时，我们建议您按以下顺序执行操作：
> 
> * 首先，将一些数据摄取到数据集。
> * 解决在数据获取过程中出现的任何问题（例如，数据验证或映射问题）。
> * 为用户档案启用数据集和架构
> * 重新摄取数据



### 验证用户档案

您可以在Platform界面(或Journey Optimizer界面)中查找客户配置文件，以确认数据已登录到实时客户配置文件。 如名称所示，用户档案会实时填充，因此不会像验证数据集中的数据那样出现延迟。

首先，必须生成更多示例数据。 重复本课程前面的步骤，以在将Luma网站映射到您的标记属性后登录到该网站。 Inspect Web SDK请求，以确保通过 `lumaCRMId`.

1. 在 [Experience Platform](https://experience.adobe.com/platform/) 界面，选择 **[!UICONTROL 用户档案]** 在左侧导航中

1. 作为 **[!UICONTROL 身份命名空间]** use `lumaCRMId`
1. 复制并粘贴 `lumaCRMId` 在您在Experience Platform调试器中检查的调用中传递(可能 `112ca06ed53d3db37e4cea49cc45b71e`)。

   ![配置文件](assets/experience-platform-validate-dataset-profile.png)

1. 如果配置文件中的 `lumaCRMId`，控制台中会填充一个配置文件ID:

   ![配置文件](assets/experience-platform-validate-dataset-profile-set.png)

1. 单击 [!UICONTROL 配置文件ID] 和 [!UICONTROL 客户用户档案] 控制台中会填充相应变量。 在这里，您可以看到与 `lumaCRMId`，例如 `ECID`:

   ![客户用户档案](assets/experience-platform-validate-dataset-custProfile.png)

您现在已为Experience Platform启用Platform Web SDK(和Real-Time CDP! Customer Journey Analytics! 还有Journey Optimizer!)!


[下一个： ](setup-analytics.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)