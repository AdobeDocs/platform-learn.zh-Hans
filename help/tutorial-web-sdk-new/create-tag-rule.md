---
title: 创建标记规则
description: 了解如何使用标记规则将事件与XDM对象一起发送到Platform Edge Network。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# 创建标记规则

了解如何使用标记规则将事件与XDM对象一起发送到Platform Edge Network。 标记规则是事件、条件和操作的组合，用于告知标记属性执行一些操作。

>[!NOTE]
>
> 出于演示目的，本课程中的练习以本课程中用到的示例为基础， [创建身份](create-identities.md) 步骤；发送XDM事件操作以从上的用户捕获内容和身份 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html).


## 学习目标

在本课程结束时，您能够：

* 使用命名惯例来管理标记中的规则
* 在标记规则中使用更新变量和发送事件操作类型发送XDM事件
* 将标记规则发布到开发库


## 先决条件

您熟悉数据收集标记和 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html)，并且您必须在教程中完成以下以前的课程：

* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)
* [创建身份](create-identities.md)

## 命名约定

为了更好地管理标记中的规则，建议遵循标准命名约定。 本教程使用三部分命名约定：

* [**位置**] - [**事件**] - [**工具**] (**序列**)

其中；

1. **位置** 是规则触发的网站上的一个或多个页面
1. **事件** 是规则的触发器
1. **工具** 是在该规则的操作步骤中使用的一个或多个特定应用程序
1. **序列** 是规则相对于其他规则应触发的顺序
<!-- minor update -->

## 创建标记规则

在标记中，规则用于在各种条件下执行操作（触发调用）。 Platform Web SDK标记扩展包含两个将在本课程中使用的操作：

* **[!UICONTROL 更新变量]** 将数据元素映射到XDM字段
* **[!UICONTROL 发送事件]** 将XDM对象发送到Experience Platform边缘网络

### 更新变量

创建此第一条规则作为“全局配置”，以使用Platform Web SDK的 **[!UICONTROL 更新变量]** 操作。 然后，创建第二个规则，按序列排列，以便在第一个规则之后触发，以使用将XDM对象发送到Platform Edge Network **[!UICONTROL 发送事件]** 操作。 在本教程的后面部分，您将根据访客所在的页面类型（例如产品页面上的产品SKU）发送不同的XDM字段。 您可以通过排序包含的规则来实现这一点 **[!UICONTROL 更新变量]** 操作，位于使用 **[!UICONTROL 发送事件]** 操作。

要创建标记规则，请执行以下操作：

1. 打开您在本教程中使用的标记属性

1. 转到 **[!UICONTROL 规则]** 在左侧导航中

1. 选择 **[!UICONTROL 创建新规则]** 按钮

   ![创建规则](assets/rules-create.png)

1. 将规则命名为 `all pages global content variables - page bottom - AA (order 1)`

1. 在 **[!UICONTROL 活动]** 部分，选择 **[!UICONTROL 添加]**

   ![命名规则并添加事件](assets/rule-name-new.png)

1. 使用 **[!UICONTROL 核心扩展]** 并选择 `Page Bottom` 作为 **[!UICONTROL 事件类型]**

1. 在 **[!UICONTROL 名称]** 字段，将其命名为 `Core - Page Bottom - order 1`. 这有助于您以有意义的名称描述触发器。

1. 选择 **[!UICONTROL 高级]** 下拉菜单并输入 `1` 在 **[!UICONTROL 订购]**

   >[!NOTE]
   >
   > 输入的数字越高，所触发的操作的整体顺序越靠后。

1. 选择 **[!UICONTROL 保留更改]** 以返回到主规则屏幕
   ![选择页面底部触发器](assets/create-tag-rule-trigger-bottom.png)

1. 在 **[!UICONTROL 操作]** 部分，选择 **[!UICONTROL 添加]**

1. 作为 **[!UICONTROL 扩展名]**，选择 **[!UICONTROL Adobe Experience Platform Web SDK]**

1. 作为 **[!UICONTROL 操作类型]**，选择 **[!UICONTROL 更新变量]**

1. 作为 **[!UICONTROL 数据元素]**，选择 `xdm.variable.content` 您已在 [创建数据元素](create-data-elements.md) 课程

   ![更新变量架构](assets/create-rule-update-variable.png)

现在映射您的 [!UICONTROL 数据元素] 到 [!UICONTROL 架构] 由XDM对象使用。

>[!NOTE]
> 
> 您可以映射到单个属性或整个对象。 在本例中，您将映射到各个属性。


