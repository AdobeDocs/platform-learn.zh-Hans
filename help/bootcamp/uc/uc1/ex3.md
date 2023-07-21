---
title: Bootcamp — 实时客户个人资料 — 创建区段 — UI
description: Bootcamp — 实时客户个人资料 — 创建区段 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# 1.3创建区段 — UI

在本练习中，您将使用Adobe Experience Platform的区段生成器创建一个区段。

## Story

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击文本来执行此操作 **[!UICONTROL 生产产品]** 在屏幕顶部的蓝线上。 选择适当的 [!UICONTROL 沙盒]，您会看到屏幕更改，现在您已专心致志地工作 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧的菜单中，转到 **区段**. 在此页面上，您可以看到所有现有区段的概述。 单击 **+创建区段** 按钮开始创建新区段。

![区段](./images/menuseg.png)

进入新的区段生成器后，您会立即注意到 **属性** 菜单选项和 **XDM个人资料** 引用。

![区段](./images/segmentationui.png)

由于XDM是支持体验业务的语言，因此XDM也是区段生成器的基础。 在Platform中引入的所有数据都应根据XDM进行映射，因此，无论数据来自何处，所有数据都会成为同一数据模型的一部分。 这为构建区段提供了很大的优势，例如，从这个区段生成器UI中，您可以在同一工作流中组合来自任何源的数据。 在Segment Builder中构建的区段可以发送到Adobe Target、Adobe Campaign和Adobe Audience Manager等解决方案以供激活。

您现在需要创建一个已查看产品的所有客户的区段 **Real-Time CDP**.

要构建此区段，您需要添加一个体验事件。 您可以通过单击 **事件** 中的图标 **字段** 菜单栏。

![区段](./images/findee.png)

接下来，您将看到顶层， **XDM ExperienceEvents** 节点。 单击 **XDM ExperienceEvent**.

![区段](./images/see.png)

转到 **产品列表项**.

![区段](./images/plitems.png)

选择 **名称** 并拖放 **名称** 对象从左侧菜单转到区段生成器画布中的 **事件** 部分。 您随后将看到以下内容：

![区段](./images/eewebpdtlname.png)

比较参数应为 **等于** 在输入字段中，输入 **Real-time CDP**.

![区段](./images/pv.png)

每次将元素添加到区段生成器时，您都可以单击 **刷新估计** 按钮以获取区段中的群体的新估计值。

![区段](./images/refreshest.png)

作为 **评估方法**，选择 **Edge**.

![区段](./images/evedge.png)

最后，让我们为您的区段命名并保存它。

作为命名约定，请使用：

- `yourLastName - Interest in Real-Time CDP`

然后，单击 **保存并关闭** 按钮以保存区段。

![区段](./images/segmentname.png)

现在，您将返回到区段概述页面，在该页面中，您将看到符合区段条件的客户配置文件预览示例。

![区段](./images/savedsegment.png)

现在，您可以继续下一个练习，并将您的区段用于Adobe Target。

下一步： [1.4采取行动：将您的区段发送到Adobe Target](./ex4.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
