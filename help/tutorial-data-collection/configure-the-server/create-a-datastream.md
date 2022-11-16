---
title: 创建数据流
description: 创建数据流
exl-id: 4a33a7f3-8bd8-4d28-9ae4-a0609444485f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 创建数据流

您使用Platform Web SDK从网站发送的数据会到达一组名为 [Adobe Experience Platform边缘网络](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). 此网络可将您的数据发送至 [您之前创建的Adobe Experience Platform数据集](create-a-schema.md) 和Adobe Experience Cloud内的其他产品。 这些Adobe产品也可能会对您的网页做出数据响应。 例如，边缘网络可能会从Adobe Target返回个性化内容。

要配置Edge Network将数据往返于哪些Adobe产品，您必须创建数据流。 当边缘网络从您的网页收到数据时，它会咨询您创建的数据流，读取其配置，然后将数据转发到相应的Adobe产品。

![数据流产品配置](../assets/datastream-diagram.png)

1. 要创建数据流，您必须首先导航到数据收集用户界面。 在Platform的右上角，单击 **[!UICONTROL 应用程序选取器]** 选择 **[!UICONTROL 数据收集]** 下拉菜单中。
   ![“数据收集”菜单](../assets/data-collection-menu.png)
1. 显示数据收集界面后，选择 **[!UICONTROL 数据流]** ，然后 **[!UICONTROL 新数据流]** 按钮。
1. 为数据流提供名称，选择 [您之前创建的架构](create-a-schema.md) 作为 **[!UICONTROL 事件数据集]**，然后选择 **[!UICONTROL 保存]** （稍后将介绍映射）。
   ![数据流名称和描述](../assets/datastream-name-description.png)

## 向数据流添加服务

利用下一个屏幕，可添加哪些Adobe产品和服务应从您的网站接收您发送的数据。

1. 选择 **[!UICONTROL 添加服务]** 命令。 在本教程中，仅启用Adobe Experience Platform，请选择 [您之前创建的数据集](create-a-dataset.md) 选择 **[!UICONTROL 保存]** 中。 您的数据流已创建。
   ![数据流产品配置](../assets/datastream-product-configuration.png)

## 数据流环境

公司通常具有任何网站更新的促销路径。 公司中的某人（营销人员或工程师，具体取决于所做的更改）通常会在只有该人员正在使用的开发环境中测试其更改。 在对更改感到满意后，所做的更改会被提升到暂存环境，以便他们接受进一步的测试。 最后，将所做的更改发布到用户看到的生产网站。 数据流支持此促销模式。

如果您支持基于平台的应用程序，如实时CDP、Journey Optimizer或Customer Journey Analytics，则必须在与这些环境对应的单独平台沙箱中创建其他数据流。

如果您不是Platform客户，则可以在单个沙盒中创建多个数据流，并可以使用数据流复制功能来复制设置。

服务器现已完全配置为从网页接收数据。

[下一个： ](../configure-the-client/whats-a-data-layer.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
