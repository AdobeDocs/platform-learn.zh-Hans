---
title: Bootcamp — 实时客户个人资料 — 从未知到网站上已知
description: Bootcamp — 实时客户个人资料 — 从未知到网站上已知
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 1.1从未知到网站上已知

## 上下文

从未知到已知的过程，以及客户从收购到维系的过程，是当今品牌圈最重要的主题之一。

Adobe Experience Platform在此历程中发挥着巨大作用。 平台是沟通的大脑， **体验记录系统**.

Platform是一个环境，在该环境中，客户一词不仅限于已知客户。 从Platform的角度来看，网站上的未知访客也是客户，因此，作为未知访客的所有行为也会发送到Platform。 凭借这种方法，当该访客最终成为已知客户时，品牌也可以可视化此时之前发生的事情。 这在归因和体验优化方面很有用。

## 客户历程流程

转到 [https://bootcamp.aepdemo.net](https://publish9122.adobedemo.com/content/aep-bootcamp-experience/language-masters/en.html). 单击 **全部允许**.

![DSN](./images/web8.png)

单击屏幕左上角的Adobe徽标图标以打开配置文件查看器。

![演示](./images/pv1.png)

请查看配置文件查看器面板和实时客户配置文件，其中包含 **EXPERIENCE CLOUDID** 用作该当前未知客户的主要标识符。

![演示](./images/pv2.png)

您还可以查看根据客户行为收集的所有体验事件。 该列表当前为空，但这种情况很快就会改变。

![演示](./images/pv3.png)

转到 **应用程序服务** 菜单选项，然后单击产品 **Real-Time CDP**.

![演示](./images/pv4.png)

然后，您将看到产品详细信息页面。 类型的体验事件 **产品查看** 已使用您在模块1中审查的Web SDK实施发送到Adobe Experience Platform。 打开配置文件查看器面板，并查看 **体验事件**.

![演示](./images/pv5.png)

转到 **应用程序服务** 菜单选项，然后单击产品 **Adobe Journey Optimizer**. 另一个Experience Event已发送到Adobe Experience Platform。

![演示](./images/pv7.png)

打开配置文件查看器面板。 您现在将看到2个类型的体验事件 **产品查看**. 虽然行为是匿名的，但每次点击都受到跟踪并存储在Adobe Experience Platform中。 一旦匿名客户被识别，我们便能够将所有匿名行为自动合并到已知配置文件中。

![演示](./images/pv8.png)

现在，让我们分析您的客户个人资料，然后使用您的行为在网站上个性化您的客户体验。

下一步： [1.2可视化您自己的实时客户个人资料 — UI](./ex2.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
