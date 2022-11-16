---
title: 创建数据流
description: 创建数据流
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 创建数据流

您从网站发送的数据会到达一组名为 [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). 此网络可将您的数据发送到 [您之前创建的Adobe Experience Platform数据集](create-a-schema.md) 和Adobe Experience Cloud内的其他产品。 这些Adobe产品也可能会对您的网页做出数据响应。 例如，边缘网络可能会从Adobe Target返回个性化内容。

要配置Edge Network将数据往返于哪些Adobe产品，您必须创建数据流。 当边缘网络从您的网页收到数据时，它会咨询您创建的数据流，读取其配置，然后将数据转发到相应的Adobe产品。

要创建数据流，请首先导航到 [!UICONTROL 数据流] 在 [!UICONTROL 数据收集]. 单击 [!UICONTROL 创建数据流] 中。 为数据流提供名称。

![数据流名称和描述](../../../assets/implementation-strategy/datastream-name-description.png)

在下一个屏幕中，您可以配置哪些Adobe产品应接收您从网站发送的数据。 在本教程中，仅启用Adobe Experience Platform，然后选择您之前创建的数据集（将在默认值中） [!UICONTROL 生产] )，然后单击 [!UICONTROL 保存].

![数据流产品配置](../../../assets/implementation-strategy/datastream-product-configuration.png)

您的数据流已创建。

## 数据流环境

公司通常具有任何网站更新的促销路径。 公司中的某人（营销人员或工程师，具体取决于所做的更改）通常会在只有该人员正在使用的开发环境中测试其更改。 在对更改感到满意后，所做的更改会被提升到暂存环境，以便他们接受进一步的测试。 最后，将所做的更改发布到用户看到的生产网站。 数据流支持此促销模式。

单击 [!UICONTROL 保存]，您应该注意到已为您自动创建了三个数据流环境： [!UICONTROL 开发环境], [!UICONTROL 暂存环境]和 [!UICONTROL 生产环境].

![数据流环境](../../../assets/implementation-strategy/datastream-environments.png)

如果单击每个数据流环境，您会注意到它们都获得了您提供的相同配置。 但是，可以单独自定义这些环境。

如果您熟悉Adobe Experience Platform标记，则可能已经熟悉开发、暂存和生产环境的概念。 标记中的环境与数据流中的环境相关。 当您通过标记发布工作流程将标记库从开发、暂存移至生产时，使用的数据流环境同样会自动从 [!UICONTROL 开发环境]，更改为 [!UICONTROL 暂存环境]，更改为 [!UICONTROL 生产环境]. 例如，这允许您在更改处于开发状态时将数据发送到一个数据集，并在更改处于生产状态时将数据发送到其他数据集。 这样，您的生产数据就可以免受开发过程中可能产生的任何垃圾数据的影响。 我们稍后将在标记属性中配置扩展时讨论数据流环境。

服务器现已完全配置为从网页接收数据。
