---
title: 配置教程的权限
description: 了解如何请求访问Experience PlatformWeb SDK，并配置完成“使用Web SDK实施Adobe Experience Cloud”教程所需的权限。
feature: Access Control
exl-id: d7c4f2c3-cf3c-4587-88f8-82113d250084
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 6%

---

# 配置教程的权限

了解如何请求访问Experience PlatformWeb SDK，以及配置完成本教程所需的权限。 要在数据收集界面中使用标记实施Platform Web SDK，您必须在 [Admin Console](https://adminconsole.adobe.com).

## 数据收集

* 拥有 **[!UICONTROL 开发]**, **[!UICONTROL 编辑]**, **[!UICONTROL 批准]**, **[!UICONTROL 发布]**, **[!UICONTROL 管理扩展]**, **[!UICONTROL 管理环境]**&#x200B;和 **[!UICONTROL 管理资产]**. 有关标记权限的更多信息，请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* 如果您将要完成可选事件转发课程，请获得包含边缘转发和权限项的产品许可证 **[!UICONTROL 平台]** > **[!UICONTROL Edge]**

## Experience Platform

这些功能应当可供所有Experience Cloud客户使用，即使您不是基于平台的应用程序(如Real-Time CDP)的客户也是如此。

* 访问 **默认生产**, **&quot;Prod&quot;** 沙盒(.
* 访问 **[!UICONTROL 管理架构]** 和 **[!UICONTROL 查看架构]** 在 **[!UICONTROL 数据建模]**
* 访问 **[!UICONTROL 管理身份命名空间]** 和 **[!UICONTROL 查看身份命名空间]** 在 **[!UICONTROL Identity Management]**
* 访问 **[!UICONTROL 管理数据流]** 和 **[!UICONTROL 查看数据流]** 在 **[!UICONTROL 数据收集]**
* 如果您是基于平台的应用程序的客户，并且将在 [设置Experience Platform](setup-experience-platform.md) 课程中，您还应该：
   * 访问 **开发** 沙盒。
   * 下的所有权限项 **[!UICONTROL 数据管理]**&#x200B;和 **[!UICONTROL 配置文件管理]**:


有关平台访问控制的更多信息，请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hans).

## Adobe Analytics

对于可选的Adobe Analytics课程，您必须 [对报表包设置、处理规则和Analysis Workspace的管理员访问权限](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=zh-Hans)

## Adobe Target

对于可选的Adobe Target课程，您必须 [编辑者或审批者](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 访问权限。

## Adobe Audience Manager

* 对于可选的Audience Manager课程，您必须有权创建、读取和写入特征、区段和目标。 有关更多信息，请参阅 [Audience Manager基于角色的访问控制](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

现在，您可以开始初始配置步骤。

[下一个： ](configure-schemas.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
