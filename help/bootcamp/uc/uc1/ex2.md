---
title: Bootcamp — 实时客户资料 — 可视化您自己的实时客户资料 — UI
description: Bootcamp — 实时客户资料 — 可视化您自己的实时客户资料 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 0474808b42925bf95529e10a42a0563f0ecc43b8
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# 1.2可视化您自己的实时客户个人资料 — UI

在本练习中，您将登录到Adobe Experience Platform，并在UI中查看自己的实时客户个人资料。

## Story

在实时客户个人资料中，所有个人资料数据都与事件数据以及现有受众成员资格一起显示。 所显示的数据可以来自任何地方，包括Adobe应用程序和外部解决方案。 这是Adobe Experience Platform中最强大的视图，真正的体验记录体系。

## 1.2.1使用Adobe Experience Platform中的“客户配置文件”视图

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击文本来执行此操作 **[!UICONTROL 生产生产]** 在屏幕顶部的蓝线上。 选择适当的 [!UICONTROL 沙盒]，您将会看到屏幕更改，现在您已进入专用页面 [!UICONTROL 沙盒].



在左侧菜单中，转到 **配置文件** 和 **浏览**.

![客户配置文件](./images/homemenu.png)

在网站上的“配置文件查看器”面板上，您可以找到身份概述。 每个身份都与命名空间关联。

![客户配置文件](./images/identities.png)


在“配置文件查看器”面板上，您当前可以看到此标识：

| 命名空间 | 标识 |
|:-------------:| :---------------:|
| Experience CloudID (ECID) | 19428085896177382402834560825640259081 |

使用Adobe Experience Platform时，所有ID都同等重要。 以前，ECID是Adobe上下文中最重要的ID，所有其他ID都以分层关系链接到ECID。 在Adobe Experience Platform中，情况已发生了变化，每个ID都可以被视为主标识符。

通常，主要标识符取决于上下文。 如果你问你的呼叫中心， **最重要的ID是什么？** 他们可能会回答， **电话号码！** 但如果您询问您的CRM团队，他们会回答， **电子邮件地址！**  Adobe Experience Platform了解这种复杂性并为您进行管理。 每个应用程序(无论是Adobe应用程序还是非Adobe应用程序)都将通过引用它们视为主要的ID来与Adobe Experience Platform通信。 而且它只管管用。

对于字段 **身份命名空间**，选择 **ECID** 和字段 **标识值** 输入您可在bootcamp网站的Profile Viewer面板中找到的ECID。 单击 **视图**. 然后，您将在列表中看到您的个人资料。 单击 **配置文件ID** 以打开您的个人资料。

![客户配置文件](./images/popupecid.png)

您现在可以看到几个重要内容的概述 **配置文件属性** ，以了解您的客户资料。

![客户配置文件](./images/profile.png)

转到 **活动**，您可以在此处查看链接到用户档案的每个体验事件的条目。

![客户配置文件](./images/profileee.png)

最后，转到菜单选项 **受众会员资格**. 您现在将看到符合此配置文件条件的所有受众。

![客户配置文件](./images/profileseg.png)

现在，让我们创建一个新受众，以便您为匿名客户或已知客户打造个性化的客户体验。

下一步： [1.3创建受众 — UI](./ex3.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
