---
title: Bootcamp — 实时客户资料 — 可视化您自己的实时客户资料 — UI
description: Bootcamp — 实时客户资料 — 可视化您自己的实时客户资料 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 1.2可视化您自己的Real-time Customer Profile - UI

在本练习中，您将登录到Adobe Experience Platform并在UI中查看自己的Real-time Customer Profile。

## Story

在Real-time Customer Profile中，所有配置文件数据都与事件数据以及现有区段成员资格一起显示。 所显示的数据可以来自任何地方，来自Adobe应用程序和外部解决方案。 这是Adobe Experience Platform中最强大的视图，真正的体验记录体系。

## 1.2.1使用Adobe Experience Platform中的客户配置文件视图

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击文本来执行此操作 **[!UICONTROL 生产产品]** 在屏幕顶部的蓝线上。 选择适当的 [!UICONTROL 沙盒]，您会看到屏幕更改，现在您已专心致志地工作 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧菜单中，转到 **配置文件** 和 **浏览**.

![客户配置文件](./images/homemenu.png)

在您网站上的“配置文件查看器”面板上，您可以找到身份概述。 每个身份都链接到命名空间。

![客户配置文件](./images/identities.png)

在“配置文件查看器”面板上，您当前可以看到此标识：

| 命名空间 | 标识 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

使用Adobe Experience Platform时，所有ID都同等重要。 以前，ECID是Adobe上下文中最重要的ID，所有其他ID都以层次结构关系链接到ECID。 在Adobe Experience Platform中，情况已发生了变化，每个ID都可视为主标识符。

通常，主要标识符取决于上下文。 如果你问你的呼叫中心， **最重要的ID是什么？** 他们可能会回答， **电话号码！** 但是，如果您询问您的CRM团队，他们会回答， **电子邮件地址！**  Adobe Experience Platform了解这种复杂性并为您管理它。 每个应用程序(无论是Adobe应用程序还是非Adobe应用程序)都将通过引用它们视为主要的ID与Adobe Experience Platform通信。 而且它只是起作用的。

对于字段 **身份命名空间**，选择 **ECID** 对于字段，为 **标识值** 输入您可在bootcamp网站的Profile Viewer面板中找到的ECID。 单击 **视图**. 然后，您将在列表中看到您的个人资料。 单击 **配置文件ID** 以打开您的个人资料。

![客户配置文件](./images/popupecid.png)

您现在可以看到几个重要内容的概述 **配置文件属性** ，以了解您的客户资料。

![客户配置文件](./images/profile.png)

转到 **事件**，您可以在此处查看链接到用户档案的每个体验事件的条目。

![客户配置文件](./images/profileee.png)

最后，转到菜单选项 **区段成员资格**. 现在，您将看到所有符合此用户档案条件的区段。

![客户配置文件](./images/profileseg.png)

现在，让我们创建一个新区段，以便您能够为匿名或知情的客户个性化客户体验。

下一步： [1.3创建区段 — UI](./ex3.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
