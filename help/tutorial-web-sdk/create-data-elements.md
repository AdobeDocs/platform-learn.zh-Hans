---
title: 创建数据元素
description: 了解如何在标记中创建XDM对象并将数据元素映射到该对象。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 9b112881a3b062cbd56502b3644c701c82380735
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 4%

---

# 创建数据元素

了解如何使用Experience PlatformWeb SDK创建捕获数据所需的基本数据元素。 在上捕获内容和身份数据 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html). 了解如何使用您之前创建的XDM架构，通过名为XDM对象的新数据元素类型使用Platform Web SDK收集数据。

>[!NOTE]
>
> 出于演示目的，本课程中的练习以中使用的示例为基础， [配置架构](configure-schemas.md) 步骤；创建示例XDM对象，用于捕获在上查看的内容和用户身份 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>本课程的数据来自 `[!UICONTROL digitalData]` Luma网站上的数据层。 要查看数据层，请打开您的开发人员控制台并键入 `[!UICONTROL digitalData]` 以查看完整的数据层。![digitalData数据层](assets/data-element-data-layer.png)


无论Platform Web SDK如何，您都必须继续在tag属性内创建数据元素，这些元素映射到来自网站的数据收集变量，例如数据层、HTML属性或其他变量。 创建这些数据元素后，必须将其映射到您在迁移期间创建的XDM架构。 [配置架构](configure-schemas.md) 上课。 为此，Platform Web SDK扩展提供了一个名为XDM对象的新数据元素类型。 因此，创建数据元素包含两个操作：

1. 将网站变量映射到数据元素，以及
1. 将这些数据元素映射到XDM对象

对于步骤1，使用任何核心标记扩展的数据元素类型，继续像当前一样将数据层映射到数据元素。 对于步骤2，Platform Web SDK扩展将创建一组以前不可用的新数据元素类型：

* 事件合并Id
* 标识映射
* XDM对象

本课程重点介绍XDM对象和身份映射数据元素类型。 您将创建XDM对象以捕获Luma访客的活动和身份验证状态。

## 学习目标

在本课程结束时，您能够：

* 创建数据元素以捕获内容和用户登录ID数据
* 创建身份映射数据元素
* 将数据元素映射到XDM对象数据元素


## 先决条件

您已了解数据层是什么，对 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 数据层，并了解如何引用标记中的数据元素。 您必须完成本教程中以下先前步骤

* [配置权限](configure-permissions.md)
* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)

