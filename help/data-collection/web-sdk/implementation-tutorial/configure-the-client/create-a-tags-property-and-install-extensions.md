---
title: 创建Adobe Experience Platform标记属性并安装扩展
description: 创建Adobe Experience Platform标记属性并安装扩展
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# 创建Adobe Experience Platform标记属性并安装扩展

现在，页面上的代码正在将数据和事件推送到数据层，这时营销人员应该从数据层读取数据，并将这些数据发送到Adobe Experience Platform。 这通常需要两个JavaScript库：

* Adobe客户端数据层：在前面的步骤中，您创建了一个数据层阵列并将对象推送到其中。 要访问数据，必须加载Adobe客户端数据层JavaScript库，该库提供了接收数据层更改和事件通知的方法，还提供了访问数据的简单方法。
* Adobe Experience Platform Web SDK：此JavaScript库与Adobe Experience Platform Edge Network通信。 SDK可处理身份、同意、数据收集、个性化、受众等。

虽然您可以将这些单独的库加载到您的网站中并直接使用它们，但建议您使用 [Adobe Experience Platform标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html). 借助Tags，您可以将单个脚本嵌入到HTML中，并使用Tags用户界面来部署Adobe客户端数据层和Adobe Experience Platform Web SDK。 标记还允许您为发送数据等创建规则。 本教程将标记用于此目的，并假设您基本了解标记的操作方式。

## 在Tags中创建属性

如果你还没有， [在Tags中创建属性](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## 安装Adobe客户端数据层扩展

导航到扩展目录，找到相应的扩展，然后单击相应的，以安装Adobe客户端数据层扩展 [!UICONTROL 安装] 按钮。 您应该会看到配置屏幕。

![Adobe客户端数据层扩展安装](../../../assets/implementation-strategy/acdl-extension-installation.png)

在本教程中，无需更改默认值。 单击[!UICONTROL 保存]。

## 安装Adobe Experience Platform Web SDK扩展

接下来，通过在扩展目录中找到相应的扩展，然后单击相应的扩展，安装Adobe Experience Platform Web SDK扩展 [!UICONTROL 安装] 按钮。 您应该会看到配置屏幕。

![Adobe Experience Platform Web SDK扩展安装](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

In [创建数据流](../configure-the-server/create-a-datastream.md)，您已创建一个Adobe Experience Platform Edge Network引用的数据流，以确定将入站数据发送到何处。 从Adobe Experience Platform Web SDK向Edge Network发出请求时，必须指示Edge Network应引用哪个数据流。

为此，请查找 [!UICONTROL 数据流] 字段并选择之前创建的数据流。 您会看到与您在中看到的相同的数据流环境 [创建数据流](../configure-the-server/create-a-datastream.md).

![数据流选择](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

如中所述 [创建数据流](../configure-the-server/create-a-dataset.md)，这些数据集环境与标记环境有关联。 假设您完成了Adobe Experience Platform Web SDK扩展的安装，请创建一个包含该扩展的标记库，然后将该库发布到标记开发环境。 当标签库加载到您的网页上，并且Adobe Experience Platform Web SDK扩展向Edge Network发出请求时，该扩展包含 [!UICONTROL 开发环境] 数据流环境ID。 而Edge Network会使用该ID来读取 [!UICONTROL 开发环境] 数据流环境，并将数据转发到适当的Adobe产品。

目前，您只有一个开发数据流环境、一个暂存数据流环境和一个生产数据流环境。 这就是扩展配置用户界面显示所有已预选且不可更改的原因。 但是，可以使用数据流用户界面创建多个数据流开发环境（一个用于您，一个用于您的同事）。 如果您有多个开发数据流环境，则可以选择要用于此标记属性的环境。

最后，向下滚动并取消选中 [!UICONTROL 启用点击数据收集]. 默认情况下，SDK会自动跟踪您的链接。 但是，在本教程中，我们将演示如何使用自定义链接信息跟踪您自己的链接点击。

单击 [!UICONTROL 保存] 按钮以完成安装Adobe Experience Platform Web SDK扩展。

已安装相应的扩展。 是时候创建规则和数据元素了。
