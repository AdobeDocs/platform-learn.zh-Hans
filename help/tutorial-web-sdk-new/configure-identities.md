---
title: 配置身份命名空间
description: 了解如何配置要与Adobe Experience Platform Web SDK一起使用的身份命名空间。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Web SDK,Identities
source-git-commit: ef3d374f800905c49cefba539c1ac16ee88c688b
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 8%

---

# 配置身份命名空间

了解如何配置要与Adobe Experience Platform Web SDK一起使用的身份命名空间。

此 [Adobe Experience Cloud Identity服务](https://experienceleague.adobe.com/docs/id-service/using/home.html) 在基于SDK的Adobe应用程序中设置一个通用访客ID (ECID)，以便增强Experience Cloud功能（如应用程序之间的受众共享）。 您还可以将自己的客户ID发送到该服务，以启用跨设备定位以及与其他系统(例如客户关系管理(CRM)系统)的集成。

此 [Adobe Experience Platform Identity服务](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hans) （是的，有两个！） 使用ECID和客户ID生成身份图，允许您将属性和行为合并到实时客户配置文件中。



>[!NOTE]
>
> 出于演示目的，本课程中的练习允许您捕获登录到中的虚构客户的身份详细信息。 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html) 使用凭据， **用户： `test@adobe.com` /密码：测试**.

## 学习目标

在本课程结束后，您将能够：

* 了解身份命名空间
* 创建自定义身份命名空间以捕获内部CRM ID


## 先决条件

您必须已完成之前的课程：

* [配置架构](configure-schemas.md)

>[!IMPORTANT]
>
>此 [Experience CloudID扩展](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 在实施Adobe Experience Platform Web SDK时不需要使用，因为Web SDK JavaScript库包含访客ID服务功能。
>
> 如果您的网站已经在您的网站上通过访客API或Experience CloudID服务标签扩展使用Experience CloudID服务，并且您希望在迁移到Adobe Experience Platform Web SDK时继续使用该服务，则必须使用最新版本的访客API或Experience CloudID服务标签扩展。 请参阅 [ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) 以了解更多信息。

## 创建身份命名空间

在本练习中，您将为Luma的自定义身份字段创建一个身份命名空间， `lumaCrmId`. 身份命名空间在构建实时客户个人资料方面发挥着关键作用，因为同一命名空间的两个匹配值会让两个数据源形成身份图。

在开始练习之前，请观看此简短视频，了解有关Adobe Experience Platform中标识的更多信息：

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

现在，为Luma CRM ID创建一个命名空间：

1. 打开 [数据收集界面](https://launch.adobe.com/){target="_blank"}
1. 选择您将在教程中使用的沙盒

   >[!NOTE]
   >
   >如果您是基于Platform的应用程序(如Real-Time CDP或Journey Optimizer)的客户，我们建议您在本教程中使用开发沙盒。 如果不是，请使用 **[!UICONTROL Prod]** 沙盒。

1. 选择 **[!UICONTROL 身份]** 在左侧导航中
1. 选择 **[!UICONTROL 浏览]**

   该页面的主界面中将显示一个身份命名空间列表，其中显示了身份命名空间的名称、身份符号、上次更新日期以及它们是标准命名空间还是自定义命名空间。 右边栏包含有关以下项的信息 [!UICONTROL 身份图强度].

1. 选择 **[!UICONTROL 创建身份命名空间]**

   ![查看身份](assets/configure-identities-screen.png)

1. 提供以下详细信息，然后选择 **[!UICONTROL 创建]**.

   | 字段 | 值 |
   |---------------|-----------|
   | 显示名称 | Luma CRM ID |
   | 身份符号 | lumaCrmId |
   | 类型 | 单个跨设备ID |


   ![创建命名空间](assets/identities-create-namespace.png)


   身份命名空间将填充在 **[!UICONTROL 身份]** 屏幕。

   ![创建命名空间](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> 在 [创建身份](create-identities.md) 课程，您将学习如何在向Platform Edge Network发送身份信息时使用此命名空间。

## 在生产沙盒中创建身份命名空间

由于Web SDK扩展中的当前限制，还必须在生产沙盒中创建身份命名空间，才能使用命名空间将数据发送到开发沙盒。 因此，如果您在本教程中使用了开发沙盒，则还应创建 `Luma CRM ID` 生产沙盒中的命名空间。

现在，标识已准备就绪，可以配置数据流。

[下一步： ](configure-datastream.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
