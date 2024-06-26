---
title: 使用Experience PlatformWeb SDK设置Adobe Analytics
description: 了解如何使用Experience PlatformWeb SDK设置Adobe Analytics。 本课程是《使用 Web SDK 实施 Adobe Experience Cloud》教程的一部分。
solution: Data Collection, Analytics
jira: KT-15408
exl-id: de86b936-0a47-4ade-8ca7-834c6ed0f041
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '2865'
ht-degree: 1%

---

# 使用Adobe Experience Platform Web SDK设置Adobe Analytics

了解如何使用设置Adobe Analytics [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/web-sdk/overview)，创建标记规则以将数据发送到Adobe Analytics，并验证Analytics是否按预期捕获数据。

[Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics) 是一款行业领先的应用程序，可帮助您充分了解客户的行为和需求，并根据客户情报掌控业务发展方向。

![Web SDK到Adobe Analytics的示意图](assets/dc-websdk-aa.png)

## 学习目标

在本课程结束后，您将能够：

* 配置数据流以启用Adobe Analytics
* 了解哪些标准XDM字段自动映射到Analytics变量
* 在数据对象中设置Analytics变量
* 通过覆盖数据流将数据发送到其他报表包
* 使用Debugger和Assurance验证Adobe Analytics变量

## 先决条件

要完成本课程，您必须首先：

* 熟悉并访问Adobe Analytics。

