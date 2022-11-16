---
title: 创建数据元素
description: 了解如何在标记中创建XDM对象并将数据元素映射到该对象。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 4%

---

# 创建数据元素

了解如何使用Experience PlatformWeb SDK创建捕获数据所需的基本数据元素。 捕获 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html). 了解如何使用您之前创建的XDM模式，通过名为XDM对象的新数据元素类型，使用Platform Web SDK收集数据。

>[!NOTE]
>
> 出于演示目的，本课程中的练习将基于 [配置架构](configure-schemas.md) 步骤；创建XDM对象示例，该对象可捕获 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>本课程的数据来自 `[!UICONTROL digitalData]` 数据层。 要查看数据层，请打开开发人员控制台并键入 `[!UICONTROL digitalData]` 以查看可用的完整数据层。![digitalData数据层](assets/data-element-data-layer.png)


无论使用何种Platform Web SDK，您都必须继续在标记属性内创建数据元素，以将其映射到来自您网站的数据收集变量，如数据层、HTML属性或其他变量。 创建这些数据元素后，必须将其映射到在 [配置架构](configure-schemas.md) 课程。 为此，Platform Web SDK扩展提供了一个名为XDM对象的新数据元素类型。 因此，创建数据元素包含两个操作：

1. 将网站变量映射到数据元素，以及
1. 将这些数据元素映射到XDM对象

对于步骤1，您可以使用任何核心标记扩展的数据元素类型，继续按照当前的方式将数据层映射到数据元素。 对于步骤2,Platform Web SDK扩展会创建一组以前不可用的新数据元素类型：

* 事件合并ID
* 身份映射
* XDM对象

本课程重点介绍XDM对象和身份映射数据元素类型。 您将创建XDM对象以捕获Luma访客的活动和身份验证状态。

## 学习目标

在本课程结束时，您能够：

* 创建数据元素以捕获内容和用户登录ID数据
* 创建身份映射数据元素
* 将数据元素映射到XDM对象数据元素


## 先决条件

您对数据层是什么有了解，并熟悉 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}数据层，并了解如何在标记中引用数据元素。 您必须在教程中完成以前的步骤

* [配置权限](configure-permissions.md)
* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [标记属性中安装的Web SDK扩展](install-web-sdk.md)

