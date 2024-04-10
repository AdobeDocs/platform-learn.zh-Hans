---
title: Bootcamp — 实时客户个人资料 — 创建受众 — UI
description: Bootcamp — 实时客户个人资料 — 创建受众 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 0474808b42925bf95529e10a42a0563f0ecc43b8
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3创建受众 — UI

在本练习中，您将使用Adobe Experience Platform的Audience Builder创建一个受众。

## Story

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击文本来执行此操作 **[!UICONTROL 生产生产]** 在屏幕顶部的蓝线上。 选择适当的 [!UICONTROL 沙盒]，您将会看到屏幕更改，现在您已进入专用页面 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧的菜单中，转到 **受众**. 在此页面上，您将看到功能板，其中包含有关以下内容的基本信息 **受众** 性能。

![区段](./images/menuseg.png)

单击 **浏览** 查看所有现有受众的概述。 单击 **+创建受众** 按钮开始创建新受众。


![区段](./images/segmentationui.png)

此时将显示一个弹出窗口，询问您是否要执行以下操作 **&#39;组合受众&#39;** 或 **&#39;生成规则&#39;**. 选择 **&#39;生成规则&#39;** 以继续，然后单击 **创建**.

![区段][def]

进入受众生成器后，您会立即注意到 **属性** 菜单选项和 **XDM个人资料** 引用。


由于XDM是支持体验业务的语言，因此XDM也是受众生成器的基础。 在Platform中引入的所有数据都应根据XDM进行映射，因此，无论数据来自何处，所有数据都会成为同一数据模型的一部分。 这为您在构建受众时提供了很大的优势，因为从这个受众生成器UI中，您可以在同一个工作流中组合来自任何来源的数据。 在Audience Builder中构建的受众可以发送到Adobe Target、Adobe Campaign或任何其他激活渠道等解决方案。

您现在需要创建查看过产品的所有客户的受众 **Real-Time CDP**.

要构建此受众，您需要添加一个体验事件。 您可以通过单击 **活动** 图标 **字段** 菜单栏。

![区段](./images/findee.png)

接下来，您将看到顶层， **XDM ExperienceEvents** 节点。 单击 **XDM ExperienceEvent**.

![区段](./images/see.png)

转到 **产品列表项**.

![区段](./images/plitems.png)

选择 **名称** 并拖放 **名称** 对象从左侧菜单转到受众生成器画布中的 **活动** 部分。 您随后将看到以下内容：

![区段](./images/eewebpdtlname.png)

比较参数应为 **等于** 在输入字段中，输入 **Real-time CDP**.

![区段](./images/pv.png)

每次将元素添加到受众生成器时，您都可以单击 **刷新估计** 按钮以获取受众中群体的新估计值。

![区段](./images/refreshest.png)

作为 **评估方法**，选择 **Edge**.

![区段](./images/evedge.png)

最后，让我们为您的受众提供一个名称并保存它。

作为命名约定，请使用：

- `yourLastName - Interest in Real-Time CDP`

然后，单击 **保存并关闭** 按钮以保存受众。

![区段](./images/segmentname.png)

您将立即返回受众概述页面，在那里您将看到符合受众条件的客户个人资料的示例预览。

![区段](./images/savedsegment.png)

您现在可以继续下一个练习，并将您的受众与Adobe Target结合使用。

下一步： [1.4操作：将受众发送到Adobe Target](./ex4.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)


[def]: ./images/segmentationpopup.png
