---
title: Foundation - Real-time Customer Profile — 从未知到网站上已知
description: Foundation - Real-time Customer Profile — 从未知到网站上已知
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 2%

---

# 2.1.1从未知到网站上已知

## 上下文

从未知到已知的过程，以及客户从收购到维系的过程，是当今品牌圈最重要的主题之一。

Adobe Experience Platform在此历程中发挥着巨大作用。 Platform是沟通的大脑，是“记录体验系统”。

Platform是一个环境，在该环境中，客户一词不仅限于已知客户。 从Platform的角度来看，网站上的未知访客也是客户，因此，作为未知访客的所有行为也会发送到Platform。 凭借这种方法，当该访客最终成为已知客户时，品牌也可以可视化此时之前发生的事情。 这在归因和体验优化方面很有用。

## 客户历程流程

转到[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

在&#x200B;**Screens**&#x200B;页面上，单击&#x200B;**运行**。

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个演示，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

单击屏幕左上角的Adobe徽标图标以打开配置文件查看器。

![演示](../../datacollection/module1.2/images/pv1.png)

请查看配置文件查看器面板和实时客户配置文件，将&#x200B;**Experience CloudID**&#x200B;作为当前未知客户的主要标识符。

![演示](../../datacollection/module1.2/images/pv2.png)

您还可以查看根据客户行为收集的所有体验事件。 该列表当前为空，但这种情况很快就会改变。

![演示](../../datacollection/module1.2/images/pv3.png)

转到&#x200B;**Men**&#x200B;产品类别。 接下来，单击产品&#x200B;**Montana防风夹克**。

![演示](../../datacollection/module1.2/images/pv4.png)

然后，您将看到产品详细信息页面。 使用您在模块1中审查的Web SDK实现，现已将&#x200B;**产品视图**&#x200B;类型的Experience Event发送到Adobe Experience Platform。

![演示](../../datacollection/module1.2/images/pv5.png)

打开“配置文件查看器”面板，并查看您的&#x200B;**体验事件**。

![演示](../../datacollection/module1.2/images/pv6.png)

返回&#x200B;**女性**&#x200B;类别页面，然后单击其他产品。 另一个Experience Event已发送到Adobe Experience Platform。

![演示](../../datacollection/module1.2/images/pv7.png)

打开配置文件查看器面板。 您现在将看到2个&#x200B;**产品视图**&#x200B;类型的体验事件。 虽然行为是匿名的，但我们能够跟踪每次点击并将其存储在Adobe Experience Platform中。 一旦匿名客户被识别，我们便能够将所有匿名行为自动合并到已知配置文件中。

![演示](../../datacollection/module1.2/images/pv8.png)

转到“注册/登录”页面。 单击&#x200B;**创建帐户**。

![演示](../../datacollection/module1.2/images/pv9.png)

填写您的详细信息，然后单击&#x200B;**注册**，之后您将被重定向到上一页。

![演示](../../datacollection/module1.2/images/pv10.png)

打开配置文件查看器面板，然后转到Real-time Customer Profile。 在“配置文件查看器”面板上，您应该会看到所有显示的个人数据，如新添加的电子邮件和电话标识符。

![演示](../../datacollection/module1.2/images/pv11.png)

在配置文件查看器面板上，转到体验事件。 您将会在配置文件查看器面板上看到之前查看的2个产品。 这两个事件现在也关联到您的“已知”配置文件。

![演示](../../datacollection/module1.2/images/pv12.png)

现在，您已将数据摄取到Adobe Experience Platform，并且已将该数据关联到ECID和电子邮件地址等标识符。 这样做的目的是为了了解您打算做什么的业务环境。 在下一个练习中，您将开始配置所需的一切配置，以便能够进行所有的数据摄取。

### 在移动设备应用程序中导航

在成为已知客户后，该开始使用移动设备应用程序了。 在iPhone上打开移动设备应用程序，然后登录该应用程序。

如果您不再安装该应用，或者忘记如何安装，请在此处查看： [0.5使用移动应用](../../gettingstarted/gettingstarted/ex5.md)

按照说明安装应用程序后，您将看到已加载Luma品牌的应用程序的登陆页面。 单击屏幕左上方的帐户图标。

![演示](./images/app_hp.png)

在“登录”屏幕上，使用您在桌面网站上使用的电子邮件地址登录。 单击&#x200B;**登录**。

![演示](./images/app_acc.png)

转到应用程序的主屏幕，然后单击以打开任何产品。

![演示](./images/app_hp.png)

然后，您将看到产品详细信息页面。

![演示](./images/app_carst.png)

转到应用程序的主屏幕，并向左轻扫屏幕以查看“配置文件查看器”面板。 然后，您将在&#x200B;**体验事件**&#x200B;部分中看到您刚才查看的产品，以及之前网站会话中的所有产品查看。

![演示](./images/app_after_carst.png)

现在，返回桌面计算机并刷新主页，之后您也会看到该产品。

![演示](./images/lb_x_aftermobile.png)

现在，您已将数据摄取到Adobe Experience Platform，并且已将该数据关联到ECID和电子邮件地址等标识符。 本练习的目标是了解您即将执行的操作的业务环境。 现在，您已经有效地构建了一个实时、跨设备的客户档案。 在下一个练习中，您将继续在Adobe Experience Platform中可视化您的个人资料。

下一步：[2.1.2可视化您自己的实时客户个人资料 — UI](./ex2.md)

[返回模块2.1](./real-time-customer-profile.md)

[返回所有模块](../../../overview.md)
