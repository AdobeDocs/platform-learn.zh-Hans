---
title: 创建数据流
description: 创建数据流
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 创建数据流

您从网站发送的数据会到达一组Adobe服务器，其名称为 [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). 此网络能够将您的数据发送到 [您之前创建的Adobe Experience Platform数据集](create-a-schema.md) 以及Adobe Experience Cloud中的其他产品。 这些Adobe产品可能还会以数据响应您的网页。 例如，Edge Network可能会从Adobe Target返回个性化内容。

要配置Edge Network的哪些Adobe产品来回传送数据，您必须创建数据流。 当Edge Network从您的网页接收数据时，它会查询您创建的数据流，读取其配置，然后将数据转发到适当的Adobe产品。

要创建数据流，请首先导航到 [!UICONTROL 数据流] 在中查看 [!UICONTROL 数据收集]. 单击 [!UICONTROL 创建数据流] 在右上角。 提供数据流的名称。

![数据流名称和描述](../../../assets/implementation-strategy/datastream-name-description.png)

在下一个屏幕中，您可以配置哪些Adobe产品应接收您从网站发送的数据。 在本教程中，请仅启用Adobe Experience Platform，然后选择您之前创建的数据集(默认为 [!UICONTROL Prod] 沙盒)，然后单击 [!UICONTROL 保存].

![数据流产品配置](../../../assets/implementation-strategy/datastream-product-configuration.png)

已创建您的数据流。

## 数据流环境

公司通常具有任何网站更新的促销路径。 公司的人员（营销人员或工程师，具体取决于更改）通常会在仅该人员使用的开发环境中测试其更改。 一旦他们对更改感到满意，就会将更改提升到暂存环境，并在该环境中接受进一步的测试。 最后，更改将发布到用户看到的生产网站。 数据流支持此提升模式。

在您单击 [!UICONTROL 保存]，您应该已经注意到，系统自动为您创建了三个数据流环境： [!UICONTROL 开发环境]， [!UICONTROL 暂存环境]、和 [!UICONTROL 生产环境].

![数据流环境](../../../assets/implementation-strategy/datastream-environments.png)

如果单击每个数据流环境，您会注意到它们都获得了与您提供的相同配置。 但是，这些环境可以单独进行自定义。

如果您熟悉Adobe Experience Platform Tags，那么您可能已经熟悉了开发、暂存和生产环境的概念。 标记中的环境与数据流中的环境相关。 当您通过标记发布工作流将标记库从开发环境移动到暂存环境、再到生产环境时，使用的数据流环境也将自动从 [!UICONTROL 开发环境]，至 [!UICONTROL 暂存环境]，至 [!UICONTROL 生产环境]. 例如，这允许您在更改处于开发状态时将数据发送到一个数据集，并在更改处于生产状态时将数据发送到其他数据集。 这样可以使生产数据免受您在开发过程中可能生成的任何垃圾数据的影响。 我们稍后将在您的标记属性中配置扩展时讨论数据流环境。

服务器现已完全配置为从网页接收数据。
