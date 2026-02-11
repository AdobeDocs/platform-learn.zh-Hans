---
title: 在呼叫中心查看您的实时客户资料的实际操作情况
description: 在呼叫中心查看您的实时客户资料的实际操作情况
kt: 5342
doc-type: tutorial
exl-id: d3bd34a1-5577-4da7-a5a5-0f186b1a73c2
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 5%

---

# 2.1.5在呼叫中心查看您的实时客户资料

在本练习中，目标是让您逐步了解客户历程，并像真实客户一样操作。

在此网站上，我们实施了Adobe Experience Platform。 每个操作都被视为体验事件，实时发送到Adobe Experience Platform，以补充实时客户资料。

在之前的练习中，你最初是一个匿名客户，在浏览网站后，经过几个步骤，你成为了一个已知客户。

当同一客户最终接听电话并致电您的呼叫中心时，能够立即获得其他渠道的信息至关重要，这样呼叫中心体验才能变得相关和个性化。

## 使用您的CX App

转到[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登录后，您将看到此内容。 单击CX App项目上的3个点&#x200B;**...**，然后单击&#x200B;**编辑**&#x200B;以将其打开。

![演示](./images/cxapp3.png)

在您的CX App项目中，转到&#x200B;**集成**。 单击&#x200B;**选择环境**。

![演示](./images/cxapp3a.png)

选择在快速入门中创建的Adobe Experience Platform数据收集属性。 您需要选择名称中包含&#x200B;**(cx-app)**&#x200B;的属性。

![演示](./images/cxapp4.png)

你会看到这个。 单击&#x200B;**运行**。

![演示](./images/cxapp4a.png)

接下来，您需要选择一个身份和相应的命名空间，然后单击&#x200B;**搜索图标**。

![客户个人资料](./images/identities.png)

| 身份标识 | 命名空间 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 79943948563923140522865572770524243489 |
| Experience Cloud ID (ECID) | 70559351147248820114888181867542007989 |
| 电子邮件ID | woutervangeluwe+18112024-01@gmail.com |
| 手机号码ID | +32473622044+18112024-01 |

![演示](./images/19.png)

现在，您会看到最好显示在呼叫中心中的信息，以便呼叫中心工程师在与客户交谈时能够立即获得所有相关信息。

![演示](./images/20.png)

## 后续步骤

返回[实时客户个人资料](./real-time-customer-profile.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
