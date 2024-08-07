---
title: Bootcamp — 实时客户资料 — 可视化您自己的实时客户资料 — UI
description: Bootcamp — 实时客户资料 — 可视化您自己的实时客户资料 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2可视化您自己的实时客户个人资料 — UI

在本练习中，您将登录到Adobe Experience Platform，并在UI中查看自己的实时客户个人资料。

## Story

在实时客户个人资料中，所有个人资料数据都与事件数据以及现有受众成员资格一起显示。 所显示的数据可以来自任何地方，包括Adobe应用程序和外部解决方案。 这是Adobe Experience Platform中最强大的视图，真正的体验记录体系。

## 1.2.1使用Adobe Experience Platform中的“客户配置文件”视图

转到[Adobe Experience Platform](https://experience.adobe.com/platform)。 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``Bootcamp``。 您可以通过单击屏幕顶部蓝线中的文本&#x200B;**[!UICONTROL Production Prod]**&#x200B;来执行此操作。 选择适当的[!UICONTROL 沙盒]后，您将看到屏幕更改，现在您已经进入专用的[!UICONTROL 沙盒]。



在左侧菜单中，转到&#x200B;**配置文件**&#x200B;和&#x200B;**浏览**。

![客户个人资料](./images/homemenu.png)

在网站上的“配置文件查看器”面板上，您可以找到身份概述。 每个身份都与命名空间关联。

![客户个人资料](./images/identities.png)




使用Adobe Experience Platform时，所有ID都同等重要。 以前，ECID是Adobe上下文中最重要的ID，所有其他ID都以分层关系链接到ECID。 在Adobe Experience Platform中，情况已发生了变化，每个ID都可以被视为主标识符。

通常，主要标识符取决于上下文。 如果您询问呼叫中心，**最重要的ID是什么？**&#x200B;他们可能会回答，**电话号码！**，但如果您询问您的CRM团队，他们会回答，**电子邮件地址！** Adobe Experience Platform了解这种复杂性并为您管理它。 每个应用程序(无论是Adobe应用程序还是非Adobe应用程序)都将通过引用它们视为主要的ID来与Adobe Experience Platform通信。 而且它只管管用。

对于字段&#x200B;**身份命名空间**，请选择&#x200B;**ECID**，对于字段&#x200B;**身份值**，请输入可在bootcamp网站的“配置文件查看器”面板中找到的ECID。 单击&#x200B;**查看**。 然后，您将在列表中看到您的个人资料。 单击&#x200B;**配置文件ID**&#x200B;以打开您的配置文件。

![客户个人资料](./images/popupecid.png)

您现在可以看到客户个人资料的几个重要&#x200B;**个人资料属性**&#x200B;的概述。

![客户个人资料](./images/profile.png)

转到&#x200B;**事件**，您可以在其中查看链接到个人资料的每个体验事件的条目。

![客户个人资料](./images/profileee.png)

最后，转到菜单选项&#x200B;**受众成员资格**。 您现在将看到符合此配置文件条件的所有受众。

![客户个人资料](./images/profileseg.png)

现在，让我们创建一个新受众，以便您为匿名客户或已知客户打造个性化的客户体验。

下一步： [1.3创建受众 — UI](./ex3.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