1. 向下滚动，直到达到 **`web`** 对象

1. 选择以将其打开

1. 将以下数据元素映射到相应的 `web` XDM变量

   * **`web.webPageDetials.name`** 到 `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** 到 `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** 到 `%page.pageInfo.hierarchie1%`

   ![更新变量内容](assets/create-rule-xdm-variable-content.png)

1. 接下来，查找 `identityMap` 对象并将其选定

1. 将映射到 `identityMap.loginID` 数据元素

   ![更新变量标识映射](assets/create-rule-variable-identityMap.png)

1. 接下来，找到eventType字段并将其选定

1. 输入值 `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > 此下拉菜单会填充 **`xdm.eventType`** 变量标识。 虽然您也可以在此字段中键入自由格式标签，但强烈建议您 **不要** 因为它对Platform有负面影响。

   >[!TIP]
   >
   > 要了解在 `eventType` 字段，您必须转到架构页面并选择 `eventType` 字段以查看右边栏上的建议值。

   ![更新变量标识映射](assets/create-tag-rule-eventType.png)


1. 选择 **[!UICONTROL 保留更改]** 然后 **[!UICONTROL 保存]** 下一个屏幕中用于完成规则创建的规则

### 发送事件

现在，您已设置变量，接下来可以创建第二个规则，使用将XDM对象发送到Platform Edge Network **[!UICONTROL 发送事件]** 操作类型。

1. 在右侧，选择 **[!UICONTROL 添加规则]** 创建其他规则

1. 将规则命名为 `all pages send event - page bottom - AA (order 50)`

1. 在 **[!UICONTROL 活动]** 部分，选择 **[!UICONTROL 添加]**

1. 使用 **[!UICONTROL 核心扩展]** 并选择 `Page Bottom` 作为 **[!UICONTROL 事件类型]**

1. 在 **[!UICONTROL 名称]** 字段，将其命名为 `Core - Page Bottom - order 50`. 这有助于您以有意义的名称描述触发器。

1. 选择 **[!UICONTROL 高级]** 下拉菜单并输入 `50` 在 **[!UICONTROL 订购]**. 这将确保第二个规则在您设置为触发的第一个规则之后触发 `1`.

1. 选择 **[!UICONTROL 保留更改]** 以返回到主规则屏幕
   ![选择页面底部触发器](assets/create-tag-rule-trigger-bottom-send.png)

1. 在 **[!UICONTROL 操作]** 部分，选择 **[!UICONTROL 添加]**

1. 作为 **[!UICONTROL 扩展名]**，选择  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. 作为  **[!UICONTROL 操作类型]**，选择  **[!UICONTROL 发送事件]**

1. 作为 **[!UICONTROL XDM]**，选择 `xdm.variable.content` 在上一课程中创建的数据元素

1. 选择 **[!UICONTROL 保留更改]** 以返回到主规则屏幕

   ![添加Send Event操作](assets/create-rule-send-event-action.png)
1. 选择 **[!UICONTROL 保存]** 保存规则

   ![保存规则](assets/create-rule-save-rule.png)

## 在库中发布规则

接下来，将规则发布到开发环境，以便您可以验证它是否有效。

要创建库，请执行以下操作：

1. 转到 **[!UICONTROL 发布流]** 在左侧导航中

1. 选择 **[!UICONTROL 添加库]**

   ![选择“添加库”](assets/rule-publish-library.png)
1. 对于 **[!UICONTROL 名称]**，输入 `Luma Web SDK Tutorial`
1. 对于 **[!UICONTROL 环境]**，选择 `Development`
1. 选择  **[!UICONTROL 添加所有已更改资源]**

   >[!NOTE]
   >
   >    除了Adobe Experience Platform Web SDK扩展和 `all pages global content variables - page bottom - AA (order 50)` 规则，您将看到在前面的课程中创建的标记组件。 核心扩展包含所有Web标记属性所需的基本JavaScript。

1. 选择 **[!UICONTROL 保存并构建用于开发]**

   ![创建并生成库](assets/create-tag-rule-library-changes.png)

库可能需要几分钟才能构建，完成后，库名称左侧会显示一个绿色圆点：

![生成完成](assets/create-rule-development-success.png)

如您所见， [!UICONTROL 发布流] 屏幕，发布流程还有许多其他内容超出了本教程的范围。 本教程仅在开发环境中使用单个库。

现在，您可以使用Adobe Experience Platform Debugger来验证请求中的数据。

[下一个 ](validate-with-debugger.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
