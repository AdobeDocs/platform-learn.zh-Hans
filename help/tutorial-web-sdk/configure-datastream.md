---
title: 配置数据流
description: 了解如何启用数据流并配置Experience Cloud解决方案。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 4%

---

# 配置数据流

了解如何启用数据流并配置Experience Cloud解决方案。

数据流会告知Adobe Experience Platform Edge Network要将Platform Web SDK收集的数据发送到何处。 在Experience Cloud流配置中，您可以启用Experience Platform应用程序、数据帐户和事件转发。 请参阅 [配置数据流的基础知识](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en) 以了解更多详细信息。

## 学习目标

在本课程结束后，您将能够：

* 创建数据流
* 启用Experience Cloud应用程序
* 启用Experience Platform

## 先决条件

在配置数据流之前，您必须已完成以下课程：

* [配置权限](configure-permissions.md)
* [配置架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)

## 创建数据流

现在，您可以创建数据流以告知Platform Edge Network要将Web SDK收集的数据发送到何处。

**要创建数据流，请执行以下操作：**

1. 打开 [数据收集界面](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. 确保您位于正确的沙盒中

   >[!NOTE]
   >
   >如果您是基于平台的应用程序(如Real-Time CDP)的客户，我们建议在本教程中使用开发沙盒。 如果没有，请使用 **[!UICONTROL 生产]** 沙盒。

1. 转到 **[!UICONTROL 数据流]** 在左侧导航中
1. 选择 **[!UICONTROL 新数据流]** 屏幕右侧。
1. 输入 `Luma Web SDK` 作为 **[!UICONTROL Name]**. 稍后当您在标记属性中配置Web SDK扩展时，将引用此名称。
1. 选择 `Luma Web Event Data` 作为 **[!UICONTROL 事件架构]**
1. 选择 **[!UICONTROL 保存]**

   ![创建数据流](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >以后，映射功能将纳入本教程中。




在下一个屏幕上，您能够将诸如Adobe应用程序之类的服务添加到数据流中，但您在教程中此时不会添加任何服务。 您稍后将在课程中执行此操作 [设置Experience Platform](setup-experience-platform.md), [设置Analytics](setup-analytics.md), [设置Audience Manager](setup-audience-manager.md), [设置目标](setup-target.md)或 [事件转发](setup-event-forwarding.md).

>[!NOTE]
>
>在您自己的网站上实施Platform Web SDK时，应创建三个数据流以映射到三个标记环境（开发、暂存和生产）。 如果您在基于平台的应用程序(如Adobe Real-time Customer Data Platform或Adobe Journey Optimizer)中使用Platform Web SDK，则应确保在相应的Platform沙箱中创建这些数据流。

现在，您可以在标记资产中安装Platform Web SDK扩展！

[下一个： ](install-web-sdk.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
