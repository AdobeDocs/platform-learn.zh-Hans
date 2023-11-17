---
title: 安装和配置Adobe Experience Platform Web SDK标记扩展
description: 了解如何在数据收集界面中安装和配置Platform Web SDK标记扩展。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 13%

---

# 安装Adobe Experience Platform Web SDK标记扩展

了解如何在数据收集界面中安装和配置Platform Web SDK标记扩展。 此标记扩展是 _仅标记扩展_ 需要将数据发送到 _所有Adobe Experience Cloud应用程序_，包括 [分析](setup-analytics.md)， [Target](setup-target.md)， [Audience Manager](setup-audience-manager.md)、Real-time Customer Data Platform和Journey Optimizer！

## 学习目标

在本课程结束后，您将能够：

* 在数据收集界面中创建标记属性
* 安装Platform Web SDK标记扩展
* 将之前创建的数据流映射到扩展

## 先决条件

您必须完成本教程中之前的课程：

* [配置权限](configure-permissions.md)
* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)

## 安装Experience PlatformWeb SDK扩展

### 添加属性

首先，您必须具有标记属性。 资产是一个容器，其中包含从网页收集详细信息并将其发送到不同位置所需的所有JavaScript、规则和其他功能。

为教程创建新的标记属性：

1. 打开 [数据收集界面](https://launch.adobe.com/){target="_blank"}
1. 选择 **[!UICONTROL 标记]** 在左侧导航中
1. 选择 **[!UICONTROL 新建属性]** 按钮
   ![添加新属性](assets/websdk-property-addNewProperty.png)
1. 作为 **[!UICONTROL 名称]**，输入 `Web SDK Course` （如果您公司的多个人员参加本教程，请添加您的姓名到结尾）
1. 作为 **[!UICONTROL 域]**，输入 `enablementadobe.com` （稍后解释）
1. 选择 **[!UICONTROL 保存]**
   ![属性详细信息](assets/websdk-property-propertyDetails.png)

## 添加Web SDK扩展

现在通过创建XDM架构、数据流和标记属性，您可以安装Platform Web SDK扩展：

1. 打开您的新标记属性
1. 转到 **[!UICONTROL 扩展]** > **[!UICONTROL 目录]**
1. 搜索 `Adobe Experience Platform Web SDK`
1. 选择 **[!UICONTROL 安装]**

   ![安装Web SDK扩展](assets/extension-platform-web-sdk.jpg)


## 将Platform Web SDK链接到数据流

保留大部分默认设置，以后根据需要进行更新。 您现在必须执行的唯一操作是将扩展链接到数据流：

1. 下 **[!UICONTROL 数据流]**，选择 **[!UICONTROL 从列表选择]** 输入法
1. 选择您之前创建的数据流， `Luma Web SDK`
1. 选择 **[!UICONTROL 保存]**
   >[!NOTE]
   >
   > 如果找不到数据流，请转到 [配置数据流](configure-datastream.md) 课程并按照步骤创建一个

   ![数据流选择](assets/extension-luma-web-sdk-datastream-extension.png)

现在，您已安装Platform Web SDK并将其关联到数据流，接下来就可以开始使用您创建的架构将数据元素映射到XDM对象了。

>[!NOTE]
>
>在本教程中，您只需配置一个数据流，并将其与所有标记环境（开发、暂存和生产）关联。 在您自己的网站上实施Platform Web SDK时，您应该为每个环境配置单独的数据流，并使用将它们映射到您的标记环境 **[!UICONTROL 输入法]** > **[!UICONTROL 输入值]**
>
>![数据流选择](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>虽然您未在配置CNAME， [!UICONTROL 边缘域] 在本课程中的设置中，Adobe建议在您自己的网站上实施Platform Web SDK时使用CNAME。 虽然 CNAME 实施未提供 Cookie 生命周期方面的好处，但可能会带来其他一些好处。这些好处包括广告拦截器和不太常见的浏览器，可防止数据被发送到它们归类为跟踪器的域。在这些情况下，使用 CNAME 可以在对使用这些工具的用户进行数据收集时防止中断。

有关扩展每个部分的更多信息，请参阅 [配置Adobe Experience Platform Web SDK扩展](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=zh-Hans)



[下一步： ](create-data-elements.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
