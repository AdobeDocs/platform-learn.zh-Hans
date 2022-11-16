---
title: Bootcamp — 呼叫中心中的个性化
description: Bootcamp — 呼叫中心中的个性化
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: f7697673-38f9-41f6-ac4d-2561db2ece67
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 2.6呼叫中心中的个性化

正如在引导营销期间多次讨论的，个性化客户体验应以全渠道方式实现。 呼叫中心通常与客户历程的其余部分非常脱节，这通常会导致令人沮丧的客户体验，但不需要。 让我们为您展示一个示例，说明呼叫中心如何能够轻松实时连接到Adobe Experience Platform。

## 客户历程流

在上一个练习中，使用移动应用程序，您通过单击 **购买** 按钮。

![DSN](./images/app20.png)

假设您对订单状态有疑问，您会怎么做？ 通常您会呼叫呼叫中心。

在呼叫呼叫中心之前，您需要了解 **忠诚度ID**. 您可以在网站的用户档案查看器中找到您的忠诚度ID。

![DSN](./images/cc1.png)

在本例中， **忠诚度ID** is **5863105**. 在演示环境中作为呼叫中心功能的自定义实施的一部分，您需要在 **忠诚度ID**. 前缀为 **11373**，因此在此示例中使用的忠诚度ID是 **11373 5863105**.

现在就开始吧。 用你的电话打电话 **+1(323)745-1670**.

![DSN](./images/cc2.png)

系统将要求您输入忠诚度ID，然后 **#**. 输入您的忠诚度ID。

![DSN](./images/cc3.png)

然后你会听到 **你好，名字**. 该名字取自Adobe Experience Platform的实时客户资料。 然后有3种选择。 按号 **1**, **订单状态**.

![DSN](./images/cc4.png)

听到您的订单状态后，您将可以选择按 **1** 要返回主菜单或其他，请按2。 按 **2**.

![DSN](./images/cc5.png)

然后，系统将要求您通过选择介于1到5之间、1为低且5为高的数字来对呼叫中心体验进行评级。 做出选择。

![DSN](./images/cc6.png)

您呼叫呼叫中心的呼叫现在将结束。

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧菜单中，转到 **用户档案** 和 **浏览**.

![客户资料](./images/homemenu.png)

选择 **身份命名空间** **电子邮件** 并输入客户用户档案的电子邮件地址。 单击 **查看**. 单击以打开您的用户档案。

![DSN](./images/cc7.png)

您将再次看到客户资料。 转到 **事件**.

![DSN](./images/cc8.png)

在events下，您将看到2个events，其eventType为 **callCenter**. 第一个事件是您对问题的回答的结果 **给您的电话满意度打分**.

![DSN](./images/cc9.png)

向下滚动一点，您将看到在选择选项以检查 **订单状态**.

![DSN](./images/cc10.png)

转到 **区段成员资格**. 现在，您将根据您通过呼叫中心进行的交互，实时看到配置文件中有2个区段符合条件。 这些区段成员关系随后可用于影响任何其他渠道间的通信和个性化情况。

![DSN](./images/cc11.png)

你现在已经完成了这个练习。

[返回到用户流量2](./uc2.md)

[返回到所有模块](../../overview.md)
