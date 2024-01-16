---
title: 使用Platform Web SDK设置Web渠道
description: 了解如何使用Platform Web SDK实施Web渠道。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '2463'
ht-degree: 0%

---


# 使用Platform Web SDK设置Web渠道

了解如何使用Platform Web SDK实施Web渠道。 本指南介绍了基本Web渠道先决条件、配置的详细步骤，并深入研究了以忠诚度状态为中心的用例。

通过遵循本指南，Journey Optimizer用户能够使用Journey Optimizer Web Designer有效地将Web渠道应用于高级在线个性化。

## 学习目标

在本课程结束时，您能够：

* 了解Web SDK在提供Web渠道体验中的功能和意义。
* 利用示例Luma忠诚度奖励用例，从头到尾了解创建Web渠道营销活动的过程。
* 在界面中配置促销活动属性、操作和计划。
* 了解Adobe Experience Cloud可视化编辑帮助程序扩展的功能和好处。
* 了解如何使用Web设计器编辑网页内容，包括图像、标题和其他元素。
* 了解如何使用优惠决策组件将优惠插入到网页中。
* 熟悉确保Web渠道营销活动质量和成功的最佳实践。

## 先决条件

要完成此部分中的课程，您必须首先：

* 确保您的AEP Web SDK版本为2.16或更高版本。
* 如果您使用Journey Optimizer Web设计器创作您的Web渠道体验，请确保您使用的是Google Chrome或Microsoft® Edge浏览器。
* 另外，请确保已下载Adobe Experience Cloud可视化编辑帮助程序浏览器扩展。 在创建Web渠道体验之前，在浏览器工具栏中启用可视化编辑帮助程序浏览器扩展。
   * 在Journey Optimizer Web设计器中，由于以下原因之一，某些网站可能无法可靠地打开：
      1. 网站具有严格的安全策略。
      1. 网站嵌入在iframe中。
      1. 无法从外部访问客户的QA或暂存站点（它是一个内部站点）。
* 确保您的浏览器允许使用第三方Cookie。 可能还需要在浏览器中禁用任何广告拦截器。
* 创建Web体验并包含Adobe Experience Manager Assets Essentials库中的内容时，必须配置用于发布此内容的子域。 [了解详情](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/web-delegated-subdomains.html?lang=en)。
* 如果使用内容试验功能，请确保您的Web数据集也包含在报表配置中。
* 目前，支持两种类型的实施，以便能够在Web资产上创作和交付Web渠道营销活动：
   * 仅限客户端：要修改您的网站，必须实施Adobe Experience Platform Web SDK。
   * 混合模式：您可以利用AEP Edge Network服务器API来请求个性化服务器端。 来自API的响应随后会提供给Adobe Experience Platform Web SDK，以便在客户端进行修改。 有关更多信息，请参阅Adobe Experience Platform Edge Network服务器API文档。 可以在这篇博客文章中找到混合模式的其他详细信息和实施示例。

>[!NOTE]
>
>当前不支持仅服务器端实施。

## 术语

首先，您应该了解Web渠道营销活动中使用的术语。

* **Web渠道**：通过Web进行通信或内容投放的媒体。 在本指南的上下文中，它介绍了在Adobe Journey Optimizer中使用Platform Web SDK向网站访客交付个性化内容的机制。
* **Web表面**：指由交付内容的URL标识的Web属性。 它可以包含单个或多个网页。
* **Journey Optimizer Web Designer**：Journey Optimizer中的特定工具或界面，用户可在其中设计其Web渠道体验。
* **Adobe Experience Cloud可视化编辑帮助程序**：一种浏览器扩展，可帮助以可视方式编辑和设计Web渠道体验。
* **数据流**：Adobe Experience Platform服务中的一种配置，可确保提供Web渠道体验。
* **合并策略**：确保准确激活和发布入站营销活动的配置。
* **受众**：符合特定标准的用户或网站访客的特定区段。
* **Web设计器**：一种界面或工具，可帮助直观地编辑和设计Web体验，而无需深入了解代码。
* **表达式编辑器**：Web Designer中的一种工具，允许用户向Web内容添加个性化，可能基于数据属性或其他标准。
* **优惠决策组件**：Web Designer中的组件，可帮助根据决策管理确定哪个选件最适合向特定访客显示。
* **内容试验**：测试不同内容变体的方法，以确定哪些变体在所需量度（如集客点击）方面表现最佳。
* **处理**：在内容实验的上下文中，处理是指对照其他内容进行测试的特定内容变体。
* **模拟**：一种预览机制，用于在为实时受众激活Web渠道体验之前对其进行可视化。

