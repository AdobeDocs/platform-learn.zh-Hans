---
title: Adobe Journey Optimizer — 外部天气API、短信操作等 — 触发您编排的客户历程
description: Adobe Journey Optimizer — 外部天气API、短信操作等 — 触发您编排的客户历程
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 4d92877d-8fdc-4902-ad32-7fa068bc1395
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# 8.5触发您的历程

在本练习中，您将测试并触发您在此模块中配置的历程。

## 8.5.1更新地理围栏事件配置

转到 [Adobe Experience Platform数据收集](https://experience.adobe.com/launch/) 选择 **标记**.

这是您之前看到的Adobe Experience Platform数据收集属性页面。

![资产页面](../module1/images/launch1.png)

在模块0中，演示系统为您创建了两个客户端属性：一个用于网站，一个用于移动设备应用程序。 通过搜索来查找 `--demoProfileLdap--` 在 **[!UICONTROL 搜索]** 框中。 单击以打开 **Web** 属性。

![搜索框](../module1/images/property6.png)

然后你会看到这个。

![启动设置](./images/rule1.png)

在左侧菜单中，转到 **规则** 和搜索规则 **地理围栏事件**. 单击规则 **地理围栏事件** 打开它。

![启动设置](./images/rule2.png)

然后，您将看到此规则的详细信息。 单击以打开操作 **将“geofence event”发送到AEP — 触发JO**.

![启动设置](./images/rule3.png)

然后，您将看到触发此操作时，会使用特定的数据元素来定义XDM数据结构。 您需要更新该数据元素，并且您需要定义 **事件ID** 的 [练习8.1](./ex1.md).

![启动设置](./images/rule4.png)

您现在需要更新数据元素 **XDM — 地理围栏事件**. 要执行此操作，请转到 **数据元素**. 搜索 **XDM — 地理围栏事件** 并单击以打开该数据元素。

![启动设置](./images/rule5.png)

然后您将看到：

![启动设置](./images/rule6.png)

导航到字段 `_experience.campaign.orchestration.eventID`. 删除当前值，并将您的eventID粘贴到此处。

事件ID位于Adobe Journey Optimizer的 **“配置”>“事件”** 然后，您将在even的示例有效负载中找到事件ID，如下所示： `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

接下来，您应该在此数据元素中定义城市。 转到 **placeContext > geo > city** 然后进入一个选择的城市。 接下来，单击 **保存** 或 **保存到库**.

![ACOP](./images/payloadeventIDgeo.png)

最后，您需要发布更改。 转到 **发布流程** 中。

![启动设置](./images/rule8.png)

单击 **Add All Changed Resources** 然后单击 **保存并构建到开发环境**.

![启动设置](./images/rule9.png)

## 8.5.2触发您的历程

转到 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](../module0/images/web8.png)

在 **Screens** 页面，单击 **运行**.

![DSN](../module1/images/web2.png)

然后，您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../module0/images/web3.png)

打开新的隐身浏览器窗口。

![DSN](../module0/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../module0/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../module0/images/web6.png)

然后，您将在无痕浏览器窗口中看到您的网站已加载。 对于每个演示，您需要使用全新的、隐身的浏览器窗口来加载演示网站URL。

![DSN](../module0/images/web7.png)

单击屏幕左上角的Adobe徽标图标以打开“配置文件查看器”。

![演示](../module2/images/pv1.png)

查看“配置文件查看器”面板和“实时客户配置文件”，其中 **Experience CloudID** 作为此当前未知客户的主要标识符。

![演示](../module2/images/pv2.png)

转到注册/登录页面。 单击 **创建帐户**.

![演示](../module2/images/pv9.png)

填写详细信息并单击 **注册** 之后，您将被重定向到上一页。

![演示](../module2/images/pv10.png)

打开“配置文件查看器”面板，然后转到“实时客户配置文件”。 在“配置文件查看器”面板上，您应会看到显示的所有个人数据，如新添加的电子邮件和电话标识符。

![演示](../module2/images/pv11.png)

在“配置文件查看器”面板上，单击 **实用程序**. 输入 `geofenceevent` 单击 **发送**.

![演示](./images/smsdemo1.png)

几秒钟后，您将收到Adobe Journey Optimizer发来的短信。

![演示](./images/smsdemo4.png)

下一步： [摘要和优点](./summary.md)

[返回模块8](journey-orchestration-external-weather-api-sms.md)

[返回到所有模块](../../overview.md)
