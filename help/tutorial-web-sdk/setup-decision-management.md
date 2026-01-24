---
title: 使用Platform Web SDK设置Journey Optimizer决策管理
description: 了解如何使用Platform Web SDK实施决策管理。 本课程是《使用 Web SDK 实施 Adobe Experience Cloud》教程的一部分。
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Decision Management,Offers
jira: KT-15412
exl-id: f7852ef4-44b0-49df-aec8-cb211726247d
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 1%

---

# 使用Platform Web SDK设置决策管理

了解如何使用Platform Web SDK实施Adobe Journey Optimizer的决策管理功能。 本指南介绍了基本的决策管理先决条件、配置的详细步骤，并深入研究了以忠诚度状态为中心的用例。

通过学习本教程，Journey Optimizer用户能够使用决策管理功能，增强其客户交互的个性化和相关性。


![Web SDK和Adobe Analytics关系图](assets/dc-websdk-ajo.png)

## 学习目标

在本课程结束时，您能够：

* 掌握Adobe Journey Optimizer中决策管理的核心概念及其与Adobe Experience Platform Web SDK的集成。

* 了解为Offer Decisioning配置Web SDK的分步流程，确保与Journey Optimizer无缝集成。

* 探索以忠诚度状态优惠为中心的详细用例，深入了解如何有效创建和管理优惠、决策和投放。

* 了解决策管理框架中的基本术语及其影响。

* 了解决策规则、收藏集限定符和备用选件在向正确用户提供正确选件方面的重要性。

* 深入了解模拟和自定义事件数据收集等高级主题，让您能够测试、验证和增强优惠交付机制。

## 先决条件

要完成此部分中的课程，您必须首先：

* 确保您的组织有权访问Adobe Journey Optimizer Ultimate(Journey Optimizer和Offer Decisioning)或Adobe Experience Platform以及Offer Decisioning加载项。

* 完成关于Platform Web SDK初始配置的所有课程。

* 为您的组织启用Edge Decisioning。

* 了解如何配置投放位置，并在决策范围JSON中实例化投放位置和活动ID。

## 限制

Adobe Journey Optimizer当前不支持基于事件的优惠。 如果您基于事件创建决策规则，则无法在优惠中应用它。

## 授予对决策管理的访问权限

要授予对决策管理功能的访问权限，您必须创建&#x200B;**产品配置文件**，并为用户分配相应的权限。 [在本节](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/access-control/privacy/high-low-permissions#decisions-permissions)中了解有关管理Journey Optimizer用户和权限的更多信息。

## 配置数据流

必须先在&#x200B;**数据流**&#x200B;配置中启用Offer Decisioning，Platform Web SDK才能交付任何决策管理活动。

要在数据流中配置Offer Decisioning，请执行以下操作：

