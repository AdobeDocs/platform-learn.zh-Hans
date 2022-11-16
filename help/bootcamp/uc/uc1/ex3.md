---
title: Bootcamp — 实时客户资料 — 创建区段 — UI
description: Bootcamp — 实时客户资料 — 创建区段 — UI
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# 1.3创建区段 — UI

在本练习中，您将通过使用Adobe Experience Platform的区段生成器来创建一个区段。

## Story

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧的菜单中，转到 **区段**. 在此页面上，您可以看到所有现有区段的概述。 单击 **+创建区段** 按钮以开始创建新区段。

![区段](./images/menuseg.png)

进入新区段生成器后，您会立即注意到 **属性** 菜单选项和 **XDM个人配置文件** 引用。

![区段](./images/segmentationui.png)

由于XDM是支持体验业务的语言，因此XDM也是区段生成器的基础。 在Platform中摄取的所有数据都应当针对XDM进行映射，因此，无论数据来自何处，所有数据都将成为同一数据模型的一部分。 这为您在生成区段时提供了很大的优势，因为通过这个区段生成器UI，您可以在同一工作流中合并来自任何来源的数据。 可以在区段生成器中构建的区段可以发送到Adobe Target、Adobe Campaign和Adobe Audience Manager等解决方案以进行激活。

现在，您需要为已查看产品的所有客户创建一个区段 **Real-Time CDP**.

要构建此区段，您需要添加体验事件。 您可以通过单击 **事件** 图标 **字段** 菜单。

![区段](./images/findee.png)

接下来，你将看到顶层， **XDM ExperienceEvents** 节点。 单击 **XDM ExperienceEvent**.

![区段](./images/see.png)

转到 **产品列表项**.

![区段](./images/plitems.png)

选择 **名称** 拖放 **名称** 对象（从左侧菜单转到区段生成器画布中） **事件** 中。 然后您将看到：

![区段](./images/eewebpdtlname.png)

比较参数应为 **等于** 在输入字段中，输入 **Real-time CDP**.

![区段](./images/pv.png)

每次向区段生成器中添加元素时，您都可以单击 **刷新估计** 按钮以获取区段中的人口新估计。

![区段](./images/refreshest.png)

作为 **评价方法**，选择 **Edge**.

![区段](./images/evedge.png)

最后，让我们为区段提供一个名称并保存该名称。

作为命名约定，请使用：

- `yourLastName - Interest in Real-Time CDP`

然后，单击 **保存并关闭** 按钮来保存区段。

![区段](./images/segmentname.png)

此时您将返回到区段概述页面，在该页面中，您将看到符合区段资格的客户配置文件预览示例。

![区段](./images/savedsegment.png)

您现在可以继续下一个练习，并将区段用于Adobe Target。

下一步： [1.4采取行动：将区段发送到Adobe Target](./ex4.md)

[返回到用户流量1](./uc1.md)

[返回到所有模块](../../overview.md)
