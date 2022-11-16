---
title: 请在呼叫中心查看您的实时客户资料
description: 请在呼叫中心查看您的实时客户资料
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 457347ca-1ce5-4699-bd30-735abdc7b450
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# 3.6在呼叫中心查看您的实时客户资料

在本练习中，您的目标是让您体验客户历程，并像真正的客户一样行事。

在这个网站上，我们实施了Adobe Experience Platform。 每项操作都会被视为体验事件，并会实时发送到Adobe Experience Platform，从而消除实时客户资料。

在之前的一个练习中，您最初是匿名客户，他正在浏览网站，几步之后，您便成为了知名客户。

当同一客户最终拿起电话并致电您的呼叫中心时，必须立即提供来自其他渠道的信息，以便呼叫中心的体验能够相关且个性化。

## 3.6.1使用您的CX应用程序

作为演示系统的一部分，我们创建了一个CX应用程序模板，可用于模拟呼叫中心环境。 按照以下步骤创建此类CX应用程序项目。

转到 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 单击 **新建项目**.

然后，您将看到您的CX应用程序项目。 单击项目以将其打开。

![演示](./images/cxapp3.png)

在您的CX应用程序项目中，转到 **集成**. 选择在模块0中创建的Adobe Experience Platform数据收集属性。 您需要选择具有 **（启用）** 以它的名称。 然后，单击 **运行**.

![演示](./images/cxapp4.png)

然后你会看到这个。

![演示](./images/cxapp5.png)

在“配置文件查看器”面板上，您可以看到ID和命名空间的以下组合：

![客户资料](./images/identities.png)

| 标识 | 命名空间 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| 电子邮件ID | woutervangeluwe+06022022-01@gmail.com |
| 手机号码ID | +32473622044+06022022-01 |

当客户致电您的呼叫中心时，可使用电话号码来识别客户。 因此，在本练习中，您将使用电话号码来检索CX应用程序中客户的配置文件。

选择 **电话号码** 在下拉菜单中，输入您在网站上使用的电话号码。 点击 **输入**.

![演示](./images/19.png)

现在，您将看到理想情况下会显示在呼叫中心的信息，以便呼叫中心员工在与客户交谈时可以立即获得所有相关信息。

![演示](./images/20.png)

下一步： [摘要和优点](./summary.md)

[返回到模块3](./real-time-customer-profile.md)

[返回到所有模块](../../overview.md)