1. 转到[数据收集](https://experience.adobe.com/#/data-collection)接口。

1. 在左侧导航中，选择&#x200B;**数据流**。

1. 选择之前创建的Luma Web SDK数据流。

   ![选择数据流](assets/decisioning-datastream-select.png)

1. 在&#x200B;**Adobe Experience Platform服务**&#x200B;中选择&#x200B;**编辑**。

   ![编辑服务](assets/decisioning-edit-datastream.png)

1. 选中&#x200B;**Offer Decisioning**&#x200B;框。

   ![添加屏幕快照](assets/decisioning-check-offer-box.png)

1. 选择&#x200B;**保存**。

这可确保&#x200B;**Adobe Experience Platform Edge**&#x200B;正确处理Journey Optimizer的入站事件。

## 为决策管理配置SDK

根据Web SDK实施类型，决策管理需要其他SDK步骤。 有两个可用选项可用于为决策管理配置SDK。

* SDK独立安装
   1. 使用您的`sendEvent`配置`decisionScopes`操作。

      ```javascript
      alloy("sendEvent", {
         ...
         "decisionScopes": [
            "[DECISION SCOPE 1]",
            "[DECISION SCOPE 2]"
         ]
      })
      ```

* SDK标记安装
   1. 转到数据收集界面。

   1. 在左侧导航中，选择&#x200B;**标记**。

      ![选择标记](assets/decisioning-data-collection-tags.png)

   1. 选择&#x200B;**标记属性**。

   1. 创建您的&#x200B;**规则**。
      * 添加Platform Web SDK **发送事件操作**，并将相关的`decisionScopes`添加到该操作的配置中。

   1. 创建并发布包含所有已配置的相关&#x200B;**规则**、**数据元素**&#x200B;和&#x200B;**扩展**&#x200B;的&#x200B;**库**。

## 术语

首先，您应该了解决策管理界面中使用的术语。

* **上限**：指示优惠出现频率的约束。 两种类型：
   * 总上限：选件在目标受众中可以显示的最大次数。
   * 配置文件上限：向特定用户显示选件的次数。
* **收藏集**：按营销人员设置的特定条件分组的优惠子集，例如，优惠类别。
* **决策**：指示优惠选择的逻辑。
* **决策规则**：优惠约束以了解用户的资格。
* **合格选件**：与预设约束匹配并可向用户显示的选件。
* **决策管理**：使用业务逻辑和决策规则精心编制和分发个性化优惠的系统。
* **后备优惠**：用户不符合集合中任何优惠资格时显示的默认优惠。
* **选件**：具有确定查看者的潜在资格规则的营销消息。
* **优惠库**：管理优惠、决策和相关规则的中央存储库。
* **个性化优惠**：根据资格约束定制的自定义营销消息。
* **位置**：向用户显示优惠的设置或方案。
* **优先级**：优惠的排名量度，考虑各种约束，如资格和上限。
* **演示文稿**：特定于渠道的信息，例如，用于指导优惠显示的位置或语言。

## 用例概述 — 忠诚度奖励

在本课程中，您将实施一个忠诚度奖励示例用例，以了解使用Web SDK的决策管理。

此用例使您能够更好地了解Journey Optimizer如何利用集中式优惠库和决策管理决策引擎来帮助为客户提供最佳优惠。

>[!NOTE]
>
> 由于本教程面向实施者，因此需要注意的是，本课程涉及Journey Optimizer中的大量界面工作。 虽然此类界面任务通常由营销人员处理，但对于实施者而言，将insight纳入流程可能会很有用，即使他们并不负责决策管理营销活动的长期创建。

## 组件

在开始创建选件之前，必须定义多个必备组件。

### 创建忠诚度优惠的版面

**投放位置**&#x200B;是用于展示优惠的容器。 在此示例中，您在Luma网站顶部创建一个版面。

可在&#x200B;**组件**&#x200B;菜单中访问版面列表。 您可以使用过滤器来帮助您根据特定渠道或内容检索投放位置。

![查看投放位置](assets/decisioning-placements-list.png)

要创建投放位置，请执行以下步骤：

1. 单击&#x200B;**创建版面**。

   ![创建版面](assets/decisioning-create-placement.png)

1. 定义投放位置的属性：
   * **名称**：投放位置的名称。 让我们调用示例位置&#x200B;*&#39;主页横幅&#39;*。
   * **渠道类型**：用于投放位置的渠道。 让我们使用&#x200B;*&#39;Web&#39;*，因为选件显示在Luma网站上。
   * **内容类型**：允许投放位置显示的内容类型：文本、HTML、图像链接或JSON。 您可以将&#x200B;*&#39;HTML&#39;*&#x200B;用于选件。
   * **描述**：投放位置的描述（可选）。

   ![添加详细信息](assets/decisioning-placement-details.png)

1. 单击&#x200B;**保存**。
1. 创建投放位置后，该投放位置将显示在投放位置列表中。
1. 选择包含新版面的行并记下版面ID，因为这对于在决策范围内进行配置可能很有必要。

   ![查看版面ID &#x200B;](assets/decisioning-placement-id.png)

### 忠诚度状态的决策规则

**决策规则**&#x200B;指定提供优惠的条件。 在此示例中，您创建决策规则以根据用户的忠诚度状态提供不同的优惠。

决策规则列表可在&#x200B;**组件**&#x200B;菜单中访问。

要创建决策规则，请执行以下步骤：

1. 导航到&#x200B;**规则**&#x200B;选项卡，然后单击&#x200B;**创建规则**。

   ![创建规则](assets/decisioning-create-rule.png)

1. 让我们命名第一个规则“*金会员状态规则*”。 您可以使用XDM字段定义规则。 Adobe Experience Platform **区段生成器**&#x200B;是一个可用于生成规则条件的直观界面。

   ![定义规则](assets/decisioning-define-rule.png)

1. 单击&#x200B;**保存**&#x200B;以确认规则条件。
1. 新保存的“*金会员状态规则*”将显示在&#x200B;**规则列表**&#x200B;中。 选择它以显示其属性。

   ![查看已创建的规则](assets/decisioning-view-rules.png)

1. 现在，为该用例创建剩余的忠诚度优惠规则条件。


### 收藏集限定符

**收藏集限定符**&#x200B;允许您轻松地在选件库中组织和搜索选件。 在本例中，您将收藏集限定符添加到忠诚度奖励选件以改进选件组织。

集合限定符列表可在&#x200B;**组件**&#x200B;菜单中访问。

要创建忠诚度奖励收集限定词，请执行以下步骤：

1. 导航到&#x200B;**集合限定符**&#x200B;选项卡，然后单击&#x200B;**创建集合限定符**。

   ![创建集合限定符](assets/decisioning-create-collection-qualifier.png)

1. 让我们命名集合限定符“*忠诚度奖励*”

   ![命名集合](assets/decisioning-name-collection.png)

1. 新的集合限定符现在应显示在&#x200B;**集合限定符**&#x200B;选项卡中

## 产品建议

现在，该创建忠诚度奖励优惠了。

可在&#x200B;**选件**&#x200B;菜单中访问选件列表。

![查看优惠菜单](assets/decisioning-offers-menu.png)


### 创建不同忠诚度级别的优惠

首先为不同的Luma忠诚度级别创建个性化优惠。

要创建第一个&#x200B;**选件**，请执行以下步骤：

1. 单击&#x200B;**创建优惠**，然后选择&#x200B;**个性化优惠**。

1. 让我们命名第一个选件“*Luma忠诚度级别 — 金级*”。 您必须为此选件指定开始/结束日期和时间。 您还应将&#x200B;**收藏集限定词**“*忠诚度奖励*”关联到选件，以便更好地在&#x200B;**选件库**&#x200B;中进行组织。 之后，单击&#x200B;**下一步**。

   ![添加优惠详细信息](assets/decisioning-add-offer-details.png)

1. 现在，您必须添加&#x200B;**呈现**&#x200B;以定义优惠的显示位置。 让我们选择&#x200B;**Web渠道**。 让我们也选择您之前配置的“*主页横幅*”**位置**。 选定的&#x200B;**投放位置**&#x200B;是HTML类型，因此您可以使用&#x200B;**自定义**&#x200B;单选按钮直接将HTML、JSON或TEXT内容添加到编辑器以构建选件。

   ![添加呈现详细信息](assets/decisioning-add-representation-details.png)

1. 直接使用&#x200B;**表达式编辑器**&#x200B;编辑选件内容。 请记住，您可以将HTML、JSON或TEXT内容添加到此投放位置。 请确保根据您的内容类型在编辑器底部选择正确的&#x200B;**模式**。 您还可以点击&#x200B;**验证**&#x200B;以确保没有错误。

   ![添加选件HTML](assets/decisioning-add-offer-html.png)

1. 此外，您可以使用表达式编辑器检索存储在Adobe Experience Platform中的属性。 让我们将用户档案的名字添加到优惠内容中，以便更好地为1:1级别的忠诚度会员进行个性化。

   ![添加优惠个性化](assets/decisioning-add-offer-personalization.png)

1. 添加约束以仅显示符合“*金会员状态规则*”的用户档案的优惠。

   ![添加规则约束](assets/decisioning-add-rule-constraint.png)

1. 查看完选件后，单击&#x200B;**完成**。 选择&#x200B;**保存并批准**。

现在为各个Luma忠诚度级别创建其余优惠

### 后备优惠

您仍希望向Luma网站的非Luma忠诚度访客提供选件。 为此，您可以为该营销活动配置&#x200B;**后备优惠**。

要创建后备优惠，请执行以下步骤：

1. 单击&#x200B;**创建选件**，然后选择&#x200B;**后备选件**。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 让我们命名后备优惠“*非Luma忠诚度*”。 您还可以将之前创建的&#x200B;**收藏集限定符**、“*忠诚度奖励*”关联到后备优惠，以便轻松组织优惠。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 将后备选件内容添加到&#x200B;**表达式编辑器**。 请记住，您可以将HTML、JSON或TEXT内容添加到此投放位置。 请确保根据您的内容类型在编辑器底部选择正确的&#x200B;**模式**。 您还可以点击&#x200B;**验证**&#x200B;以确保没有错误。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 如果一切配置正确，请按&#x200B;**完成**，然后按&#x200B;**保存并批准**。
<!--
   ![ADD SCREENSHOT](#)
-->

## 决策

**决策**&#x200B;是优惠的容器，这些优惠会根据目标为客户选择最佳优惠。

决策列表可在&#x200B;**优惠**&#x200B;菜单的&#x200B;**决策**&#x200B;选项卡中找到。
<!--
   ![ADD SCREENSHOT](#)
-->

### 创建忠诚度优惠决策

让我们为Luma忠诚度奖励用例创建决策。

要创建决策，请执行以下步骤：

1. 单击&#x200B;**创建决策**。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 让我们调用决策“*12月Luma忠诚度优惠*”。 选件应持续1个月，因此我们在此处指定它。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 现在，您必须定义&#x200B;**决策范围**。 首先，选择投放位置。 您可以使用以前创建的“*主页横幅*”。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 接下来，必须为决策范围添加&#x200B;**评估标准**。 单击“**添加**”，然后选择之前创建的“*忠诚度奖励*”**集合，其中包含要考虑的所有忠诚度优惠。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在“*忠诚度奖励*”集合中，您可以使用资格字段将优惠投放限制为Luma访客的子集。 但是，对于此用例，您希望每个访客都收到一个选件。 请记住，您为所有不忠诚的访客配置了&#x200B;**后备优惠**。 将资格设置为“无”。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 此外，如果多个选件符合用户/投放组合的条件，则可以使用&#x200B;**排名方法**&#x200B;字段为每个Luma访客选择最佳选件。 对于此用例，您可以使用&#x200B;**优惠优先级**&#x200B;方法，该方法使用优惠中定义的值来提供最佳优惠。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 现在将&#x200B;**后备优惠**&#x200B;添加到决策中。 提醒，如果Luma访客不属于任何Luma忠诚度受众，则备用选件是向Luma访客显示的默认选件。 从“*主页横幅*”版面的可用后备优惠列表中选择“*非Luma忠诚度*”。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在激活决策之前，我们先查看决策范围、后备优惠、预览可用优惠并评估符合条件的用户档案。 一旦一切看起来正常，您可以单击&#x200B;**完成**&#x200B;和&#x200B;**保存并激活**。
<!--
   ![ADD SCREENSHOT](#)
-->

## 模拟

作为最佳实践，您应该验证Luma忠诚度决策逻辑，以确保将正确的选件交付给正确的忠诚度受众。 您可以使用&#x200B;**测试配置文件**&#x200B;来执行此验证。 在将新选件版本推送到生产环境之前，最好通过测试用户档案测试对选件所做的更改。

要开始测试，请从&#x200B;**选件**&#x200B;菜单中选择&#x200B;**模拟**&#x200B;选项卡。

### 测试忠诚度优惠

1. 选择要用于模拟的测试用户档案。 单击&#x200B;**管理配置文件**。 [要创建或指定新的测试配置文件以进行选件测试，请遵循本指南](https://experienceleague.adobe.com/zh-hans/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles#create-test-profiles-csv)。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 将一个或多个测试用户档案添加到模拟中，并保存您的选择。 对于用例测试，您应确保已为每个Luma忠诚度奖励受众配置了测试用户档案。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 选择要测试的决策范围。 选择&#x200B;**添加决策范围**。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 选择之前创建的“*主页横幅*”位置。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 将显示可用的决策，选择之前创建的“*12月Luma忠诚度优惠*”决策，然后单击“**添加**”。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 选择测试配置文件后，单击&#x200B;**查看结果**。 针对“*12月Luma忠诚度优惠*”决策向选定的测试配置文件显示最佳可用优惠。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 选择其他测试配置文件，然后单击&#x200B;**查看结果**。 理想情况下，您应该看到不同的模拟选件，与测试用户档案的忠诚度等级相对应。

## 使用Adobe Experience Platform Debugger进行决策管理验证

适用于Chrome和Firefox的&#x200B;**Adobe Experience Platform Debugger**&#x200B;扩展可分析您的网页，以识别Adobe Experience Cloud解决方案实施中的问题。

您可以使用Luma网站上的调试器来验证生产中的决策逻辑。 忠诚度奖励用例启动并运行后，此验证是一种很好的做法，可确保一切配置正确。

[通过此处](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/data-collection/debugger/overview)了解如何使用指南在浏览器中配置调试器。

要使用调试器开始验证，请执行以下操作：

1. 导航到包含优惠版面的Luma网页。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在网页上，打开&#x200B;**Adobe Experience Platform Debugger**。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 导航到&#x200B;**摘要**。 验证&#x200B;**数据流ID**&#x200B;是否与您启用了Offer Decisioning的&#x200B;**Adobe数据收集**&#x200B;中的&#x200B;**数据流**&#x200B;匹配。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在&#x200B;**解决方案**&#x200B;下，导航到&#x200B;**Experience Platform Web SDK**。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在&#x200B;**配置**&#x200B;选项卡中，打开&#x200B;**启用调试**。 这将启用&#x200B;**Adobe Experience Platform Assurance**&#x200B;会话中会话的日志记录。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 然后，您可以使用各种Luma忠诚度帐户登录网站，并使用调试器验证发送到&#x200B;**Adobe Experience Platform Edge网络**&#x200B;的请求。 所有这些请求都应在&#x200B;**Assurance**&#x200B;中捕获以进行日志跟踪。
<!--
   ![ADD SCREENSHOT](#)
-->

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=zh-Hans)上分享这些内容