## 配置数据流

确保在Adobe Experience Platform服务中定义了数据流，并启用了Adobe Journey Optimizer选项。 必须先配置此设置，然后才能通过Platform Web SDK提供任何Web渠道体验。

要在数据流中配置Adobe Journey Optimizer，请执行以下操作：

1. 转到数据收集界面。
1. 在左侧导航中，选择 **数据流**.
1. 选择之前创建的Luma Web SDK数据流。

   ![选择数据流](../assets/web-channel-select-datastream.png)

1. 选择 **编辑** 在Adobe Experience Platform服务中。

   ![编辑数据流](../assets/web-channel-edit-datastream.png)

1. 查看 **Adobe Journey Optimizer** 盒子。

   ![选中AJO框](../assets/web-channel-check-ajo-box.png)

1. 选择&#x200B;**保存**。

这可确保Adobe Experience Platform Edge正确处理Journey Optimizer的入站事件。

## 配置合并策略

确保使用定义了合并策略 **Active-On-Edge合并策略** 选项已启用。 Journey Optimizer集客渠道可使用此合并策略选项，以确保在边缘准确地激活和发布集客营销活动。

要在合并策略中配置选项，请执行以下操作：

1. 转到 **客户>用户档案** 界面。
1. 在导航中，选择 **合并策略**.
1. 选择您的策略，然后切换 **Active-On-Edge合并策略** 内的选项 **配置** 步骤。

   ![切换合并策略](..//assets/web-channel-active-on-edge-merge-policy.png)

## 为内容试验配置Web数据集

要在Web渠道营销活动中使用内容实验，必须确保使用的Web数据集也包含在报表配置中。 Journey Optimizer报表系统以只读方式使用数据集来填充OOTB内容试验报表。

[有关为内容试验报告添加数据集的详情，请参阅此部分](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/content-experiment/reporting-configuration.html?lang=en#add-datasets).

## 用例概述 — 忠诚度奖励

在本课程中，一个忠诚度奖励用例用于详细介绍使用Web SDK实施Web渠道体验。

此用例使您能够更好地了解Journey Optimizer如何利用Journey Optimizer营销活动和Web设计器，帮助您为客户提供最佳入站体验。

>[!NOTE]
>
>由于本教程面向实施者，因此需要注意的是，本课程涉及AJO中的大量UI工作。 虽然此类UI任务通常由营销人员处理，但对于实施者而言，深入了解该流程可能会很有用，即使他们最终不负责Web渠道营销活动创建也是如此。

### 创建忠诚度奖励营销活动

让我们从Adobe Journey Optimizer中创建忠诚度奖励网络渠道营销活动开始。

要创建示例营销活动，请执行以下操作：

1. 在左侧导航中导航到历程管理>促销活动
1. 单击 **创建营销活动** 在右上角。
1. 在 **属性** 部分，指定您希望如何执行活动。 对于“忠诚度奖励”用例，请选择 **已计划**.

   ![计划的营销活动](../assets/web-channel-campaign-properties-scheduled.png)

1. 在 **操作** 部分，选择 **Web渠道**. 在这个阶段，还要选择Web界面。

>[!NOTE]
>
>Web表面是指由交付内容的URL标识的Web属性。 它可以对应于单个页面URL或包含多个页面，使您能够在一个或多个网页中应用修改。

选择 **页面URL** Web表面选项，用于将体验部署在此营销活动的一个页面上。 输入Luma页面的URL。

1. 定义Web曲面后，选择 **创建**.

   ![选择Web表面](../assets/web-channel-web-surface.png)

1. 现在向新的Web渠道营销活动添加一些其他详细信息。 首先，命名营销活动。 调用它&#39;*Luma忠诚度奖励 — 金牌状态 — 2023年10月*’。 （可选）您可以向市场活动添加描述。 同时添加 **标记** 以改进整个营销活动分类。

   ![命名营销活动](../assets/web-channel-campaign-name.png)

1. 默认情况下，该营销活动对所有网站访客有效。 对于此用例，只有金会员状态奖励会员才能看到体验。 要启用此功能，请单击 **选择受众** 并选择“*Luma忠诚度奖励 — 金牌状态*&#39;受众。

1. 在 **身份命名空间** 字段中，选择用于标识所选区段内个人的命名空间。 由于您要将促销活动部署在Luma网站上，因此可以选择ECID命名空间。 &#39;中的配置文件&#x200B;*Luma忠诚度奖励 — 金牌状态*&#39;各种身份中缺少ECID命名空间的受众不会成为Web渠道营销活动的目标。

   ![选择身份类型](../assets/web-channel-indentity-type.png)

1. 使用安排促销活动在12月1日开始 **营销活动开始** 期权，并于12月31日终止使用 **营销活动结束** 选项。

   ![Campaign计划](../assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>请记住，对于Web渠道营销活动，Web体验会在访客打开页面时显示。 因此，与Adobe Journey Optimizer中的其他类型的营销活动不同， **操作触发器** 部分不可配置。

### 尝试忠诚度奖励内容

在 **操作** 部分，您可以选择创建一个试验，以测试哪些内容更适合&#39;*Luma忠诚度奖励 — 金牌状态*&#39;受众。 让我们创建并测试两个处理作为Campaign配置的一部分。

要创建内容试验，请执行以下操作：

1. 单击 **创建试验**.

   ![创建试验](../assets/web-channel-create-content-experiment.png)

1. 首先选择 **成功量度**. 这是确定内容有效性的量度。 选择 **独特入站点击次数**，以了解哪种内容处理方式在Web体验CTA上产生了更多的点击次数。

   ![选择成功量度](../assets/web-channel-content-experiment-metric.png)

1. 使用Web渠道设置试验并选择 **入站点击次数**， **独特入站点击次数**， **页面查看次数**，或 **独特页面查看次数** 量度， **单击操作** 利用下拉列表，可精确跟踪和监控特定页面上的点击次数和查看次数。

1. （可选）您可以指定 **保留样本** 两种疗法都没有用。 暂时取消选中此项。

1. （可选）选择 **均匀分布**. 选中此选项可确保始终平均拆分处理拆分。

[详细了解Adobe Journey Optimizer Web Channel中的内容实验](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/content-experiment/get-started-experiment.html?lang=en).

### 使用可视化帮助程序编辑内容

现在，让我们创作Web渠道体验。 要实现此目的，请使用Adobe Experience Cloud **可视化帮助程序**. 此工具是一个与Google Chrome和Microsoft® Edge兼容的浏览器扩展。 在尝试构建体验之前，请确保已下载该扩展。 还要确保网页包含Web SDK。

1. 在 **操作** 选项卡，单击 **编辑内容**. 由于您输入了单个页面URL作为表面，因此您应该可以在编辑器中开始工作。

   ![编辑内容](../assets/web-channel-edit-content.png)

1. 现在，单击 **编辑网页** 以开始创作。

   ![编辑网页](../assets/web-channel-edit-web-page.png)

1. 首先，使用Web编辑器编辑某些元素。 使用上下文菜单编辑Luma主页图像标题。 调整右侧上下文窗格的样式。

   ![添加上下文编辑](../assets/web-channel-some-contextual-edit.png)

1. 还可以使用将个性化内容添加到容器中 **表达式编辑器**.

   ![添加个性化内容](../assets/web-channel-add-basic-personalization.png)

1. 确保正确跟踪点击体验。 选择 **点击跟踪元素** 从上下文菜单中。

   ![点击跟踪](../assets/web-channel-click-tracking.png)

1. 使用 **优惠决策组件** 以在网页中插入选件。 此组件使用 **决策管理** 以选择向Luma访客提供的最佳选件。


### HTML设计更改

如果您希望将更高级的更改或自定义的更改作为忠诚度奖励促销活动的一部分，可以使用一些方法。

使用 **组件** 窗格，用于将HTML或其他内容直接添加到Luma网站。

![浏览组件窗格](../assets/web-channel-components-pane.png)

在页面顶部添加新的HTML组件。 从设计界面编辑组件中的HTML或 **上下文** 窗格。

![添加自定义HTML](../assets/web-channel-add-html-component.png)

或者，从添加HTML编辑 **修改** 窗格。 此窗格允许您在页面上选择一个组件，然后从设计器界面中对其进行编辑。

在编辑器中，添加&#39;的HTML *Luma忠诚度奖励 — 金牌状态*&#39;受众。 单击 **验证**.

![验证HTML](../assets/web-channel-add-custom-html-validate.png)

现在，查看新的自定义HTML组件以了解其适用情况。

![查看自定义HTML](../assets/web-channel-review-custom-html.png)

使用编辑特定组件 **CSS选择器类型** 修改。

![修改CSS](../assets/web-channel-css-selector.png)

使用添加自定义代码 **页面 `<head>` type** 修改。

![修改head](../assets/web-channel-page-head-modification.png)

使用 **可视化帮助程序**.

### 模拟忠诚度奖励内容

在激活营销活动之前，查看已修改网页的预览。 请记住，您必须将测试用户档案配置为模拟Web渠道体验。

要模拟体验，请执行以下操作：

1. 选择 **模拟内容** 在营销活动中。

   ![模拟内容](../assets/web-channel-simulate-content.png)

1. 选择要接收模拟的测试用户档案。 请记住，测试用户档案应位于“*Luma忠诚度奖励 — 金牌状态*”受众获得适当的对待。

1. 将显示测试用户档案的预览。

### 激活忠诚度奖励营销活动

最后，激活Web渠道营销活动。

1. 选择 **审查以激活**.

1. 系统会提示您最后一次确认促销活动详细信息。 选择 **激活**. 营销活动最多可能需要15分钟才能在网站上处于活动状态。

### 忠诚度奖励QA

作为最佳实践，请监控 **Web** 定位的KPI的营销活动实时报表和全局报表的选项卡。 对于此营销活动，监视体验展示次数，然后单击率。

![查看Web报表](../assets/web-channel-web-report.png)

### 使用Adobe Experience Platform Debugger进行Web渠道验证

可用于Chrome和Firefox的Adobe Experience Platform Debugger扩展可分析您的网页，以识别Adobe Experience Cloud解决方案实施中的问题。

您可以使用Luma网站上的调试器来验证生产环境中的Web渠道体验。 在忠诚度奖励用例启动并运行后，这是一种最佳实践，可确保正确配置所有内容。

[使用此处指南了解如何在浏览器中配置调试器](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html?lang=en).

要使用调试器开始验证，请执行以下操作：

1. 导航到具有Web渠道体验的Luma网页。
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 在网页上，打开 **Adobe Experience Platform debugger**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 导航到 **摘要**. 验证 **数据流ID** 匹配 **数据流** 在 **Adobe数据收集** 您已为其启用Adobe Journey Optimizer的。
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 然后，您可以使用各种Luma忠诚度帐户登录网站，并使用该调试器验证发送到Adobe Experience Platform Edge网络的请求。
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 下 **解决方案** 导航至 **Experience PlatformWeb SDK**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 在 **配置** 选项卡，打开 **启用调试**. 这将启用会话日志记录 **Adobe Experience Platform Assurance** 会话。
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 使用各种Luma忠诚度帐户登录网站，然后使用调试器验证发送到 **Adobe Experience Platform Edge network**. 所有这些请求都应捕获到 **Assurance** 用于日志跟踪。
<!--
   ![ADD SCREENSHOT](#)
-->