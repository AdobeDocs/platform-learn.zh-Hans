---
title: 基础 — 实时客户资料 — 可视化您自己的实时客户资料 — UI
description: 基础 — 实时客户资料 — 可视化您自己的实时客户资料 — UI
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: ed13e37f-48eb-4668-b828-6c58340a7cc1
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---

# 3.2可视化您自己的实时客户用户档案 — UI

在本练习中，您将登录Adobe Experience Platform，并在UI中查看您自己的实时客户资料。

## Story

在“实时客户资料”中，所有资料数据都与事件数据以及现有区段成员资格一起显示。 显示的数据可以从任何位置、Adobe应用程序和外部解决方案获取。 这是Adobe Experience Platform最有力的观点，真正的体验体系。

## 3.2.1使用Adobe Experience Platform中的“客户配置文件视图”

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](../module2/images/sb1.png)

在左侧菜单中，转到 **用户档案** 和 **浏览**.

![客户资料](./images/homemenu.png)

在您网站的“配置文件查看器”面板上，您可以找到多个身份。 每个身份都链接到一个命名空间。

![客户资料](./images/identities.png)

在“配置文件查看器”面板上，您可以看到ID和命名空间的以下组合：

| 标识 | 命名空间 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| 电子邮件ID | woutervangeluwe+06022022-01@gmail.com |
| 手机号码ID | +32473622044+06022022-01 |

有了Adobe Experience Platform，所有ID都同样重要。 以前，ECID是Adobe上下文中最重要的ID，所有其他ID都以层级关系链接到ECID。 对于Adobe Experience Platform，情况已不再如此，并且每个ID都可以被视为主要标识符。

通常，主标识符取决于上下文。 如果你问你的呼叫中心， **最重要的ID是什么？** 他们可能会回答， **电话号码！** 但如果你问你的CRM团队，他们会回答， **电子邮件地址！**  Adobe Experience Platform理解这种复杂性，并为您进行管理。 每个应用程序(无论是Adobe应用程序还是非Adobe应用程序)都将通过引用它们视为主ID来与Adobe Experience Platform沟通。 它很管用。

对于字段 **身份命名空间**，选择 **电子邮件** 和 **标识值** 输入您在上一个练习中用于注册的电子邮件地址。 单击 **查看**. 然后，您会在列表中看到您的个人资料。 单击 **配置文件ID** 以打开您的个人资料。

![客户资料](./images/popupecid.png)

现在，您将看到以下几个重要 **配置文件属性** 客户资料。

![客户资料](./images/profile.png)

如果要查看配置文件的所有可用配置文件属性，请转到 **属性**.

![客户资料](./images/profilattr.png)

转到 **事件**，您可以在其中查看链接到用户档案的每个体验事件的条目。

![客户资料](./images/profileee.png)

最后，转到菜单选项 **区段成员资格**. 现在，您将看到符合此用户档案资格的所有区段。

![客户资料](./images/profileseg.png)

现在，您已了解如何通过使用Adobe Experience Platform的用户界面查看任何客户的实时用户档案，接下来让我们通过API通过利用Postman和Adobe I/O对Adobe Experience Platform API进行查询来执行相同的操作。

下一步： [3.3可视化您自己的实时客户资料 — API](./ex3.md)

[返回到模块3](./real-time-customer-profile.md)

[返回到所有模块](../../overview.md)
