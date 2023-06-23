---
title: 创建规则以跟踪页面查看和商务事件
description: 创建规则以跟踪页面查看和商务事件
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 创建规则以跟踪页面查看和商务事件

要跟踪用户是否查看过产品页面，请在Adobe Experience Platform标记中创建规则。 通过单击 [!UICONTROL 规则] 在左侧菜单中，然后单击 [!UICONTROL 添加规则].

对于规则名称，输入 _已查看页面_.

## 添加事件

单击 [!UICONTROL 添加] 按钮位于 [!UICONTROL 事件]. 您现在显示在事件视图中。 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL Adobe客户端数据层]. 对于 [!UICONTROL 事件类型] 字段，选择 [!UICONTROL 推送的数据].

因为您只希望此规则在 `pageViewed` 事件被推送到数据层，请选择 [!UICONTROL 特定事件] 下 [!UICONTROL 收听] 和类型 _pageViewed_ 到 [!UICONTROL 要注册的事件/密钥] 文本字段。

![已查看页面事件](../../../assets/implementation-strategy/page-viewed-event.png)

单击 [!UICONTROL Keep Changes].

## 添加操作

现在，您已返回规则视图，请单击 [!UICONTROL 添加] 按钮位于 [!UICONTROL 操作]. 现在，您应位于操作视图中。 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL Adobe Experience Platform Web SDK]. 对于 [!UICONTROL 操作类型] 字段，选择 [!UICONTROL 发送事件]. 此操作允许您向Adobe Experience Platform Edge Network发送体验事件。

在屏幕的右侧，找到 [!UICONTROL 类型] 字段并选择 `web.webpagedetails.pageViews`. 这是Adobe Experience Platform提供的现成规范体验事件类型之一。 它表示页面查看。

对于 [!UICONTROL XDM数据] 字段，输入 `%event.fullState%`. 这表示在触发规则时捕获的数据层的计算状态（也称为完全状态），应当作为体验事件的一部分发送。

![已查看页面操作](../../../assets/implementation-strategy/page-viewed-action.png)

如果您从网站推入数据层的数据不符合XDM架构，或者您只想发送数据层的部分计算状态，请使用 [!UICONTROL XDM对象] 数据元素类型(由Adobe Experience Platform Web SDK扩展提供)，以构建与您的架构匹配的适当对象。

单击 [!UICONTROL Keep Changes] 按钮.

## 保存规则

您的规则现在应已完成。

![页面查看规则](../../../assets/implementation-strategy/page-viewed-rule.png)

通过单击保存规则 [!UICONTROL 保存].

## 重复该过程

重复上述过程以创建规则，用于何时查看产品、打开购物车以及何时将产品添加到购物车。 规则之间唯一的区别是规则名称，即在 [!UICONTROL 要注册的事件/密钥] 中的字段 [!UICONTROL 推送的数据] 事件，以及 [!UICONTROL 类型] 中的字段 [!UICONTROL 发送事件] 操作。 以下是每个规则的值：

产品查看规则：

* **规则名称**： _已查看的产品_
* **要注册的事件/密钥** 范围 [!UICONTROL 推送的数据] 事件： `productViewed`
* **类型** 范围 [!UICONTROL 发送事件] 操作： `commerce.productViews`

购物车已打开规则：

* **规则名称**： _购物车已打开_
* **要注册的事件/密钥** 范围 [!UICONTROL 推送的数据] 事件： `cartOpened`
* **类型** 范围 [!UICONTROL 发送事件] 操作： `commerce.productListOpens`

产品已添加到购物车规则：

* **规则名称**： _产品已添加到购物车_
* **要注册的事件/密钥** 范围 [!UICONTROL 推送的数据] 事件： `productAddedToCart`
* **类型** 范围 [!UICONTROL 发送事件] 操作： `commerce.productListAdds`

接下来，我们将处理 [!UICONTROL 下载应用程序] 链接。
