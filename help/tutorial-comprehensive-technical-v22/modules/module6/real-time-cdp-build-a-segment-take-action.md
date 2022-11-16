---
title: Real-time CDP — 构建一个区段并采取行动
description: Real-time CDP — 构建一个区段并采取行动
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---

# 6. Real-time CDP — 构建一个区段并采取行动

**作者： [沃特·范·格鲁韦](https://www.linkedin.com/in/woutervangeluwe/), [阿尔贝托·德卡罗](https://www.linkedin.com/in/albertodecaro/), [贝内迪克特·威德尼克](https://www.linkedin.com/in/benedikt-wedenik/)**

在此模块中，您将配置一个流区段，并将该区段激活到多个目标。

## 学习目标

- 了解如何构建区段并启用该区段以进行流处理。
- 了解如何使用Adobe Experience Platform UI配置广告目标。
- 了解如何将区段连接到目标并激活它。
- 了解如何在Adobe Audience Manager中使用Adobe Experience Platform区段，以及如何在Adobe Experience Platform中使用Adobe Audience Manager区段，这要归功于双向区段共享。

## 先决条件

- 访问 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 访问Adobe Target
- 访问AWS S3

>[!IMPORTANT]
>
>本教程的创建是为了促进特定研讨会格式。 它使用您可能无权访问的特定系统和帐户。 即使没有访问权限，我们认为您仍然可以通过阅读这些非常详细的内容来学习很多知识。 如果您是某个研讨会的参加者，并且需要您的访问凭据，请联系您的Adobe代表，他们将为您提供所需的信息。

## 架构概述

请查看以下架构，其中重点介绍了将在本模块中讨论和使用的组件。

![架构概述](../../assets/images/architecturem11.png)

## 要使用的沙盒

对于本模块，请使用以下沙盒： `--module11sandbox--`.

>[!NOTE]
>
>请不要忘记安装、配置和使用Chrome扩展，如 [0.1 — 安装适用于Experience League文档的Chrome扩展](../module0/ex1.md)

## 练习

[6.1创建区段](./ex1.md)

了解如何创建区段。

[6.2查看如何使用目标配置DV360目标](./ex2.md)

了解如何使用Real-Time CDP UI配置广告目标。

[6.3采取行动：将区段发送到DV360](./ex3.md)

将练习6.1中构建的区段连接到目标DV360。

[6.4采取行动：将区段发送到S3目标](./ex4.md)

使用您在练习6.1中构建的区段，并将其发送到S3目标，通常用于电子邮件营销目标。

[6.5采取行动：将区段发送到Adobe Target](./ex5.md)

使用在练习6.1中构建的区段在Adobe Target中配置体验定位活动。

[6.6外部受众](./ex6.md)

将受众从外部源系统导入Adobe Experience Platform。

[6.7目标SDK](./ex7.md)

使用目标SDK配置您自己的目标。

[摘要和优点](./summary.md)

本模块的摘要和优势概述。

>[!NOTE]
>
>谢谢你花时间学习关于Adobe Experience Platform的一切。 如果您有任何疑问，想要分享对未来内容的建议的一般反馈，请直接联系Wouter Van Geluwe，方法是向 **vangeluw@adobe.com**.

[返回到所有模块](../../overview.md)
