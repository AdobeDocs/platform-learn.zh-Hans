---
title: 创建标记规则
description: 了解如何使用标记规则将事件与XDM对象一起发送到Platform Edge Network。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Tags
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 4%

---

# 创建标记规则

了解如何使用标记规则将事件与XDM对象一起发送到Platform Edge Network。 标记规则是事件、条件和操作的组合，用于告知标记属性执行一些操作。

>[!NOTE]
>
> 出于演示目的，本课程中的练习以本课程中用到的示例为基础， [创建数据元素](create-data-elements.md) 步骤；发送XDM事件操作以从上的用户捕获内容和身份 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html).


## 学习目标

在本课程结束后，您将能够：

* 使用命名惯例来管理标记中的规则
* 创建标记规则以发送XDM事件
* 将标记规则发布到开发库


## 先决条件

您熟悉数据收集标记和 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html)，并且您必须在教程中完成以下以前的课程：

* [配置权限](configure-permissions.md)
* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)

## 命名约定

为了更好地管理标记中的规则，建议遵循标准命名约定。 本教程使用三部分命名约定：

* [位置] - [事件] - [工具]

其中；

1. 位置是触发规则的网站上的一个或多个页面
1. 事件是触发信标的触发器
1. 工具是在该规则的操作步骤中使用的一个或多个特定应用程序


## 创建标记规则

在标记中，规则用于在各种条件下执行操作（触发调用）。 您将使用此第一条规则通过Web SDK的 [!UICONTROL 发送事件] 操作。 在本教程的后面部分，您将根据访客所在的页面类型发送不同版本的XDM对象。 因此，您将使用规则条件来排除这些其他类型的页面。

要创建标记规则，请执行以下操作：

1. 打开您在本教程中使用的标记属性
1. 转到 **[!UICONTROL 规则]** 在左侧导航中
1. 选择 **[!UICONTROL 创建新规则]** 按钮
   ![创建规则](assets/rules-create.png)
1. 将规则命名为 `all pages - library load - AA & AT`

   >[!NOTE]
   >
   > Adobe Analytics和Target在未来课程中以特定方式使用此规则，这正是为什么 `AA & AT` 在名称的末尾使用。

1. 在 **[!UICONTROL 活动]** 部分，选择 **[!UICONTROL 添加]**
   ![命名规则并添加事件](assets/rule-name.png)
1. 使用 **[!UICONTROL 核心扩展]** 并选择 `Library Loaded (Page Top)` 作为 **[!UICONTROL 事件类型]**.

   此设置意味着每当在页面上加载标记库时，就会触发规则。
1. 选择 **[!UICONTROL 保留更改]** 以返回到主规则屏幕
   ![添加Library Loaded事件](assets/rule-event-pagetop.png)
1. 在 **[!UICONTROL 条件]** 部分，选择 **[!UICONTROL 添加]** 按钮
   ![添加条件](assets/rules-add-conditions.png)
1. 选择 **[!UICONTROL 逻辑类型]** `Exception`， **[!UICONTROL 扩展名]** `Core`、和 **[!UICONTROL 完成情况类型]** `Path Without Query String`
1. 输入URL路径 `/content/luma/us/en/user/cart.html` 在 **[!UICONTROL 路径等于]** 字段，以及 **[!UICONTROL name]** it `Core - cart page`
1. 选择 **[!UICONTROL 保留更改]**
   ![添加条件](assets/rule-condition-exception.png)
1. 为以下URL路径再添加三个例外

   * **`Core - checkout page`** for `/content/luma/us/en/user/checkout.html`
   * **`Core - thank you page`** for `/content/luma/us/en/user/checkout/order/thank-you.html`
   * **`Core - product page`** 对象 `/products/` Regex开关打开时

   ![添加条件](assets/rule-condition-exception-all.png)

1. 在 **[!UICONTROL 操作]** 部分，选择 **[!UICONTROL 添加]**
1. 选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 作为 **[!UICONTROL 扩展名]**
1. 选择 **[!UICONTROL 发送事件]** 作为 **[!UICONTROL 操作类型]**
1. 选择 **[!UICONTROL web.webpagedetails.pageViews]** 作为 **[!UICONTROL 类型]**.

   >[!WARNING]
   >
   > 此下拉菜单会填充 **`xdm.eventType`** 变量标识。 虽然您也可以在此字段中键入自由格式标签，但强烈建议您 **不要** 因为它对Platform会产生负面影响。

1. 作为 **[!UICONTROL XDM数据]**，选择 `xdm.content` 在上一课程中创建的数据元素
1. 选择 **[!UICONTROL 保留更改]** 以返回到主规则屏幕

   ![添加Send Event操作](assets/rule-set-action-xdm.png)
1. 选择 **[!UICONTROL 保存]** 保存规则

   ![保存规则](assets/rule-save.png)

## 在库中发布规则

接下来，将规则发布到您的开发环境，以便我们可以验证它是否正常工作。

要创建库，请执行以下操作：

1. 转到 **[!UICONTROL 发布流]** 在左侧导航中
1. 选择 **[!UICONTROL 添加库]**

   ![选择“添加库”](assets/rule-publish-library.png)
1. 对于 **[!UICONTROL 名称]**，输入 `Luma Web SDK Tutorial`
1. 对于 **[!UICONTROL 环境]**，选择 `Development`
1. 选择  **[!UICONTROL 添加所有已更改资源]**

   >[!NOTE]
   >
   >    除了Adobe Experience Platform Web SDK扩展和 `all pages - library load - AA & AT` 规则，您将看到在前面的课程中创建的标记组件。 核心扩展包含所有Web标记属性所需的基本JavaScript。

1. 选择 **[!UICONTROL 保存并构建用于开发]**

   ![创建并生成库](assets/rule-publish-add-all-changes.png)

库可能需要几分钟才能构建，完成后，库名称左侧会显示一个绿色圆点：

![生成完成](assets/rule-publish-success.png)

如您所见， [!UICONTROL 发布流] 屏幕，发布流程还有许多其他内容超出了本教程的范围。 本教程仅在开发环境中使用单个库。

现在，您可以使用Adobe Experience Platform Debugger来验证请求中的数据。

[下一个 ](validate-with-debugger.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
