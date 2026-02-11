---
title: Audience Activation到Microsoft Azure活动中心
description: Audience Activation到Microsoft Azure活动中心
kt: 5342
doc-type: tutorial
exl-id: c1f5566d-0f57-4554-95ee-950d66373716
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# 2.4 Real-Time CDP：Audience Activation到Microsoft Azure事件中心

在本模块中，您将设置Microsoft Azure EventHub目标作为Adobe Experience Platform Real-time CDP的实时目标。 您还将设置和部署Azure函数，每当Adobe Experience Platform将受众有效负载交付到Azure EventHub目标时，该函数都将实时触发。 您将触发的Azure函数将显示Adobe Experience Platform Real-time CDP激活功能的机制。

在本模块中，您还将了解什么会触发Real-time CDP将有效负载实际传送到指定目标。 我们还将讨论受众资格的状态以及它与激活的关系。

Adobe Experience Platform Real-time CDP支持将数据激活到流式云存储目标，允许您以JSON格式将受众数据和事件实时导出到这些目标。 然后，您可以基于目标中的这些事件描述业务逻辑

Microsoft Azure事件中心是一项完全托管的实时数据摄取服务，它简单、可靠且可扩展。 每秒从任何来源流式传输数百万个事件以构建动态数据管道并立即响应业务挑战。

## 学习目标

- 熟悉Microsoft Azure活动中心
- 设置Microsoft Azure事件中心的RTCDP目标
- 了解Real-time CDP何时激活以及激活有效负载的外观
- 设置Visual Studio代码以开发、测试和部署您的Azure项目
- 创建和部署利用RTCDP实时提供的受众资格的Azure功能

## 先决条件

- 访问[Adobe Experience Platform](https://experience.adobe.com/platform)
- 了解如何在Adobe Experience Platform中定义、使用和激活受众

>[!NOTE]
>
>请按照[为Chrome文档安装Chrome扩展](../../../getting-started/gettingstarted/ex1.md)中所述，安装、配置并使用Experience League扩展

## 练习

[2.4.1配置环境](./ex1.md)

在本练习中，您将设置Microsoft Azure环境。

[2.4.2配置Microsoft Azure EventHub环境](./ex2.md)

在本练习中，您将设置Microsoft Azure EventHub环境。

[2.4.3在Adobe Experience Platform中配置Azure事件中心目标](./ex3.md)

在本练习中，您将设置您的Real-time CDP目标连接，该连接会将受众实时交付到您在上一个练习中配置的事件中心实例。

[2.4.4创建受众](./ex4.md)

在本练习中，您将在Adobe Experience Platform中创建受众

[2.4.5激活受众](./ex5.md)

在本练习中，您将向EventHub目标激活受众。

[2.4.6创建您的Microsoft Azure项目](./ex6.md)

在本练习中，您将创建一个Azure函数，当Adobe Experience Platform将受众资格交付到相应的Azure事件中心目标时，该函数将实时触发。

[2.4.7端到端方案](./ex7.md)

此时，一切都已设置。 您现在可以在演示网站上进行浏览，并将受众资格交付到Microsoft Azure事件中心触发器功能。

![技术内部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform及其应用程序的所有知识。 如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./../../../../overview.md)
