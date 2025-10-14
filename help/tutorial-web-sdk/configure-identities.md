---
title: 配置身份命名空间
description: 了解如何配置身份命名空间以用于Adobe Experience Platform Web SDK。 本课程是《使用 Web SDK 实施 Adobe Experience Cloud》教程的一部分。
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 12%

---

# 配置身份命名空间

了解如何配置身份标识命名空间，以与 Adobe Experience Platform Web SDK 一起使用。

[Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/zh-hans/docs/id-service/using/home)在基于SDK的Adobe应用程序中设置了一个通用访客ID (ECID)，以增强Experience Cloud功能，如应用程序之间的受众共享。 您还可以将自己的客户ID发送到该服务，以启用跨设备定位以及与其他系统(例如客户关系管理(CRM)系统)的集成。

[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/identity/home)（是的，有两个！）使用ECID和客户ID生成标识图，从而允许您将属性和行为合并到实时客户配置文件中。

>[!NOTE]
>
>使用Web SDK实施Adobe Analytics、Adobe Target或Adobe Audience Manager时，_不需要_&#x200B;自定义身份命名空间（身份验证身份可以在`data`对象中传递，而不是你稍后将看到的`xdm`对象中传递）。 平台原生应用程序(如Journey Optimizer、Real-Time Customer Data Platform、Customer Journey Analytics)需要身份命名空间。 虽然您可以决定不在自己的实施中使用身份命名空间，但您应当在本教程中这样做。

>[!NOTE]
>
> 出于演示目的，本课程中的练习允许您使用凭据[用户： &#x200B;](https://luma.enablementadobe.com/content/luma/us/en.html) /密码： test **捕获登录到`test@test.com`Luma演示站点**&#x200B;的虚构客户的身份详细信息。

## 学习目标

在本课程结束后，您将能够：

* 了解身份命名空间
* 创建自定义身份命名空间以捕获内部CRM ID


## 先决条件

您必须已完成之前的课程：

* [配置架构](configure-schemas.md)

>[!IMPORTANT]
>
>实施Adobe Experience Platform Web SDK时不需要[Experience Cloud ID扩展](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension)，因为Web SDK JavaScript库包含访客ID服务功能。
>
> 如果您的网站已经在您的网站上通过访客API或Experience Cloud ID服务标签扩展使用Experience Cloud ID服务，并且您希望在迁移到Adobe Experience Platform Web SDK时继续使用它，则必须使用最新版本的访客API或Experience Cloud ID服务标签扩展。 有关详细信息，请参阅[ID迁移](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview)。

## 创建身份命名空间

在本练习中，您将为Luma的自定义身份字段`lumaCrmId`创建身份命名空间。 身份标识命名空间在构建实时客户轮廓方面发挥着关键作用，因为同一命名空间的两个匹配值会让两个数据源形成身份标识图。

在开始练习之前，请观看此简短视频，了解有关Adobe Experience Platform中标识的更多信息：

>[!VIDEO](https://video.tv.adobe.com/v/3422769?learn=on&enablevpops&captions=chi_hans)

现在，为Luma CRM ID创建一个命名空间：

1. 打开[数据收集接口](https://experience.adobe.com/data-collection/){target="_blank"}
1. 选择您将在教程中使用的沙盒

   >[!NOTE]
   >
   >如果您是基于Platform的应用程序(如Real-Time CDP或Journey Optimizer)的客户，我们建议您在本教程中使用开发沙盒。 如果不是，请使用&#x200B;**[!UICONTROL Prod]**&#x200B;沙盒。

1. 在左侧导航中选择&#x200B;**[!UICONTROL 标识]**
1. 选择&#x200B;**[!UICONTROL 浏览]**

   该页面的主界面中将显示一个身份命名空间列表，其中显示了身份命名空间的名称、身份符号、上次更新日期以及它们是标准命名空间还是自定义命名空间。 右边栏包含有关[!UICONTROL 身份图形强度]的信息。

1. 选择&#x200B;**[!UICONTROL 创建身份命名空间]**

   ![查看身份](assets/configure-identities-screen.png)

1. 提供如下详细信息，然后选择&#x200B;**[!UICONTROL 创建]**。

   | 字段 | 值 |
   |---------------|-----------|
   | 显示名称 | Luma CRM ID |
   | 身份标识符号 | lumaCrmId |
   | 类型 | 个人跨设备 ID |


   ![创建命名空间](assets/identities-create-namespace.png)


   标识命名空间填充在&#x200B;**[!UICONTROL 标识]**&#x200B;屏幕中。

   ![创建命名空间](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> 在[创建身份](create-identities.md)课程中，您将了解在向Platform Edge Network发送身份时如何使用此命名空间。

现在，标识已准备就绪，可以配置数据流。

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享这些内容
