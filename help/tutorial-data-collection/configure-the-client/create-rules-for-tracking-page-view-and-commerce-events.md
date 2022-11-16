---
title: 创建用于跟踪页面查看和商务事件的规则
description: 创建用于跟踪页面查看和商务事件的规则
exl-id: 00bf3374-9319-47ce-a75a-2b94f793c938
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# 创建用于跟踪页面查看和商务事件的规则

要跟踪用户是否已查看产品页面，请在Adobe Experience Platform中创建规则 [!DNL Tags].

1. 单击 **[!UICONTROL 规则]** 在左侧导航中，单击 **[!UICONTROL 创建新规则]**.

1. 对于规则名称，输入 **_查看的页面_**.

## 添加事件

1. 单击 **[!UICONTROL 添加]** 按钮 [!UICONTROL 事件]. 您现在可以在事件视图中显示。 对于 [!UICONTROL 扩展] 字段，选择 **[!UICONTROL Adobe客户端数据层]**. 对于 [!UICONTROL 事件类型] 字段，选择 **[!UICONTROL 数据推送]**.
1. 因为您只希望在 `pageViewed` 事件被推送到数据层，请选择 **[!UICONTROL 特定事件]** 在 [!UICONTROL 听] 和类型 **_pageViewed_** 到 [!UICONTROL 要注册的事件/键] 文本。
1. 单击 **[!UICONTROL Keep Changes]**.
   ![页面查看事件](../assets/page-viewed-event.png)

## 添加操作

现在，您又回到了规则视图：

1. 单击&#x200B;**[!UICONTROL 操作]**&#x200B;下的[!UICONTROL 添加]按钮。此时您应该处于操作视图中。 对于 [!UICONTROL 扩展] 字段，选择 **[!UICONTROL Adobe Experience Platform Web SDK]**. 对于 [!UICONTROL 操作类型] 字段，选择 **[!UICONTROL 发送事件]**. 此操作允许您将体验事件发送到Adobe Experience Platform Edge Network。
1. 在屏幕的中间，找到 [!UICONTROL 类型] 字段和选择 **`web.webpagedetails.pageViews`**. 这是Adobe Experience Platform开箱即用提供的一种规范型体验事件类型。 它表示页面查看。
1. 对于 [!UICONTROL XDM数据] 字段，输入 **`%event.fullState%`**. 这表示在触发规则时捕获的数据层的计算状态（也称为完全状态）。 该事件应作为体验事件的一部分发送。
1. 单击 **[!UICONTROL Keep Changes]** 按钮.
   ![“查看的页面”操作](../assets/page-viewed-action.png)

如果您从网站推送到数据层的数据与XDM架构不符，或者如果您只想发送数据层的一部分计算状态，请使用 [!UICONTROL XDM对象] 数据元素类型(由Adobe Experience Platform Web SDK扩展提供)，以构建与您的模式匹配的相应对象。

## 保存规则

1. 通过单击 **[!UICONTROL 保存]**.
   ![查看的页面规则](../assets/page-viewed-rule.png)

## 重复该过程

重复上述过程以创建查看产品、打开购物车以及将产品添加到购物车的规则。 这些规则之间的唯一区别是规则名称，即在 [!UICONTROL 要注册的事件/键] 字段 [!UICONTROL 数据推送] 事件和 [!UICONTROL 类型] 字段 [!UICONTROL 发送事件] 操作。 以下是每个规则的值：

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

[下一个： ](create-a-data-element-and-rule-for-tracking-app-downloads.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
