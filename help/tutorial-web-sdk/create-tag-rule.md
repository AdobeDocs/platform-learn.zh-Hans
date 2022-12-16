---
title: 创建标记规则
description: 了解如何使用标记规则，通过XDM对象将事件发送到Platform Edge Network。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Tags
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 7b978e1d98aa539c98b7f11ae33432729ac33bea
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 4%

---

# 创建标记规则

了解如何使用标记规则，通过XDM对象将事件发送到Platform Edge Network。 标记规则是事件、条件和操作的组合，用于告知标记属性执行一些操作。

>[!NOTE]
>
> 出于演示目的，本课程中的练习将以 [创建数据元素](create-data-elements.md) 步骤；发送XDM事件操作，以从 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html).


## 学习目标

在本课程结束后，您将能够：

* 使用命名约定管理标记内的规则
* 创建标记规则以发送XDM事件
* 将标记规则发布到开发库


## 先决条件

您熟悉数据收集标记和 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html)，并且您必须完成教程中以前的以下课程：

* [配置权限](configure-permissions.md)
* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [标记属性中安装的Web SDK扩展](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)

## 命名约定

为了更好地管理标记中的规则，建议遵循标准命名约定。 本教程使用三步命名约定：

* [位置] - [事件] - [工具]

地；

1. 位置是规则触发的站点上的一个或多个页面
1. 事件是触发信标的触发器
1. 工具是在该规则的操作步骤中使用的特定应用程序或应用程序


## 创建标记规则

在标记中，规则用于在各种条件下执行操作（触发调用）。 您将使用第一个规则，使用Web SDK的 [!UICONTROL 发送事件] 操作。 在本教程的后面，您将根据访客所在的页面类型发送不同版本的XDM对象。 因此，您将使用规则条件排除其他类型的页面。

要创建标记规则，请执行以下操作：

1. 打开您在本教程中使用的标记属性
1. 转到 **[!UICONTROL 规则]** 在左侧导航中
1. 选择 **[!UICONTROL 创建新规则]** 按钮
   ![创建规则](assets/rules-create.png)
1. 将规则命名为 `all pages - library load - AA & AT`

   >[!NOTE]
   >
   > Adobe Analytics和Target在将来的课程中将以特定方式使用此规则，这就是为什么 `AA & AT` 在名称的末尾使用。

1. 在 **[!UICONTROL 事件]** 选择 **[!UICONTROL 添加]**

   ![命名规则并添加事件](assets/rule-name.png)
1. 使用 **[!UICONTROL 核心扩展]** 选择 `Library Loaded (Page Top)` 作为 **[!UICONTROL 事件类型]**.

   此设置意味着，每当页面上加载标记库时，都会触发规则。
1. 选择 **[!UICONTROL 保留更改]** 返回主规则屏幕
   ![添加Library Loaded事件](assets/rule-event-pagetop.png)
1. 在 **[!UICONTROL 条件]** 选择 **[!UICONTROL 添加]** 按钮
   ![添加条件](assets/rules-add-conditions.png)
1. 选择 **[!UICONTROL 逻辑类型]** `Exception`, **[!UICONTROL 扩展]** `Core`和 **[!UICONTROL 条件类型]** `Path Without Query String`
1. 输入URL路径 `/content/luma/us/en/user/cart.html` 在 **[!UICONTROL 路径等于]** 字段，以及 **[!UICONTROL name]** it `Core - cart page`
1. 选择 **[!UICONTROL 保留更改]**

   ![添加条件](assets/rule-condition-exception.png)
1. 为以下URL路径添加另外三个例外

   * **`Core - checkout page`** for `/content/luma/us/en/user/checkout.html`
   * **`Core - thank you page`** for `/content/luma/us/en/user/checkout/order/thank-you.html`
   * **`Core - product page`** 表示 `/products/` Regex开关打开时

   ![添加条件](assets/rule-condition-exception-all.png)

1. 在 **[!UICONTROL 操作]** 选择 **[!UICONTROL 添加]**
1. 选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 作为 **[!UICONTROL 扩展]**
1. 选择 **[!UICONTROL 发送事件]** 作为 **[!UICONTROL 操作类型]**
1. 选择 **[!UICONTROL web.webpagedetails.pageViews]** 作为 **[!UICONTROL 类型]**.

   >[!WARNING]
   >
   > 此下拉菜单填充 **`xdm.eventType`** 变量。 虽然您还可以在此字段中键入自由格式标签，但强烈建议您 **不** 因为Platform会产生反感效果。

1. 作为 **[!UICONTROL XDM数据]**，选择 `xdm.content` 在上一课程中创建的数据元素
1. 选择 **[!UICONTROL 保留更改]** 返回主规则屏幕

   ![添加Send Event操作](assets/rule-set-action-xdm.png)
1. 选择 **[!UICONTROL 保存]** 保存规则

   ![保存规则](assets/rule-save.png)

## 在库中发布规则

接下来，将规则发布到您的开发环境，以便我们能够验证该规则是否有效。

要创建库，请执行以下操作：

1. 转到 **[!UICONTROL 发布流程]** 在左侧导航中
1. 选择 **[!UICONTROL 添加库]**

   ![选择添加库](assets/rule-publish-library.png)
1. 对于 **[!UICONTROL 名称]**，输入 `Luma Web SDK Tutorial`
1. 对于 **[!UICONTROL 环境]**，选择 `Development`
1. 选择  **[!UICONTROL Add All Changed Resources]**

   >[!NOTE]
   >
   >    除了Adobe Experience Platform Web SDK扩展和 `all pages - library load - AA & AT` 规则中，您将看到在以前的课程中创建的标记组件。 核心扩展包含所有Web标记属性所需的基本JavaScript。

1. 选择 **[!UICONTROL 保存并构建以用于开发]**

   ![创建和构建库](assets/rule-publish-add-all-changes.png)

库可能需要几分钟时间才能构建完成，它会在库名称左侧显示一个绿色圆点：

![构建完成](assets/rule-publish-success.png)

如您在 [!UICONTROL 发布流程] 屏幕上，发布流程还有许多内容不在本教程的涵盖范围内。 本教程在开发环境中只使用一个库。

现在，您可以使用Adobe Experience Platform Debugger验证请求中的数据。

[下一个 ](validate-with-debugger.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
