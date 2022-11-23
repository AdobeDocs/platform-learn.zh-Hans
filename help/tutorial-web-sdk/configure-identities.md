---
title: 配置身份命名空间
description: 了解如何配置身份命名空间以与Adobe Experience Platform Web SDK结合使用。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 2b5013ea01bf4e2388a6e1fc046b1685945be238
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 5%

---

# 配置身份命名空间

了解如何配置身份命名空间以与Adobe Experience Platform Web SDK结合使用。

的 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans) 在所有Adobe解决方案中设置一个通用访客ID，以便增强Experience Cloud功能，如解决方案之间的受众共享。 您还可以将您自己的客户ID发送到该服务，以启用跨设备定位以及与其他系统(如客户关系管理(CRM)系统)的集成。

如果您的网站已在您的网站上使用Experience CloudID服务(通过访客API或Experience CloudID服务标签扩展)，并且您希望在迁移到Adobe Experience Platform Web SDK时继续使用该服务，则您必须使用最新版本的访客API或Experience CloudID服务标签扩展。 请参阅 [ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) 以了解更多信息。

>[!NOTE]
>
> 出于演示目的，本课程中的练习让您能够捕获登录到 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html) 使用凭据， **用户：test@adobe.com /密码：测试**. 虽然您可以使用这些步骤为您自己创建不同的标识，但要了解数据收集界面中身份映射的功能，建议您先跟进以捕获示例标识。

## 学习目标

在本课程结束后，您将能够：

* 了解身份命名空间
* 创建自定义标识命名空间以捕获内部CRM ID


## 先决条件

您必须已完成以前的课程：

* [配置权限](configure-permissions.md)
* [配置架构](configure-schemas.md)

>[!IMPORTANT]
>
>的 [Experience CloudID扩展](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 实施Adobe Experience Platform Web SDK时不需要，因为Web SDK JavaScript库包含访客ID服务功能。

## 创建身份命名空间

在本练习中，您为Luma的自定义标识字段创建标识命名空间， `lumaCrmId`. 身份命名空间在构建实时客户配置文件方面起着关键作用，因为同一命名空间中的两个匹配值允许两个数据源形成身份图。

在开始练习之前，请观看此简短视频，进一步了解Adobe Experience Platform中的身份信息：
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

现在，为Luma CRM ID创建命名空间：

1. 打开 [数据收集界面](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. 选择您在教程中使用的沙盒

   >[!NOTE]
   >
   >如果您是基于平台的应用程序（如实时CDP）的客户，我们建议在本教程中使用一个开发沙盒。 如果没有，请使用 **[!UICONTROL 生产]** 沙盒。

1. 选择 **[!UICONTROL 标识]** 在左侧导航中
1. 选择 **[!UICONTROL 浏览]**

   页面的主界面中会显示身份命名空间列表，其中显示了身份命名空间的名称、身份符号、上次更新日期，以及这些命名空间是标准命名空间还是自定义命名空间。 右边栏包含有关身份图强度的信息。

1. 选择 **[!UICONTROL 创建身份命名空间]**

   ![查看标识](assets/configure-identities-screen.png)

1. 提供详细信息（如下所示）并选择 **[!UICONTROL 创建]**.

   | 字段 | 值 |
   |---------------|-----------|
   | 显示名称 | Luma CRM ID |
   | 身份符号 | lumaCrmId |
   | 类型 | 跨设备ID |


   ![创建命名空间](assets/identities-create-namespace.png)


   在 **[!UICONTROL 标识]** 屏幕。

   ![创建命名空间](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> 在 [创建数据元素](create-data-elements.md) 课程，您将学习如何在向Platform Edge Network发送身份时使用此命名空间。

## 在生产沙盒中创建身份命名空间

由于Web SDK扩展当前存在限制，还必须在生产沙盒中创建身份命名空间，才能使用命名空间将数据发送到开发沙盒。 因此，如果您在本教程中使用了开发沙盒，请另外创建 `Luma CRM ID` 命名空间。

## 其他资源

* [Identity Service 文档](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hans)
* [Identity Service API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

现在，身份就位，可以配置数据流。

[下一个： ](configure-datastream.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