* 至少具有一个测试/开发报表包ID。 如果您没有可在本教程中使用的测试/开发报表包， [请创建一个](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

* 完成本教程的初始配置和标记配置部分中之前的课程。

## 配置数据流

Platform Web SDK将数据从您的网站发送到PlatformEdge Network。 然后，您的数据流会告知PlatformEdge Network，您的数据应该发送到哪个Adobe Analytics报表包。

1. 转到 [数据收集](https://experience.adobe.com/#/data-collection){target="blank"} 界面
1. 在左侧导航中，选择 **[!UICONTROL 数据流]**
1. 选择之前创建的 `Luma Web SDK: Development Environment` 数据流

   ![选择Luma Web SDK数据流](assets/datastream-luma-web-sdk-development.png)

1. 选择 **[!UICONTROL 添加服务]**
   ![向数据流添加服务](assets/datastream-analytics-addService.png)
1. 选择 **[!UICONTROL Adobe Analytics]** 作为 **[!UICONTROL 服务]**
1. 输入 **[!UICONTROL 报表包ID]** 开发报表包的
1. 选择 **[!UICONTROL 保存]**

   ![数据流保存分析](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >通过选择添加更多报表包 **[!UICONTROL 添加报表包]** 等同于多包标记。

>[!WARNING]
>
>在本教程中，您将仅为开发环境配置Adobe Analytics报表包。 在为您自己的网站创建数据流时，您应该为暂存环境和生产环境创建其他数据流和报表包。

## 设置Analytics变量

有多种方法可以在Web SDK实施中设置Analytics变量：

1. XDM字段到Analytics变量的自动映射（自动）。
1. 在中设置字段 `data` 对象（推荐）。
1. 在Analytics处理规则中将XDM字段映射到Analytics变量（不再推荐）。
1. 直接在XDM架构中映射到Analytics变量（不再推荐）。

自2024年5月起，您不再需要创建XDM模式来使用Platform Web SDK实施Adobe Analytics。 此 `data` 对象(以及 `data.variable` 您在中创建的数据元素 [创建数据元素](create-data-elements.md) 课程)可用于设置所有自定义Analytics变量。 现有Analytics客户将会很熟悉在数据对象中设置这些变量，并且比使用处理规则界面更有效，还可以防止不必要的数据占用实时客户配置文件中的空间(如果您有Real-time Customer Data Platform或Journey Optimizer，这一点很重要)。

### 自动映射的字段

许多XDM字段会自动映射到Analytics变量。 有关最新的映射列表，请参阅 [Analytics Experience Edge中的Adobe变量映射](https://experienceleague.adobe.com/en/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars).

出现以下情况时，会发生这种情况 _即使您尚未定义自定义架构_. Experience PlatformWeb SDK会自动收集一些数据，并将其作为XDM字段发送到PlatformEdge Network。 例如，Web SDK读取当前页面URL并将其作为XDM字段发送 `web.webPageDetails.URL`. 此字段将转发到Adobe Analytics，并且它会自动在Adobe Analytics中填充页面URL报表。

如果您使用XDM架构实施适用于Adobe Analytics的Web SDK，如本教程中所述，则您已经自定义实施了一些自动映射到Analytics变量的XDM字段，如下表所述：

| XDM到Analytics的自动映射变量 | Adobe Analytics变量 |
|-------|---------|
| `identitymap.ecid.[0].id` | mid |
| `web.webPageDetails.name` | s.pageName |
| `web.webPageDetails.server` | s.server |
| `web.webPageDetails.siteSection` | s.channel |
| `commerce.productViews.value` | prodView |
| `commerce.productListViews.value` | scView |
| `commerce.checkouts.value` | scCheckout |
| `commerce.purchases.value` | 购买 |
| `commerce.order.currencyCode` | s.currencyCode |
| `commerce.order.purchaseID` | s.purchaseID |
| `productListItems[].SKU` | s.products=；产品名称；；；；；（主要 — 请参阅下面的注释） |
| `productListItems[].name` | s.products=；产品名称；；；；；（回退 — 请参阅下面的注释） |
| `productListItems[].quantity` | s.products=；；product quantity；；； |
| `productListItems[].priceTotal` | s.product=；；；产品价格；； |

Analytics产品字符串的各个部分通过下的不同XDM变量进行设置。 `productListItems` 对象。

>[!NOTE]
>
>截至2022年8月18日， `productListItems[].SKU` 具有映射到s.products变量中的产品名称的优先级。
>值设置为 `productListItems[].name` 仅在以下情况下映射到产品名称： `productListItems[].SKU` 不存在。 否则，它将被取消映射，并可用于上下文数据。
>请勿将空字符串或null设置为 `productListItems[].SKU`. 这会产生不需要的效果，即映射到s.products变量中的产品名称。


### 在数据对象中设置变量

但evar、prop和事件呢？ 在中设置变量 `data` 推荐使用Web SDK来设置这些Analytics变量。 在数据对象中设置变量还可以覆盖任何自动映射的变量。

首先，什么是 `data` 对象？ 在任何Web SDK事件中，您可以使用自定义数据发送两个对象，即 `xdm` 对象和 `data` 对象。 两者都会发送到PlatformEdge Network，但仅限 `xdm` 对象将发送到Experience Platform数据集。 中的属性 `data` 对象可以在Edge上映射到 `xdm` 字段使用为数据收集准备数据功能，否则不会发送到Experience Platform。 这使其成为将数据发送到Analytics等并非基于Experience Platform构建的原生应用程序的理想方式。

以下是通用Web SDK调用中的两个对象：

![数据和xdm对象](assets/analytics-data-object-intro.png)

Adobe Analytics配置为在 `data.__adobe.analytics` 对象，并将其用于Analytics变量。

现在，让我们看看这是如何运行的。 让我们设置 `eVar1` 和 `prop1` 页面名称，并了解如何覆盖XDM映射的值

1. 打开标记规则 `all pages - library loaded - set global variables - 1`
1. 添加新 **[!UICONTROL 操作]**
1. 选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 扩展
1. 选择 **[!UICONTROL 操作类型]** 作为 **[!UICONTROL 更新变量]**
1. 选择 `data.variable` 作为 **[!UICONTROL 数据元素]**
1. 选择 **[!UICONTROL 分析]** 对象
1. 设置 `eVar1` 作为 `page.pageInfo.pageName` 数据元素
1. 设置 `prop1` 以复制 `eVar1`
1. 要测试XDM映射值的覆盖，请在 **[!UICONTROL 其他属性]** 部分将页面名称设置为静态值 `test`
1. 保存规则


现在，我们需要在发送事件规则中包含数据对象。

1. 打开标记规则 `all pages - library loaded - send event - 50`
1. 打开 **[!UICONTROL 发送事件]** 操作
1. 选择 `data.variable` 作为 **[!UICONTROL 数据]**
1. 选择 **[!UICONTROL 保留更改]**
1. 选择 **[!UICONTROL 保存]**



<!--


### Map to Analytics variables with processing rules

All fields in the XDM schema become available to Adobe Analytics as Context Data Variables with the following prefix `a.x.`. For example, `a.x.web.webinteraction.region`

In this exercise, you map one XDM variable to a prop. Follow these same steps for any custom mapping that you must do for any `eVar`, `prop`, `event`, or variable accessible via Processing Rules.

1. Go to the Analytics interface
1. Go to [!UICONTROL Admin] > [!UICONTROL Admin Tools] > [!UICONTROL Report Suites ]
1. Select the dev/test report suite that you are using for the tutorial > [!UICONTROL Edit Settings] > [!UICONTROL General] > [!UICONTROL Processing Rules]

    ![Analytics Purchase](assets/analytics-process-rules.png)   

1. Create a rule to **[!UICONTROL Overwrite value of]** `[!UICONTROL Product SKU (prop1)]` to `a.x.productlistitems.0.sku`. Remember to add a note about why you are creating the rule and name your rule title. Select **[!UICONTROL Save]**

    ![Analytics Purchase](assets/analytics-set-processing-rule.png)   

    >[!IMPORTANT]
    >
    >The first time you map to a processing rule, the UI does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.

### Map to Analytics variables using the Adobe Analytics field group

An alternative to processing rules is to map to Analytics variables in the XDM schema using the `Adobe Analytics ExperienceEvent Template` field group. This approach has gained popularity because many users find it simpler than configuring processing rules, however, by increasing the size of the XDM payload it could in turn increase the profile size in other applications like Real-Time CDP.

To add the `Adobe Analytics ExperienceEvent Template` field group to your schema:

1. Open the [Data Collection](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Select **[!UICONTROL Schemas]** from the left navigation
1. Make sure you are in the sandbox you are using from the tutorial
1. Open your `Luma Web Event Data` schema
1. In the **[!UICONTROL Field Groups]** section, select **[!UICONTROL Add]**
1. Find the `Adobe Analytics ExperienceEvent Template` field group and add it to your schema


Now, set a merchandising eVar in the product string. With the `Adobe Analytics ExperienceEvent Template` field group, you are able to map variables to merchandising eVars or events within the product string. This is also known as setting **Product Syntax Merchandising**. 

1. Go back to your tag property

1. Open the rule `ecommerce - library loaded - set product details variables - 20`

1. Open the **[!UICONTROL Set Variable]** action

1. Select to open `_experience > analytics > customDimensions > eVars > eVar1`

1. Set the **[!UICONTROL Value]** to `%product.productInfo.title%`

1. Select **[!UICONTROL Keep Changes]**

    ![Product SKU XDM object Variable](assets/set-up-analytics-product-merchandising.png)

1. Select **[!UICONTROL Save]** to save the rule

As you just saw, basically all of the Analytics variables can be set in the `Adobe Analytics ExperienceEvent Template` field group.

>[!NOTE]
>
> Notice the `_experience` object under `productListItems` > `Item 1`. Setting any variable under this [!UICONTROL object] sets Product Syntax eVars or Events.

-->

## 将数据发送到其他报表包

您可能希望更改当访客出现在某些页面中时，要将哪些Adobe Analytics报表包数据发送到。 这需要数据流和规则中的配置。

### 为报表包覆盖配置数据流

要在数据流中配置Adobe Analytics报表包覆盖设置，请执行以下操作：

1. 打开您的数据流
1. 编辑 **[!UICONTROL Adobe Analytics]** 通过打开 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) 菜单，然后选择 **[!UICONTROL 编辑]**

   ![覆盖数据流](assets/datastream-edit-analytics.png)

1. 选择 **[!UICONTROL 高级选项]** 以打开 **[!UICONTROL 报表包覆盖]**

1. 选择要覆盖的报表包。 在本例中， `Web SDK Course Dev` 和 `Web SDK Course Stg`

1. 选择 **[!UICONTROL 保存]**

   ![覆盖数据流](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


### 为报表包覆盖配置规则

让我们创建一个规则以向其他报表包发送额外的页面查看调用。 使用数据流覆盖功能，使用以下方式更改页面的报表包： **[!UICONTROL 发送事件]** 操作。

1. 创建新规则，将其命名为 `homepage - library loaded - AA report suite override - 51`

1. 选择下的加号 **[!UICONTROL 事件]** 添加新触发器

1. 下 **[!UICONTROL 扩展名]**，选择 **[!UICONTROL 核心]**

1. 下 **[!UICONTROL 事件类型]**，选择 **[!UICONTROL Library Loaded (Page Top)]**

1. 选择以打开 **[!UICONTROL 高级选项]**，键入 `51`. 这可确保规则在 `all pages - library loaded - send event - 50` 设置基线XDM **[!UICONTROL 更新变量]** 操作类型。
1. 选择 **[!UICONTROL 保留更改]**

   ![Analytics报表包覆盖](assets/set-up-analytics-rs-override.png)

1. 下 **[!UICONTROL 条件]**，选择以 **[!UICONTROL 添加]**

1. 离开 **[!UICONTROL 逻辑类型]** 作为 **[!UICONTROL 常规]**

1. 离开 **[!UICONTROL 扩展]** 作为 **[!UICONTROL 核心]**

1. 选择 **[!UICONTROL 完成情况类型]** 作为 **[!UICONTROL 不含查询字符串的路径]**

1. 在右边，离开 **[!UICONTROL 正则表达式]** 切换已禁用

1. 下 **[!UICONTROL 路径等于]** 设置 `/content/luma/us/en.html`. 对于Luma演示站点，它确保规则仅在主页上触发

1. 选择 **[!UICONTROL 保留更改]**

   ![Analytics报表包覆盖条件](assets/set-up-analytics-override-condition.png)

1. 下 **[!UICONTROL 操作]** 选择 **[!UICONTROL 添加]**

1. 作为 **[!UICONTROL 扩展名]**，选择 **[!UICONTROL Adobe Experience Platform Web SDK]**

1. 作为 **[!UICONTROL 操作类型]**，选择 **[!UICONTROL 发送事件]**

1. 作为 **[!UICONTROL XDM数据]**，选择 `xdm.variable.content` 您在中创建的数据元素 [创建数据元素](create-data-elements.md) 课程

1. 作为 **[!UICONTROL 数据]**，选择 `data.variable` 您在中创建的数据元素 [创建数据元素](create-data-elements.md) 课程

   ![Analytics数据流覆盖](assets/set-up-analytics-datastream-override-1.png)

1. 向下滚动到 **[!UICONTROL 数据流配置覆盖]** 部分

1. 离开 **[!UICONTROL 开发]** 选项卡处于选中状态。

   >[!TIP]
   >
   >    此选项卡确定覆盖发生在哪个标记环境中。 对于此练习，您只指定了开发环境，但在将此体验部署到生产环境时，请记得也在 **[!UICONTROL 生产]** 环境。

1. 选择 **[!UICONTROL 沙盒]** 在本教程中，您将使用
1. 选择 **[!UICONTROL 数据流]**，在本例中 `Luma Web SDK: Development Environment`

1. 下 **[!UICONTROL 报表包]**，选择要覆盖的报表站点。 在本例中， `tmd-websdk-course-stg`.

1. 选择 **[!UICONTROL 保留更改]**

1. 和 **[!UICONTROL 保存]** 您的规则

   ![Analytics数据流覆盖](assets/analytics-tags-report-suite-override.png)


## 构建开发环境

将更新后的规则添加到 `Luma Web SDK Tutorial` 标记库并重新构建开发环境。

恭喜！下一步是通过Experience PlatformWeb SDK验证Adobe Analytics实施。

## 使用Debugger验证Adobe Analytics

了解如何使用Experience PlatformDebugger的边缘跟踪功能验证Adobe Analytics是否正在捕获ECID、页面查看次数、产品字符串和电子商务事件。

在 [调试程序](validate-with-debugger.md) 在本课程中，您已了解如何使用Platform Debugger和浏览器开发人员控制台检查客户端XDM请求，这与您调试 `AppMeasurement.js` Analytics实施。 您还了解了如何验证发送到Adobe应用程序的平台Edge Network服务器端请求，以及如何使用Assurance查看完全处理的负载。

要验证Analytics是否通过Experience PlatformWeb SDK正确捕获数据，您必须进一步执行两个步骤：

1. 使用Experience PlatformDebugger的边缘跟踪功能，验证平台Edge Network上XDM对象如何处理数据
1. 使用Adobe Experience Platform保障验证Analytics完全处理数据的方式

### Experience CloudID验证

1. 转到 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}
1. 选择右上角的登录按钮，并使用凭据u： test@adobe.com p：测试进行身份验证
1. 打开Experience PlatformDebugger并 [将网站上的tag属性切换到您自己的开发资产](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)


1. 要启用边缘跟踪，请转到Experience Platform调试器，在左侧导航中，选择 **[!UICONTROL 日志]**，然后选择 **[!UICONTROL Edge]** 选项卡，然后选择 **[!UICONTROL 连接]**

   ![连接边缘跟踪](assets/analytics-debugger-edgeTrace.png)

1. 现在它将为空

   ![连接的边缘跟踪](assets/analytics-debugger-edge-connected.png)

1. 刷新“Luma”页面并再次检查Experience Platform调试器，您应该会看到数据通过。 以开头的行 **[!UICONTROL Analytics自动映射]** 是Adobe Analytics信标
1. 选择以打开 `[!UICONTROL mappedQueryParams]` 下拉列表和查看Analytics变量的第二个下拉列表

   ![Analytics信标边缘跟踪](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >第二个下拉列表对应于您要将数据发送到的分析报表包ID。 它应该与您自己的报表包匹配，而不是与屏幕快照中的报表包匹配。

1. 向下滚动以查找 `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. 它是一个捕获ECID的上下文数据变量
1. 一直向下滚动直到看到Analytics `[!UICONTROL mid]` 变量。 两个ID均与设备的Experience CloudID匹配。
1. 在Luma网站上，

   ![Analytics ECID](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >由于您已登录，请花些时间验证经过身份验证的ID `112ca06ed53d3db37e4cea49cc45b71e` 对于用户 **`test@adobe.com`** 也被捕获到 `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`

### 报表包覆盖验证

在上面，您为配置了数据流覆盖 [Luma主页](https://luma.enablementadobe.com/content/luma/us/en.html).  验证此配置的步骤

1. 查找包含 **[!UICONTROL 应用覆盖后的数据流配置]**. 在这里，您可以找到为报表包覆盖配置的主报表包和其他报表包。

   ![Analytics报表包覆盖列表验证](assets/aep-debugger-datastream-override.png)

1. 向下滚动到以开头的行 **[!UICONTROL Analytics自动映射]**  并确认 `[!UICONTROL reportSuiteIds]` 显示您在覆盖配置中指定的报表包

   ![Analytics报表包覆盖调用验证](assets/aep-debugger-analytics-report-suite-override.png)

### 内容页面查看次数验证

转到产品页面，如 [Didi Sport Watch产品页](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  验证Analytics是否捕获了内容页面查看。

1. 查找 `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. 向下滚动以查看 `[!UICONTROL gn]` 变量。 它是的Analytics动态语法 `[!UICONTROL s.pageName]` 变量。 它从数据层捕获页面名称。

   ![Analytics产品字符串](assets/analytics-debugger-edge-page-view.png)

### 产品字符串和电子商务事件验证

由于您已在产品页面上，因此本练习将继续使用相同的边缘跟踪来验证Analytics捕获的产品数据。 产品字符串和电子商务事件都会自动将XDM变量映射到Analytics。 只要您已映射到适当的 `productListItem` XDM变量，而 [为Adobe Analytics配置XDM架构](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics)，PlatformEdge Network负责将数据映射到适当的Analytics变量。

**首先验证 `Product String` 已设置**

1. 查找 `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. 变量会捕获您映射到 `productListItems.item1.sku` 本课程前面部分
1. 同时查找 `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. 变量会捕获您映射到的数据元素值 `productListItems.item1._experience.analytics.customdimensions.evars.evar1`
1. 向下滚动以查看 `[!UICONTROL pl]` 变量。 它是Analytics产品字符串变量的动态语法
1. 请注意，数据层中的产品名称会同时映射到 `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` 和 `[!UICONTROL product]` 产品字符串的参数。  此外，数据层中的产品标题会映射到products string中的推销evar1。

   ![Analytics产品字符串](assets/analytics-debugger-prodstring.png)

   边缘跟踪处理 `commerce` 事件与略有不同 `productList` 维度。 您不会看到上下文数据变量以与查看产品名称映射到的方式相同的方式进行映射 `[!UICONTROL c.a.x.productlistitem.[0].name]` 以上。 取而代之的是，边缘描摹显示Analytics中的最终事件自动映射 `event` 变量。 只要您映射到适当的XDM，平台Edge Network就会相应地映射它 `commerce` 变量while [为Adobe Analytics配置架构](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics)；在这种情况下， `commerce.productViews.value=1`.

1. 返回Experience Platform调试器窗口，向下滚动到 `[!UICONTROL events]` 变量中，它被设置为 `[!UICONTROL prodView]`

1. 另请注意 `[!UICONTROL c.a.x.eventType]` 设置为 `commerce.productViews` 因为您位于产品页面上。

   >[!TIP]
   >
   > 此 `ecommerce - pdp library loaded - AA (order 20)` 规则正在覆盖的值 `eventType` 由 `all pages global content variables - library loaded - AA (order 1)` 规则，因为该规则设置为在序列中稍后触发


   ![Analytics产品视图](assets/analytics-debugger-prodView.png)

**验证为Analytics设置的其余电子商务事件和产品字符串**

1. 添加 [滴滴出行手表](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) 到购物车
1. 转到 [购物车页面](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html)，检查边缘跟踪

   * `eventType` 设置为 `commerce.productListViews`
   * `[!UICONTROL events: "scView"]`、和
   * 设置product string

   ![Analytics购物车查看](assets/analytics-debugger-cartView.png)

1. 继续结帐，检查边缘跟踪

   * `eventType` 设置为 `commerce.checkouts`
   * `[!UICONTROL events: "scCheckout"]`、和
   * 设置product string

   ![Analytics签出](assets/analytics-debugger-checkout.png)

1. 仅填写 **名字** 和 **姓氏** 填写发货单上的字段并选择 **继续**. 在下一页，选择 **下单**
1. 在确认页面上，检查边缘跟踪

   * `eventType` 设置为 `commerce.purchases`
   * 正在设置购买事件 `[!UICONTROL events: "purchase"]`
   * 正在设置的货币代码变量 `[!UICONTROL cc: "USD"]`
   * 在中设置了购买ID `[!UICONTROL pi]`
   * 产品字符串 `[!UICONTROL pl]` 设置产品名称、数量和价格

   ![Analytics购买](assets/analytics-debugger-purchase.png)



## 使用Assurance验证Adobe Analytics

Adobe Experience Platform Assurance可帮助您检查、验证、模拟和验证您收集数据或向网站和移动应用程序提供体验的方式。

在上一个练习中，您已验证Adobe Analytics是否通过Experience PlatformDebugger的边缘跟踪功能来捕获ECID、页面查看次数、产品字符串以及电子商务事件。  接下来，使用Adobe Experience Platform Assurance验证这些相同的事件，这是用于在Edge Trace中访问相同数据的替代界面。

正如您在 [Assurance](validate-with-assurance.md) 课程，有几种方法可启动保证会话。 由于您已经使用上一个练习中启动的边缘跟踪会话打开了Adobe Experience Platform Debugger，因此我们建议您通过Debugger访问Assurance：
![通过Adobe Experience Platform数据收集提供保证](assets/assurance-open-aep-debugger.png)

在 **[!UICONTROL “Web SDK教程3”]** 进入保证会话 **[!UICONTROL &quot;hitdebugger&quot;]** 放到事件搜索栏中，将结果筛选为Adobe Analytics后处理数据。
![保证Adobe分析后处理数据](assets/assurance-hitdebugger.png)

### Experience CloudID验证

要验证Adobe Analytics是否正在捕获ECID，请选择一个信标并打开有效负载。  此信标的供应商应为 **[!UICONTROL com.adobe.analytics.hitdebugger]**
![使用Assurance进行Adobe Analytics验证](assets/assurance-hitdebugger-payload.png)

然后向下滚动到 **[!UICONTROL mcvisId]** 以验证是否已正确捕获ECID
![使用保证进行Experience CloudID验证](assets/assurance-hitdebugger-mcvisId.png)

### 内容页面查看次数验证

使用相同的信标，验证内容页面查看是否已映射到正确的Adobe Analytics变量。
向下滚动到 **[!UICONTROL pageName]** 以验证 `Page Name` 正确捕获
![使用保证进行页面名称验证](assets/assurance-hitdebugger-content-pagename.png)

### 产品字符串和电子商务事件验证

按照使用上述Experience Platform调试器进行验证时所使用的相同验证用例，继续使用相同的信标来验证 `Ecommerce Events` 和 `Product String`.

1. 查找有效负荷，其中 **[!UICONTROL 事件]** contain `prodView`
   ![带保证的产品字符串验证](assets/assurance-hitdebugger-prodView-event.png)
1. 向下滚动到 **[!UICONTROL 产品字符串]** 验证 `Product String`.
   * 请注意 `Product SKU` 和 `Merchandizing eVar1`.
1. 进一步向下滚动并验证 `prop1`（在上一部分中使用处理规则配置的）包含 `Product SKU`\
   ![带保证的促销变量验证的产品字符串](assets/assurance-hitdebugger-prodView-productString-merchVar.png)

通过查看购物车、结帐和购买事件来继续验证实施。

1. 查找有效负荷，其中 **[!UICONTROL 事件]** contain `scView` 并验证产品字符串。
   ![带保证的产品字符串验证](assets/assurance-hitdebugger-scView-event.png)
1. 查找有效负荷，其中 **[!UICONTROL 事件]** contain `scCheckout` 并验证产品字符串。
   ![带保证的产品字符串验证](assets/assurance-hitdebugger-scView-event.png)
1. 查找有效负荷，其中 **[!UICONTROL 事件]** contain `purchase`
   ![带保证的产品字符串验证](assets/assurance-hitdebugger-purchase-event.png)
1. 验证 `purchase` 事件，请注意 `Product String` 应包含 `Product SKU`， `Product Quantity` 、和 `Product Total Price`.
1. 此外，对于 `purchase` 验证 `purchase-id` 和/或 `purchaseId` 已设置


恭喜！你做到了！ 在本课程结束时，您已准备好使用Platform Web SDK为您自己的网站实施Adobe Analytics。

[下一步： ](setup-audience-manager.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
