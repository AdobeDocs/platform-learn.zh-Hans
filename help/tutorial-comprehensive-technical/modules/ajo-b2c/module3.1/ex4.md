---
title: 更新配置ID并测试历程
description: 更新配置ID并测试历程
kt: 5342
doc-type: tutorial
source-git-commit: 2bd4249d96eb697da66db68895761f8b0bd6e638
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---

# 3.1.3更新您的数据收集属性并测试您的历程

## 3.1.3.1更新您的数据收集属性

转到[Adobe Experience Platform数据收集](https://experience.adobe.com/launch/)并选择&#x200B;**标记**。

![属性页](./../../../modules/datacollection/module1.1/images/launch1.png)

在&#x200B;**快速入门**&#x200B;中，演示系统为您创建了两个客户端属性：一个用于网站，另一个用于移动应用程序。 通过在&#x200B;**[!UICONTROL 搜索]**&#x200B;框中搜索`--aepUserLdap--`来查找它们。 单击以打开&#x200B;**Web**&#x200B;属性。

![搜索框](./../../../modules/datacollection/module1.1/images/property6.png)

你会看到这个。

![启动安装程序](./images/rule1.png)

在左侧菜单中，转到&#x200B;**规则**&#x200B;并搜索规则&#x200B;**创建帐户**。 单击规则&#x200B;**创建帐户**&#x200B;以将其打开。

![启动安装程序](./images/rule2.png)

然后，您将看到此规则的详细信息。 单击以打开操作&#x200B;**发送“注册事件”体验事件**。

![启动安装程序](./images/rule3.png)

然后，您会看到在触发此操作时，将使用特定的数据元素来定义XDM数据结构。 您需要更新该数据元素，并且需要定义您在[练习3.1.1](./ex1.md)中配置的事件的&#x200B;**事件ID**。

![启动安装程序](./images/rule4.png)

您现在需要更新数据元素&#x200B;**XDM — 注册事件**。 为此，请转到&#x200B;**数据元素**。 搜索&#x200B;**XDM — 注册**，然后单击以打开该数据元素。

![启动安装程序](./images/rule5.png)

您随后将看到以下内容：

![启动安装程序](./images/rule6.png)

导航到字段`_experience.campaign.orchestration.eventID`。 删除当前值，并将您的eventID粘贴到该处。

提醒一下，您可以在Adobe Journey Optimizer中的&#x200B;**配置>事件**&#x200B;下找到事件ID，您还可以在事件有效负荷中找到事件ID，如下所示： `"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`。

![ACOP](./images/payloadeventID.png)

粘贴eventID后，屏幕应如下所示。 接下来，单击&#x200B;**保存**&#x200B;或&#x200B;**保存到库**。

![启动安装程序](./images/rule7.png)

最后，您需要发布更改。 在左侧菜单中转到&#x200B;**发布流**，然后单击以打开您的&#x200B;**Main**&#x200B;库。

![启动安装程序](./images/rule8.png)

单击&#x200B;**添加所有更改的资源**，然后单击&#x200B;**保存并生成到开发**。

![启动安装程序](./images/rule9.png)

随后将更新您的库，1-2分钟后，您可以继续测试您的配置。

## 3.1.3.2测试您的历程

转到[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登录后，您将看到此内容。 单击网站项目上的3个点&#x200B;**...**，然后单击&#x200B;**运行**&#x200B;以将其打开。

![DSN](./../../datacollection/module1.1/images/web8.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个练习，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

单击屏幕左上角的Adobe徽标图标以打开配置文件查看器。

![演示](./../../../modules/datacollection/module1.2/images/pv1.png)

请查看配置文件查看器面板和实时客户配置文件，将&#x200B;**Experience CloudID**&#x200B;作为此当前未知客户的主要标识符。 单击&#x200B;**登录**。

![演示](./../../../modules/datacollection/module1.2/images/pv2.png)

单击&#x200B;**创建帐户**。

![演示](./../../../modules/datacollection/module1.2/images/pv9.png)

填写您的详细信息，然后单击&#x200B;**注册**，之后您将被重定向到上一页。

![演示](./../../../modules/datacollection/module1.2/images/pv10.png)

打开配置文件查看器面板，然后转到Real-time Customer Profile。 在“配置文件查看器”面板上，您应该会看到所有显示的个人数据，如新添加的电子邮件和电话标识符。

![演示](./../../../modules/datacollection/module1.2/images/pv11.png)

创建帐户1分钟后，您将收到来自Adobe Journey Optimizer的帐户创建电子邮件。

![启动安装程序](./images/email.png)

您还将在Journey Optimizer中的旅程仪表板上看到旅程条目和旅程进度。

![启动安装程序](./images/emaildash.png)

下一步：[摘要和优点](./summary.md)

[返回模块3.1](./journey-orchestration-create-account.md)

[返回所有模块](../../../overview.md)
