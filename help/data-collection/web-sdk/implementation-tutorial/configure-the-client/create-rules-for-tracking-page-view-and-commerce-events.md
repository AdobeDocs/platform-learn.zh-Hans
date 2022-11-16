---
title: 创建用于跟踪页面查看和商务事件的规则
description: 创建用于跟踪页面查看和商务事件的规则
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 创建用于跟踪页面查看和商务事件的规则

要跟踪用户是否已查看产品页面，请在Adobe Experience Platform标记中创建规则。 通过单击 [!UICONTROL 规则] 在左侧菜单中，单击 [!UICONTROL 添加规则].

对于规则名称，输入 _查看的页面_.

## 添加事件

单击 [!UICONTROL 添加] 按钮 [!UICONTROL 事件]. 您现在可以在事件视图中显示。 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL Adobe客户端数据层]. 对于 [!UICONTROL 事件类型] 字段，选择 [!UICONTROL 数据推送].

因为您只希望在 `pageViewed` 事件被推送到数据层，请选择 [!UICONTROL 特定事件] 在 [!UICONTROL 听] 和类型 _pageViewed_ 到 [!UICONTROL 要注册的事件/键] 文本。

![页面查看事件](../../../assets/implementation-strategy/page-viewed-event.png)

单击 [!UICONTROL Keep Changes].

## 添加操作

现在，您又回到了规则视图，单击 [!UICONTROL 添加] 按钮 [!UICONTROL 操作]. 此时您应该处于操作视图中。 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL Adobe Experience Platform Web SDK]. 对于 [!UICONTROL 操作类型] 字段，选择 [!UICONTROL 发送事件]. 此操作允许您将体验事件发送到Adobe Experience Platform Edge Network。

在屏幕的右侧，找到 [!UICONTROL 类型] 字段和选择 `web.webpagedetails.pageViews`. 这是Adobe Experience Platform开箱即用提供的一种规范型体验事件类型。 它表示页面查看。

对于 [!UICONTROL XDM数据] 字段，输入 `%event.fullState%`. 这表示在触发规则时捕获的数据层的计算状态（也称为完全状态）应作为体验事件的一部分发送。

![“查看的页面”操作](../../../assets/implementation-strategy/page-viewed-action.png)

如果您从网站推送到数据层的数据与XDM架构不符，或者如果您只想发送数据层的一部分计算状态，请使用 [!UICONTROL XDM对象] 数据元素类型(由Adobe Experience Platform Web SDK扩展提供)，以构建与您的模式匹配的相应对象。

单击 [!UICONTROL Keep Changes] 按钮.

## 保存规则

您的规则现在应该已完成。

![查看的页面规则](../../../assets/implementation-strategy/page-viewed-rule.png)

通过单击 [!UICONTROL 保存].

## 重复该过程

重复上述过程以创建查看产品、打开购物车以及将产品添加到购物车的规则。 规则之间的唯一区别将是规则名称，即在 [!UICONTROL 要注册的事件/键] 字段 [!UICONTROL 数据推送] 事件和 [!UICONTROL 类型] 字段 [!UICONTROL 发送事件] 操作。 以下是每个规则的值：

产品查看规则：

* **规则名称**: _查看的产品_
* **要注册的事件/键** within [!UICONTROL 数据推送] 事件： `productViewed`
* **类型** within [!UICONTROL 发送事件] 操作： `commerce.productViews`

购物车打开规则：

* **规则名称**: _购物车打开_
* **要注册的事件/键** within [!UICONTROL 数据推送] 事件： `cartOpened`
* **类型** within [!UICONTROL 发送事件] 操作： `commerce.productListOpens`

添加到购物车规则的产品：

* **规则名称**: _添加到购物车的产品_
* **要注册的事件/键** within [!UICONTROL 数据推送] 事件： `productAddedToCart`
* **类型** within [!UICONTROL 发送事件] 操作： `commerce.productListAdds`

接下来，我们将处理 [!UICONTROL 下载应用程序] 链接。