>[!IMPORTANT]
>
>此 [Experience CloudID服务扩展](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 在实施Adobe Experience Platform Web SDK时不需要使用，因为ID服务功能已内置到Platform Web SDK中。

## 创建数据元素以捕获数据层

在开始创建XDM对象之前，请创建以下一组映射到对象的数据元素 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 数据层：

1. 转到 **[!UICONTROL 数据元素]** 并选择 **[!UICONTROL 添加数据元素]** (或 **[!UICONTROL 创建新数据元素]** 如果标记属性中没有现有的数据元素)

   ![创建数据元素](assets/data-element-create.jpg)

1. 将数据元素命名为 `page.pageInfo.pageName`
1. 使用 **[!UICONTROL JavaScript变量]** **[!UICONTROL 数据元素类型]** 指向Luma数据层中的值： `digitalData.page.pageInfo.pageName`

1. 选中 **[!UICONTROL Force lowercase value]** 和 **[!UICONTROL Clean text]** 复选框，以使大小写标准化，并删除无关空格

1. 离开 `None` 作为 **[!UICONTROL 存储持续时间]** 设置，因为该值在每个页面上都不相同

1. 选择 **[!UICONTROL 保存]**

   ![页面名称数据元素](assets/data-element-pageName.jpg)

按照相同的步骤创建以下四个附加数据元素：

* **`page.pageInfo.server`**  已映射到
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  已映射到
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  已映射到
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** 已映射到
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** 已映射到 `digitalData.cart.orderId` (您将在以下时段使用此项： [设置Analytics](setup-analytics.md) 课程)


>[!CAUTION]
>
>此 [!UICONTROL JavaScript变量] data element type将数组引用视为点而不是括号，因此引用username数据元素为 `digitalData.user[0].profile[0].attributes.username` **不起作用**.

## 创建身份映射数据元素

接下来，您可以创建Identity Map数据元素：

1. 转到 **[!UICONTROL 数据元素]** 并选择 **[!UICONTROL 添加数据元素]**

1. **[!UICONTROL 名称]** 数据元素 `identityMap.loginID`

1. 作为 **[!UICONTROL 扩展]**，选择 `Adobe Experience Platform Web SDK`

1. 作为 **[!UICONTROL 数据元素类型]**，选择 `Identity map`

1. 这会提示右侧的屏幕区域 **[!UICONTROL 数据收集界面]** 用于配置身份：

   ![数据收集界面](assets/identity-identityMap-setup.png)

1. 作为  **[!UICONTROL 命名空间]**，选择 `Luma CRM Id` 您之前在中创建的命名空间 [配置身份](configure-identities.md) 上课。

   >[!NOTE]
   >
   >    如果您没有看到您的 `Luma CRM Id` 命名空间，请确认您还在默认的生产沙盒中创建了该命名空间。 只有默认生产沙盒中创建的命名空间当前才会显示在命名空间下拉列表中。

1. 在 **[!UICONTROL 命名空间]** ，则必须设置ID。 选择 `user.profile.attributes.username` 在本课程前面创建的数据元素，会在用户登录Luma网站时捕获ID。

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. 作为 **[!UICONTROL 已验证状态]**，选择 **[!UICONTROL 已验证]**

1. 选择 **[!UICONTROL 保存]**

   ![数据收集界面](assets/identity-id-namespace.png)

<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## 将数据元素映射到XDM对象

您创建的所有数据元素必须映射到XDM对象。 此对象应符合您在 [配置架构](configure-schemas.md) 上课。

有不同的方法可以将数据元素映射到XDM对象字段。 您可以将单个数据元素映射到单个XDM字段，也可以将数据元素映射到整个XDM对象，前提是数据元素与XDM对象中存在的确切键值对架构匹配。 在本课程中，您捕获的内容数据将通过映射到各个字段来捕获。 您将学习如何 [将数据元素映射到整个XDM对象](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) 在 [设置Analytics](setup-analytics.md) 上课。

创建XDM对象以捕获内容数据：

1. 在左侧导航中，选择 **[!UICONTROL 数据元素]**
1. 选择 **[!UICONTROL 添加数据元素]**
1. ****&#x200B;将数据元素命名为 **`xdm.content`**
1. 作为 **[!UICONTROL 扩展]** 选择 `Adobe Experience Platform Web SDK`
1. 作为 **[!UICONTROL 数据元素类型]** 选择 `XDM object`
1. 选择平台 **[!UICONTROL 沙盒]** ，您在此期间在中创建了XDM架构。 [配置XDM架构](configure-schemas.md) 课程，在本例中 `DEVELOPMENT Mobile and Web SDK Courses`
1. 作为 **[!UICONTROL 架构]**，选择您的 `Luma Web Event Data` 架构：

   ![XDM对象](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >沙盒对应于您在其中创建架构的Experience Platform沙盒。 您的Experience Platform实例中可能有多个沙盒，因此请确保选择正确的沙盒。 始终先从事开发，然后从事生产。

1. 向下滚动，直到达到 **`web`** 对象
1. 选择以将其打开

   ![Web对象](assets/data-element-pageviews-xdm-object.png)


1. 将以下Web XDM变量映射到数据元素

   * **`web.webPageDetials.name`** 到 `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** 到 `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** 到 `%page.pageInfo.hierarchie1%`

   ![XDM对象](assets/data-element-xdm.content.png)

1. 接下来，查找 `identityMap` 对象并将其选定

1. 将映射到 `identityMap.loginID` 数据元素

1. 选择 **[!UICONTROL 保存]**

   ![数据收集界面](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




在这些步骤结束时，您应该创建以下数据元素：

| 核心扩展数据元素 | Platform Web SDK数据元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

设置这些数据元素后，您便可以在标记中创建规则，开始通过XDM对象向Platform Edge Network发送数据。

[下一步： ](create-tag-rule.md)

>[!NOTE]
>
>感谢您投入时间来了解Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此分享这些内容 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