>[!IMPORTANT]
>
>的 [Experience CloudID服务扩展](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 实施Adobe Experience Platform Web SDK时不需要，因为ID服务功能内置于Platform Web SDK中。

## 创建数据元素以捕获数据层

在开始创建XDM对象之前，请创建以下映射到的数据元素集 [Luma演示网站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}数据层：

1. 转到 **[!UICONTROL 数据元素]** 选择 **[!UICONTROL 添加数据元素]** (或 **[!UICONTROL 创建新数据元素]** 如果标记属性中没有现有数据元素)

   ![创建数据元素](assets/data-element-create.jpg)

1. 将数据元素命名为 `page.pageInfo.pageName`
1. 使用 **[!UICONTROL JavaScript变量]** **[!UICONTROL 数据元素类型]** 指向Luma数据层中的值： `digitalData.page.pageInfo.pageName`

1. 选中 **[!UICONTROL Force lowercase value]** 和 **[!UICONTROL Clean text]** 复选框，以使大小写标准化，并删除无关空格

1. 离开 `None` 作为 **[!UICONTROL 存储持续时间]** 设置，因为该值在每个页面上都不同

1. 选择 **[!UICONTROL 保存]**

   ![页面名称数据元素](assets/data-element-pageName.jpg)

按照相同的步骤创建这四个附加数据元素：

* **`page.pageInfo.server`**  映射到
   `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  映射到
   `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  映射到
   `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** 映射到
   `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** 映射到 `digitalData.cart.orderId` (在 [设置分析](setup-analytics.md) lession)


>[!CAUTION]
>
>的 [!UICONTROL JavaScript变量] 数据元素类型将数组引用视为点而不是括号，因此引用用户名数据元素将作为 `digitalData.user[0].profile[0].attributes.username` **不起作用**.

## 创建身份映射数据元素

接下来，您可以创建身份映射数据元素：

1. 转到 **[!UICONTROL 数据元素]** 选择 **[!UICONTROL 添加数据元素]**

1. **[!UICONTROL 名称]** 数据元素 `identityMap.loginID`

1. 作为 **[!UICONTROL 扩展]**，选择 `Adobe Experience Platform Web SDK`

1. 作为 **[!UICONTROL 数据元素类型]**，选择 `Identity map`

1. 这会提示屏幕右侧的 **[!UICONTROL 数据收集界面]** 用于配置标识：

   ![数据收集界面](assets/identity-identityMap-setup.png)

1. 作为  **[!UICONTROL 命名空间]**，选择 `Luma CRM Id` 之前在 [配置标识](configure-identities.md) 课程。

   >[!NOTE]
   >
   >    如果你没有看到 `Luma CRM Id` 命名空间中，请确认您还在默认的生产沙盒中创建了该命名空间。 当前，只有在默认生产沙盒中创建的命名空间才会显示在命名空间下拉列表中。

1. 在 **[!UICONTROL 命名空间]** ，则必须设置ID。 选择 `user.profile.attributes.username` 本课程前面创建的数据元素，该元素会在用户登录Luma网站时捕获ID。

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. 作为 **[!UICONTROL 已验证状态]**，选择 **[!UICONTROL 已验证]**

1. 选择 **[!UICONTROL 保存]**

   ![数据收集界面](assets/identity-id-namespace.png)

>[!WARNING]
>
>所有发送到Adobe Experience Platform的记录中都需要主标识。 默认情况下，Experience CloudID(ECID)将用作Platform Web SDK的主标识。 你绝不会想用 `Luma CRM ID` 作为Web SDK的主标识，因为该标识仅在用户进行身份验证后存在，因此不能在所有记录中使用。

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

您创建的所有数据元素都必须映射到XDM对象。 此对象应符合您在 [配置架构](configure-schemas.md) 课程。

数据元素有不同的方法可映射到XDM对象字段。 您可以将单个数据元素映射到单个XDM字段，或将数据元素映射到整个XDM对象，前提是您的数据元素与XDM对象中存在的精确键值对架构匹配。 在本课程中，您将通过映射到各个字段来捕获内容数据。 您将学习如何 [将数据元素映射到整个XDM对象](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) 在 [设置分析](setup-analytics.md) 课程。

创建XDM对象以捕获内容数据：

1. 在左侧导航中，选择 **[!UICONTROL 数据元素]**
1. 选择 **[!UICONTROL 添加数据元素]**
1. ****&#x200B;将数据元素命名为 **`xdm.content`**
1. 作为 **[!UICONTROL 扩展]** 选择 `Adobe Experience Platform Web SDK`
1. 作为 **[!UICONTROL 数据元素类型]** 选择 `XDM object`
1. 选择平台 **[!UICONTROL 沙盒]** 中创建了XDM架构。 [配置XDM架构](configure-schemas.md) 本例中的课程 `DEVELOPMENT Mobile and Web SDK Courses`
1. 作为 **[!UICONTROL 架构]**，选择 `Luma Web Event Data` 架构：

   ![XDM对象](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >沙盒对应于您在其中创建架构的Experience Platform沙盒。 您的Experience Platform实例中可以有多个可用沙箱，因此请确保选择正确的沙箱。 总是先在开发中工作，再在生产中工作。

1. 向下滚动直到您到达 **`web`** 对象
1. 选择以将其打开

   ![Web对象](assets/data-element-pageviews-xdm-object.png)


1. 将以下Web XDM变量映射到数据元素

   * **`web.webPageDetials.name`** to `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** to `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** to `%page.pageInfo.hierarchie1%`

   ![XDM对象](assets/data-element-xdm.content.png)

1. 接下来，查找 `identityMap` 对象，然后选择该对象

1. 映射到 `identityMap.loginID` 数据元素

1. 选择 **[!UICONTROL 保存]**

   ![数据收集界面](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




在这些步骤的末尾，您应创建以下数据元素：

| 核心扩展数据元素 | 平台Web SDK数据元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` |  |
| `page.pageInfo.server` |  |
| `user.profile.attributes.loggedIn` |  |
| `user.profile.attributes.username` |  |

在这些数据元素到位后，您便可以通过在标记中创建规则，通过XDM对象开始向Platform Edge Network发送数据。

[下一个： ](create-tag-rule.md)

>[!NOTE]
>
>感谢您花时间学习Adobe Experience Platform Web SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
