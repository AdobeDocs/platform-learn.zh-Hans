---
title: Bootcamp — 将物理和数字相结合 — 使用移动应用程序并触发信标条目
description: Bootcamp — 将物理和数字相结合 — 使用移动应用程序并触发信标条目
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Mobile SDK
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 3.1使用移动设备应用程序并触发信标条目

## 安装移动应用程序

在安装应用之前，您需要在iOS设备上启用&#x200B;**跟踪**。 为此，请转到&#x200B;**设置** > **隐私和安全性** > **跟踪**，并确保选项&#x200B;**允许应用程序请求跟踪**。

![DSN](./../uc3/images/app4.png)

转到Apple App Store并搜索`aepmobile-bootcamp`。 单击&#x200B;**安装**&#x200B;或&#x200B;**下载**。

![DSN](./../uc3/images/app1.png)

安装应用后，单击&#x200B;**打开**。

![DSN](./../uc3/images/app2.png)

单击&#x200B;**确定**。

![DSN](./../uc3/images/app9.png)

单击&#x200B;**允许**。

![DSN](./../uc3/images/app3.png)

单击&#x200B;**我同意**。

![DSN](./../uc3/images/app7.png)

使用应用&#x200B;**时单击**&#x200B;允许。

![DSN](./../uc3/images/app8.png)

单击&#x200B;**允许**。

![DSN](./../uc3/images/app5.png)

现在，您位于应用程序的主页上，可以随时了解客户历程。

![DSN](./../uc3/images/app12.png)

## 客户历程流程

首先，您需要登录。 单击&#x200B;**登录**。

![DSN](./images/app13.png)

在前面的练习中创建帐户后，您会在网站上看到此内容。 现在，您需要重新使用在应用程序中创建的帐户电子邮件地址来登录。

![演示](./images/pv1.png)

在此处输入您在网站上使用的电子邮件地址，然后单击&#x200B;**登录**。

![DSN](./images/app14.png)

然后，您会收到一个确认您已登录的邮件，并且您会收到一个推送通知。

![DSN](./images/app15.png)

返回应用程序中的主页，您将看到其他功能。

![DSN](./images/app17.png)

首先，转到&#x200B;**产品**。 单击任何产品，在本例中为&#x200B;**Coffee to go**。

![DSN](./images/app19.png)

您将在应用程序中看到&#x200B;**Coffee to go**&#x200B;产品页面。

![DSN](./images/app20.png)

现在，您将在离线商店位置中模拟信标进入事件。 模拟这一过程的目标是在店内屏幕上使客户体验个性化。 为了直观显示店内体验，已创建了一个页面，该页面将动态显示与刚刚进入商店的客户相关的信息。

在继续之前，请在计算机上打开此网页： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

您随后将看到以下内容：

![DSN](./images/screen1.png)

接下来，返回主页。 单击&#x200B;**信标**&#x200B;图标。

![DSN](./images/app23.png)

你会看到这个。 首先，选择&#x200B;**Bootcamp屏幕信标**，然后单击&#x200B;**条目**&#x200B;按钮。 这将允许您模拟信标条目。

![DSN](./images/app21.png)

现在，看看店内屏幕。 5秒内，您将看到您查看的最后一个产品显示在该处。

![DSN](./images/screen2.png)

然后，返回&#x200B;**产品**。 单击任何产品，在本例中为&#x200B;**Beach blanket Tan**。

![DSN](./images/app22.png)

接下来，返回主页。 单击&#x200B;**信标**&#x200B;图标。

![DSN](./images/app23.png)

你会看到这个。 首先，选择&#x200B;**Bootcamp屏幕信标**，然后再次单击&#x200B;**条目**&#x200B;按钮。 这将允许您模拟信标条目。

![DSN](./images/app21.png)

现在，再次查看店内屏幕。 5秒内，您将看到您查看的最后一个产品显示在该处。

![DSN](./images/screen3.png)

现在，我们还可以查看您网站上的配置文件查看器。 您将看到许多添加到那里的事件，只是为了显示与客户的任何交互都收集并存储在Adobe Experience Platform中。

![DSN](./images/screen4.png)

在接下来的练习中，您将配置和测试自己的信标进入历程。

下一步： [3.2创建您的事件](./ex2.md)

[返回用户流程3](./uc3.md)

[返回所有模块](../../overview.md)
