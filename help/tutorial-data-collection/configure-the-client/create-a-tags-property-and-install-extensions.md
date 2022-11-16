---
title: 创建Adobe Experience Platform标记属性并安装扩展
description: 创建Adobe Experience Platform标记属性并安装扩展
exl-id: d0fe82b5-a036-4e13-bae1-d1fee78d0084
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# 创建Adobe Experience Platform [!DNL Tags] 资产和安装扩展

现在，页面代码正在将数据和事件推送到数据层，接下来是营销人员从数据层读取数据并将这些数据发送到Adobe Experience Platform的时间。 这通常需要两个JavaScript库：

* Adobe客户端数据层：在前面的步骤中，您创建了数据层数组，并将对象推送到该数组中。 要访问此数据，必须加载Adobe客户端数据层JavaScript库。 此库提供事件和数据层更改的通知，以及对数据的简单访问。
* Adobe Experience Platform Web SDK:此JavaScript库与 [Adobe Experience Platform边缘网络](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). SDK可处理身份、同意、数据收集、个性化、受众等。

虽然您可以将这些单独的库加载到您的网站上并直接使用它们，但我们建议您使用 [Adobe Experience Platform标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans). 借助标记，您可以将单个脚本嵌入到HTML中，并使用标记用户界面来部署Adobe客户端数据层和Adobe Experience Platform Web SDK。 标记还允许您创建用于发送数据的规则，等等。 本教程将使用标记来实现此目的，并假定您基本了解标记的操作方式。

## 在标记中创建属性

1. [在标记中创建属性](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## 安装Adobe客户端数据层扩展

安装Adobe客户端数据层扩展：

1. 选择 **[!UICONTROL 扩展]** 的左侧导航栏（位于您将在本教程中使用的标记属性中）。
1. 选择 **[!UICONTROL 目录]** 链接，然后搜索“数据层”。
1. Adobe客户端数据层显示在结果中后，单击 **[!UICONTROL 安装]** 按钮。 您应会看到配置屏幕。 在本教程中，无需更改默认值。
1. 单击&#x200B;**[!UICONTROL 保存]**。
   ![Adobe客户端数据层扩展安装](../assets/acdl-extension-installation.png)


## 安装Adobe Experience Platform Web SDK扩展

接下来，安装Adobe Experience Platform Web SDK扩展：

1. 在扩展目录中搜索扩展，然后单击相应的 **[!UICONTROL 安装]** 按钮。 您应会看到配置屏幕：
   ![Adobe Experience Platform Web SDK扩展安装](../assets/web-sdk-extension-installation.png)
1. 在 [!UICONTROL 数据流] 字段中，选择您之前创建的数据流。 您会看到与 [创建数据流](../configure-the-server/create-a-datastream.md).
   ![数据流选择](../assets/web-sdk-datastream-selection.png)
1. 进一步，在配置屏幕中，查找并取消选中 **[!UICONTROL 启用点击数据收集]**. 默认情况下，SDK会自动跟踪您的链接。 但是，在本教程中，我们演示了如何使用自定义链接信息跟踪您自己的链接点击量。
1. 单击 **[!UICONTROL 保存]** 按钮以完成安装Adobe Experience Platform Web SDK扩展。

>[!TIP]
>
>数据集环境与“标记”环境有关。 假定您完成Adobe Experience Platform Web SDK扩展的安装后，创建一个包含该扩展的标记库，然后将该库发布到标记开发环境。 当标记库加载到您的网页上，并且Adobe Experience Platform Web SDK扩展向Edge Network发出请求时，该扩展包括 [!UICONTROL 开发环境] 数据流环境ID。 而边缘网络则使用该ID来读取 [!UICONTROL 开发环境] 数据流环境，并将数据转发到相应的Adobe产品。
>
>目前，您只有一个开发数据流环境、一个暂存数据流环境和一个生产数据流环境。 使用数据流用户界面可以创建多个数据流开发环境（一个适用于您，也许是一个适用于您的同事）。 如果您有多个开发数据流环境，则可以选择要用于此标记资产的环境。


已安装相应的扩展。 该创建规则和数据元素了。

[下一个： ](create-rules-for-tracking-page-view-and-commerce-events.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
