---
title: Real-time CDP — 构建区段并采取操作 — 构建区段
description: Real-time CDP — 构建区段并采取操作 — 构建区段
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: c0778e81-4282-433d-9e02-37e32bf370ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---

# 6.1创建区段

在本练习中，您将通过使用Adobe Experience Platform的区段生成器来创建一个区段。

## 6.1.1上下文

在当今世界，对客户行为的响应需要是实时的。 实时响应客户行为的一种方法是，在区段符合实时条件的情况下，使用区段。 在本练习中，您需要构建一个区段，同时考虑到我们所使用的网站上的实际活动。

## 6.1.2识别您要对

转到 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](../module0/images/web8.png)

您现在可以按照以下流程访问网站。 单击 **集成**.

![DSN](../module0/images/web1.png)

在 **集成** 页面，您需要选择在练习0.1中创建的数据收集属性。

![DSN](../module0/images/web2.png)

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

在本例中，您希望对查看特定产品的特定客户做出响应。
从 **卢马** 主页，转到 **男**，然后单击产品 **PROTEUS健身长衫**.

![数据获取](./images/homenadia.png)

因此，当某人访问产品页面时 **PROTEUS健身长衫**，则您希望能够采取措施。 要执行操作，首先要定义区段。

![数据获取](./images/homenadiapp.png)

## 6.1.3创建区段

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](../module2/images/sb1.png)

在左侧的菜单中，转到 **区段** 然后转到 **浏览** 您可以在其中查看所有现有区段的概述。 单击 **创建区段** 按钮以开始创建新区段。

![区段](./images/menuseg.png)

如上所述，您需要根据已查看产品的所有客户构建一个区段 **PROTEUS健身长衫**.

要构建此区段，您需要添加事件。 通过单击 **事件** 图标 **区段** 菜单。

接下来，您将看到顶层 **XDM ExperienceEvent** 节点。

要查找已访问 **PROTEUS健身长衫** 产品，单击 **XDM ExperienceEvent**.

![区段](./images/findee.png)

向下滚动到 **产品列表项** 然后单击它。

![区段](./images/see.png)

选择 **名称** 拖放 **名称** 从左侧对象 **产品列表项** 菜单中的“区段生成器”画布，进入 **事件** 中。

![区段](./images/eewebpdtlname1.png)

比较参数应为 **等于** 在输入字段中，输入 `PROTEUS FITNESS JACKSHIRT`.

![区段](./images/pv.png)

您的 **事件规则** 现在应该是这样。 每次向区段生成器中添加元素时，您都可以单击 **刷新估计** 按钮以获取区段中的人口新估计。

![区段](./images/ldap4.png)

最后，让我们为区段提供一个名称并保存该名称。

作为命名约定，请使用：

- `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

您的区段名称应如下所示：
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

接下来，单击 **保存并关闭** 按钮来保存区段。

![区段](./images/segmentname.png)

此时您将返回到区段概述页面。

![区段](./images/savedsegment.png)

下一步： [6.2查看如何使用目标配置DV360目标](./ex2.md)

[返回到模块11](./real-time-cdp-build-a-segment-take-action.md)

[返回到所有模块](../../overview.md)
