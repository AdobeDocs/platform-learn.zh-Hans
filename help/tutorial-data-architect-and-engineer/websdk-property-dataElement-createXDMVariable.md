---
title: 引入流数据
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 引入流数据
description: 在本课程中，您将使用Web SDK将数据流式传输到Experience Platform中。
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: 45fec5b2a82e12bdc4a9d017664e8c11d5625cef
workflow-type: tm+mt
source-wordcount: '2966'
ht-degree: 0%

---

# 引入流数据

<!--1hr-->

在本课程中，您将使用Adobe Experience Platform Web SDK流式传输数据。

>[!WARNING]
>
> 本教程中使用的Luma网站预计将在2026年2月16日这一周内被替换。 作为本教程的一部分完成的工作可能不适用于新网站。

数据收集任务分为两个主要任务：

* 在Luma网站上实施Web SDK以将客户事件流式传输到Experience Platform Edge Network。

* 配置数据流以告知Edge Network在Experience Platform中将数据转发到我们的`Luma Web Events Dataset`。

**数据工程师**&#x200B;需要在此教程之外摄取流数据。 虽然Web开发人员通常在网站中实施Web SDK，但了解此过程的工作原理非常重要。 即使您不是Web开发人员，您也应该能够完成此基本实施。

在开始练习之前，请观看这两个简短视频，详细了解流数据引入和Web SDK：

>[!VIDEO](https://video.tv.adobe.com/v/31669?captions=chi_hans&learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/37264?captions=chi_hans&learn=on&enablevpops)

>[!NOTE]
>
>虽然本教程侧重于通过Web SDK从网站流式摄取，但您也可以使用[Mobile SDK](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/implement-mobile-sdk/overview)、[Edge Network Server API](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/data-collection/server-api/overview)和[HTTP API](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/streaming/http)流式传输数据。

## 需要权限

在[配置权限](configure-permissions.md)课程中，您已设置完成本课程所需的所有访问控制。


## 配置数据流

首先，我们将配置数据流。 数据流会告知Experience Platform Edge Network在从Web SDK调用收到数据后将数据发送到何处。 例如，是否要将数据发送到Experience Platform、Adobe Analytics或Adobe Target？

![Web SDK、数据流和Edge Network关系图](assets/dc-websdk-datastreams.png)

要创建您的[!UICONTROL 数据流]：

1. 确保您仍然在` Luma Tutorial`沙盒中
1. 在左侧导航中选择&#x200B;**[!UICONTROL 数据流]**
1. 选择右上角的&#x200B;**[!UICONTROL 新建数据流]**&#x200B;按钮

   ![在左侧导航中选择数据流](assets/websdk-datastream-newDatastream.png)


1. 对于&#x200B;**[!UICONTROL Name]**，输入`Luma Platform Tutorial` （如果贵公司的多个人员参加本教程，请添加您的姓名到结尾）
1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;按钮

   ![命名数据流并保存](assets/websdk-datastream-name.png)

数据到达Edge后，[!UICONTROL 数据流]会将其转发到配置的[!UICONTROL 服务]。 要将数据发送到Experience Platform，请执行以下操作：

1. 选择&#x200B;**[!UICONTROL 添加服务]**
   ![添加服务](assets/websdk-datastream-addService.png)

1. 选择`Adobe Experience Platform`
1. 选择您的`Luma Web Events Dataset`
1. 选择&#x200B;**[!UICONTROL 保存]**

   ![选择您的数据集并保存](assets/websdk-datastream-addPlatformService.png)

尽管数据流配置中有一个“配置文件数据集”选项，但不应使用此选项将普通的XDM个人配置文件数据发送到Platform。 此设置只应用于发送同意、推送令牌和用户活动区域详细信息。

[!UICONTROL Offer Decisioning]、[!UICONTROL Edge分段]、[!UICONTROL Personalization目标]和[!UICONTROL Adobe Journey Optimizer]的复选框允许您在Edge上激活数据，但本教程中并未使用这些复选框。

## 实施Web SDK

### 添加属性

首先，我们必须创建标记属性（以前称为标记属性）。 资产是一个容器，其中包含从网页收集详细信息并将其发送到不同位置所需的所有JavaScript、规则和其他功能。

要创建资产，请执行以下操作：

1. 在左侧导航中转到&#x200B;**[!UICONTROL 标记]**
1. 选择&#x200B;**[!UICONTROL 新属性]**
   ![添加新属性](assets/websdk-property-addNewProperty.png)
1. 作为&#x200B;**[!UICONTROL Name]**，输入`Luma Platform Tutorial` （如果贵公司的多个人员参加本教程，请添加您的姓名到结尾）
1. 作为&#x200B;**[!UICONTROL 域]**，请输入`enablementadobe.com`（稍后解释）
1. 选择&#x200B;**[!UICONTROL 保存]**
   ![属性详细信息](assets/websdk-property-propertyDetails.png)


### 将扩展添加到资产

现在您有了资产，可以使用扩展添加Web SDK。 扩展是一个代码包，用于向标记属性和实施添加功能。 要添加扩展，请执行以下操作：

1. 打开您的标记属性
1. 在左侧导航中转到&#x200B;**[!UICONTROL 扩展]**
1. 转到&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡
1. 有许多扩展可用于标记。 使用术语`Web SDK`筛选目录
1. 选择&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;扩展以打开侧面板
1. 选择&#x200B;**[!UICONTROL 安装]**&#x200B;按钮
   ![安装Adobe Experience Platform Web SDK扩展](assets/websdk-property-addExtension.png)
1. Web SDK扩展有多种配置可用，但在本教程中，我们将只配置两种。 将&#x200B;**[!UICONTROL Edge域]**&#x200B;更新为`data.enablementadobe.com`。 此设置允许您在Web SDK实施中设置第一方Cookie，我们鼓励这样做。 在您自己的网站上实施Web SDK时，我们建议您为自己的数据收集目的创建一个CNAME，例如`data.YOUR_DOMAIN.com`
1. 在&#x200B;**[!UICONTROL 数据流]**&#x200B;部分中，对于生产环境，选择您的`Luma Tutorial`沙盒和`Luma Platform Tutorial`数据流。
1. 您可以查看其他配置选项（但不要更改它们！），然后选择&#x200B;**[!UICONTROL 保存]**
   ![配置Web SDK扩展](assets/websdk-property-configureExtension.png)

从扩展目录屏幕中，安装Adobe Client Data Layer扩展。 此扩展将帮助我们从Luma网站读取数据层：

![安装Adobe客户端数据层扩展](assets/websdk-property-installACDLExtension.png)

扩展中不需要任何配置，因此只需将其保存到库即可。

## 创建规则以发送数据

现在，我们将创建一个规则以将数据发送到Platform。 规则是指示标记执行操作的事件、条件和操作的组合。 要创建规则，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 规则]**
1. 选择&#x200B;**[!UICONTROL 创建新规则]**&#x200B;按钮
   ![创建规则](assets/websdk-property-createRule.png)
1. 将规则命名为 `adobeDataLayer event`
1. 在&#x200B;**[!UICONTROL 事件]**&#x200B;下，选择&#x200B;**[!UICONTROL 添加]**&#x200B;按钮
   ![命名规则并添加事件](assets/websdk-property-nameRule.png)
1. 使用&#x200B;**[!UICONTROL Adobe Client Data Layer]** **[!UICONTROL 扩展]**&#x200B;并选择&#x200B;**[!UICONTROL 推送的数据]**&#x200B;作为&#x200B;**[!UICONTROL 事件类型]**。
1. 选择&#x200B;**[!UICONTROL 侦听]**。 **[!UICONTROL 所有活动]**。
1. 选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以返回主规则屏幕
   ![添加Library Loaded事件](assets/websdk-property-addEvent.png)
1. 在&#x200B;**[!UICONTROL 操作]**&#x200B;下，选择&#x200B;**[!UICONTROL 添加]**&#x200B;按钮
1. 使用&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]** **[!UICONTROL 扩展]**&#x200B;并选择&#x200B;**[!UICONTROL 发送事件]**&#x200B;作为&#x200B;**[!UICONTROL 操作类型]**
1. 在右侧，从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Web Webpagedetails页面查看次数]**。 这将填充我们`Luma Web Events Schema`的eventType字段
1. 选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以返回主规则屏幕
   ![添加“发送事件”操作](assets/websdk-property-addAction.png)
1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存规则\
   ![保存规则](assets/websdk-property-saveRule.png)

## 在库中发布规则

接下来，我们将将规则发布到开发环境，以便验证它是否有效。


要创建库，请执行以下操作：

1. 在左侧导航中转到&#x200B;**[!UICONTROL 发布流]**
1. 选择&#x200B;**[!UICONTROL 添加库]**
   ![选择“添加库”](assets/websdk-property-pubAddNewLib.png)
1. 对于&#x200B;**[!UICONTROL Name]**，输入`Luma Platform Tutorial`
1. 对于&#x200B;**[!UICONTROL 环境]**，请选择`Development`
1. 选择&#x200B;**[!UICONTROL Add All Changed Resources]**&#x200B;按钮。 (除了[!UICONTROL Adobe Experience Platform Web SDK]扩展和`adobeDataLayer event`规则之外，您还将看到添加的[!UICONTROL Core]扩展包含所有标记Web属性所需的基本JavaScript。)
1. 选择&#x200B;**[!UICONTROL Save &amp; Build for Development]**&#x200B;按钮
   ![创建并生成库](assets/websdk-property-buildLibrary.png)

库可能需要几分钟才能构建，完成后，库名称左侧会显示一个绿色圆点：
![生成完成](assets/websdk-property-buildComplete.png)

如您在[!UICONTROL 发布流]屏幕上所见，发布流程还有许多内容超出了本教程的范围。 我们将在开发环境中使用单个库。

## 验证请求中的数据

### 添加Adobe Experience Platform Debugger

Experience Platform Debugger是适用于Chrome的扩展，可帮助您查看在网页中实施的Adobe技术。 下载首选浏览器的版本：

* [Chrome扩展](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您以前从未使用过该调试器，则可能需要观看以下时长为5分钟的概述视频：

>[!VIDEO](https://video.tv.adobe.com/v/35858?captions=chi_hans&learn=on&enablevpops)

### 打开Luma网站

在本教程中，我们使用公开托管版本的Luma演示网站。 让我们打开它并将其加入书签：

1. 在新的浏览器选项卡中，打开[Luma网站](https://newluma.enablementadobe.com)。
1. 将页面加入书签以便在本教程的其余部分中使用

此托管网站是我们为什么在初始标记属性配置的`enablementadobe.com`Domains[!UICONTROL 字段中使用]，以及为什么在`data.enablementadobe.com`Adobe Experience Platform Web SDK[!UICONTROL 扩展中使用]作为第一方域的原因。 我有个计划！

![Luma主页](assets/websdk-luma-homepage.png)

### 使用Experience Platform Debugger映射到您的标记属性

Experience Platform Debugger具有一项酷炫功能，允许您使用其他标记属性替换现有标记属性。 这有助于验证，并允许您跳过本教程中的许多实施步骤。

1. 确保已打开Luma网站并选择Experience Platform Debugger扩展图标
1. 调试器将会打开并显示硬编码实施的一些详细信息，这些详细信息与本教程无关（在打开调试器后，您可能需要重新加载Luma网站）
1. 确认Debugger已“**[!UICONTROL 连接到Luma]**”（如下图所示），然后选择“**[!UICONTROL 锁定]**”图标以将Debugger锁定到Luma网站。
1. 选择右上角的&#x200B;**[!UICONTROL 登录]**&#x200B;按钮进行身份验证。
1. 现在转到左侧导航栏中的&#x200B;**[!UICONTROL Experience Platform标记]**
1. 选择配置选项卡
1. 右侧显示&#x200B;**[!UICONTROL 页面嵌入代码]**，打开&#x200B;**[!UICONTROL 操作]**&#x200B;下拉列表，然后选择&#x200B;**[!UICONTROL 替换]**
   ![选择“操作”>“替换”](assets/websdk-debugger-replaceLibrary.png)
1. 由于您已经过身份验证，调试器将会拉入您的可用标记属性和环境。 选择您的`Luma Platform Tutorial`属性
1. 选择您的`Development`环境
1. 选择&#x200B;**[!UICONTROL 应用]**&#x200B;按钮
   ![选择备用标记属性](assets/websdk-debugger-selectProperty.png)
1. Luma网站现在将使用您的标记属性&#x200B;_重新加载_。
   已替换![标记属性](assets/websdk-debugger-propertyReplaced.png)
1. 转到左侧导航中的&#x200B;**[!UICONTROL 摘要]**，查看[!UICONTROL 标记]属性的详细信息
   ![摘要选项卡](assets/websdk-debugger-summary.png)
1. 现在转到左侧导航栏中的&#x200B;**[!UICONTROL Experience Platform Web SDK]**&#x200B;以查看&#x200B;**[!UICONTROL 网络请求]**
1. 选择&#x200B;**[!UICONTROL 事件]**&#x200B;行

   ![Adobe Experience Platform Web SDK请求](assets/websdk-debugger-platformNetwork.png)

1. 请注意我们如何查看在`web.webpagedetails.pageView`发送事件[!UICONTROL 操作中指定的]事件类型
   ![Adobe Experience Platform Web SDK请求](assets/websdk-debugger-eventDetails.png)


1. 请求详细信息也显示在浏览器的Web开发人员工具&#x200B;**网络**&#x200B;选项卡中。 打开并重新加载页面。 筛选具有`interact`的调用以查找该调用，选择它，然后查看&#x200B;**标头**&#x200B;选项卡，**请求有效负载**&#x200B;区域。
   ![网络选项卡](assets/websdk-debugger-networkTab.png)
1. 转到&#x200B;**响应**&#x200B;选项卡，并记下ECID值是如何包含在响应中的。 复制此值，因为您将在下一个练习中使用它来验证用户档案信息。
   ![网络选项卡](assets/websdk-debugger-networkTab-response.png)



## 在Experience Platform中验证数据

您可以通过查看`Luma Web Events Dataset`中到达的数据批来验证数据是否已登陆Platform。 (我知道，这被称为流式数据摄取，但现在我要说的是，它是批量获取的！ 它实时流式传输到用户档案，因此可用于实时分段和激活，但每15分钟会批量发送到数据湖。)

要验证数据：

1. 在Platform用户界面中，转到左侧导航中的&#x200B;**[!UICONTROL 数据集]**
1. 打开`Luma Web Events Dataset`并确认批次已到达。 请记住，它们每15分钟发送一次，因此您可能需要等待批次显示。
1. 选择&#x200B;**[!UICONTROL 预览数据集]**&#x200B;按钮
   ![打开数据集](assets/websdk-platform-dataset.png)
1. 在预览模式中，请注意如何选择左侧的架构的不同字段来预览这些特定数据点：
   ![预览字段](assets/websdk-platform-datasetPreview.png)

您还可以确认新配置文件是否显示：

1. 在Platform用户界面中，转到左侧导航中的&#x200B;**[!UICONTROL 配置文件]**
1. 选择&#x200B;**[!UICONTROL ECID]**&#x200B;命名空间并搜索您的ECID值（从响应中复制）。 该配置文件将具有其自己的ID，与ECID分开。
1. 选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;以打开配置文件
   ![查找并打开配置文件](assets/websdk-platform-openProfile.png)
1. 选择&#x200B;**[!UICONTROL 事件]**&#x200B;选项卡以查看您查看的页面
   ![配置文件事件](assets/websdk-platform-profileEvents.png)\
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## 向事件添加自定义数据

Web SDK会自动填充许多XDM字段，但您将不可避免地需要自定义实施以从网站收集其他字段。 这其中涉及很多，但这里有一些简单的例子。

### 创建数据元素以存储XDM数据

1. 导航回您的`Luma Platform Tutorial`标记属性
1. 打开&#x200B;**[!UICONTROL 选择工作库]**&#x200B;下拉列表，然后选择您的`Luma Platform Tutorial`库。 此设置使得向库发布其他更新更加容易。
1. 现在转到左侧导航中的&#x200B;**[!UICONTROL 数据元素]**
1. 选择&#x200B;**[!UICONTROL 创建新数据元素]**&#x200B;按钮

   ![创建新数据元素](assets/websdk-property-createNewDataElement.png)

在&#x200B;**[!UICONTROL 数据元素]**&#x200B;页面上：


1. 作为&#x200B;**[!UICONTROL Name]**，输入`XDM data`
1. 对于&#x200B;**[!UICONTROL 扩展]**，请选择`Adobe Experience Platform Web SDK`
1. 作为&#x200B;**[!UICONTROL 数据元素类型]**，请选择`Variable`
1. 作为&#x200B;**[!UICONTROL 沙盒]**，选择您的`Luma Tutorial`沙盒
1. 作为&#x200B;**[!UICONTROL 架构]**，选择您的`Luma Web Events Schema`
1. 确保选择`Luma Platform Tutorial`作为工作库
1. 选择&#x200B;**[!UICONTROL 保存到库]**
   ![将页面名称映射到XDM对象数据元素](assets/websdk-property-dataElement-createXDMVariable.png)

### 为页面名称创建数据元素

1. 创建新数据元素
1. 作为&#x200B;**[!UICONTROL Name]**，输入`Page Name`
1. 作为&#x200B;**[!UICONTROL 数据元素类型]**，请选择`JavaScript Variable`
1. 对于&#x200B;**[!UICONTROL JavaScript变量名称]**，请输入`adobeDataLayer.0.page.name`
1. 为了帮助标准化值的格式，请选中&#x200B;**[!UICONTROL 强制小写值]**&#x200B;和&#x200B;**[!UICONTROL 清除文本]**&#x200B;的复选框
1. 选择&#x200B;**[!UICONTROL 保存到库]**
   ![为页面名称创建数据元素](assets/websdk-property-dataElement-pageName.png)


### 将XDM数据添加到您的“发送事件”操作

现在，您已将数据映射到XDM字段，下面可以将其包含在发送事件操作中：

1. 转到&#x200B;**[!UICONTROL 规则]**&#x200B;屏幕
1. 打开您的`adobeDataLayer event`规则
1. 打开`Adobe Experience Platform Web SDK - Send Event`操作
1. 作为&#x200B;**[!UICONTROL XDM]**，选择图标以打开数据元素选择模式并选择您的`XDM data`数据元素
1. 选择&#x200B;**[!UICONTROL 保留更改]**
   ![将XDM数据添加到发送事件操作](assets/websdk-property-addXDMtoSendEvent.png)

1. 向规则中添加新操作
1. 选择`Adobe Experience Platform Web SDK` **[!UICONTROL 扩展]**
1. 选择`Update Variable` **[!UICONTROL 操作类型]**
1. 将您的`Page Name`数据元素填充为`web.webPageDetails.name`
1. 选择&#x200B;**[!UICONTROL 保留更改]**
   ![将“更新变量”操作添加到您的规则](assets/websdk-property-addUpdateVariableAction.png)

1. 重新排列[!UICONTROL 操作]，以便[!UICONTROL 更新变量]在[!UICONTROL 发送事件]之前触发
1. 现在，由于您在上几个练习中选择了`Luma Platform Tutorial`作为工作库，您最近的更改已直接保存到库。 您只需打开下拉菜单并选择&#x200B;**[!UICONTROL Save to Library and Build]**，而不必通过“发布流”屏幕发布我们的更改
   ![保存到库并生成](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

这样将开始使用您刚刚进行的三项更改来构建新的标记库。

### 验证XDM数据

现在，在使用Debugger映射到您的标记属性时，您应该能够重新加载Luma主页，并且看到请求中填充了page name字段！
![验证XDM数据](assets/websdk-debugger-pageName.png)

您还可以通过预览数据集和配置文件，验证在Platform中收到的页面名称数据。

## 发送其他身份

您的Web SDK实施现在正在发送将Experience Cloud ID (ECID)作为主要标识符的事件。 ECID由Web SDK自动生成，每个设备和浏览器均是唯一的。 根据客户使用的设备和浏览器，一个客户可以拥有多个ECID。 那么，我们如何才能获得该客户的统一视图，并将其在线活动关联到我们的CRM、忠诚度和离线购买数据？ 我们通过在会话期间收集其他身份并允许Identity Service确定性地链接它们来实现这一点。

如果您还记得，我曾在[映射身份](map-identities.md)课程中提到我们将使用ECID和CRM ID作为Web数据的身份。 让我们使用Web SDK收集CRM ID！

### 为CRM ID添加数据元素

首先，将CRM ID存储在数据元素中：

1. 在标记界面中，添加名为`CRM Id`的数据元素
1. 对于&#x200B;**[!UICONTROL 数据元素类型]**，请选择&#x200B;**[!UICONTROL JavaScript变量]**
1. 对于&#x200B;**[!UICONTROL JavaScript变量名称]**，请输入`adobeDataLayer.0.user.id`
1. 选择&#x200B;**[!UICONTROL 保存到库]**&#x200B;按钮（`Luma Platform Tutorial`仍应该是您的工作库）
   ![添加CRM Id的数据元素](assets/websdk-property-dataElement-crmId.png)

### 将CRM ID添加到Identity Map数据元素

现在，我们已捕获CRM ID值，我们必须将其与名为[!UICONTROL 标识映射]数据元素的特殊数据元素类型相关联：

1. 添加名为`Identity Map`的数据元素
1. 作为&#x200B;**[!UICONTROL 扩展]**，请选择&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**
1. 作为&#x200B;**[!UICONTROL 数据元素类型]**，请选择&#x200B;**[!UICONTROL 标识映射]**
1. 作为&#x200B;**[!UICONTROL 命名空间]**，请选择或键入`Luma CRM Id`，它是我们在以前的课程中创建的[!UICONTROL 命名空间]。

1. 作为&#x200B;**[!UICONTROL ID]**，选择图标以打开数据元素选择模式并选择您的`CRM Id`数据元素
1. 作为&#x200B;**[!UICONTROL Authenticated State]**，请选择&#x200B;**[!UICONTROL Authenticated]**
1. 检查&#x200B;**[!UICONTROL 主要]**

   >[!TIP]
   >
   > Adobe建议将代表人员（如`Luma CRM Id`）的标识作为[!UICONTROL primary]标识发送。
   >
   > 如果身份映射包含人员标识符（例如，`Luma CRM Id`），则人员标识符将变为[!UICONTROL 主]身份。 否则，`ECID`将成为[!UICONTROL 主]标识。

1. 选择&#x200B;**[!UICONTROL 保存到库]**&#x200B;按钮（`Luma Platform Tutorial`仍应该是您的工作库）
   ![将CRM ID添加到身份映射数据元素](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>您可以使用[!UICONTROL 标识映射]数据类型传递多个标识符。

### 将身份映射数据元素添加到XDM变量

现在，我们必须更新规则中的XDM变量操作以包含身份映射。 别担心，我们差不多学完了！

1. 打开您的`adobeDataLayer event`规则
1. 打开`Update variable`操作
1. 将您的`Identity Map`数据元素选择到`identityMap` XDM字段。
1. 选择&#x200B;**[!UICONTROL 保留更改]**
   ![将IdentityMap数据元素添加到XDM对象](assets/websdk-property-dataElement-addIdentitiesToXDMVariable.png)
1. 由于您在上几个练习中选择了`Luma Platform Tutorial`作为工作库，请选择&#x200B;**[!UICONTROL 保存到库并生成]**

   ![保存并生成库](assets/websdk-property-saveAndBuild.png)

<!--U1770721295408-->

### 验证身份

要验证Web SDK现在是否正在发送CRM ID，请执行以下操作：

1. 打开[Luma网站](https://luma.enablementadobe.com/content/luma/us/en.html)
1. 按照之前的说明，使用Debugger将其映射到您的标记属性
1. 选择Luma网站右上角的&#x200B;**登录**&#x200B;链接
1. 使用凭据`test@test.com`/`test`登录
1. 通过身份验证后，在Debugger中检查Experience Platform Web SDK调用(最近请求的&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]** > **[!UICONTROL 网络请求]** > **[!UICONTROL 事件]**)，此时您应会看到`lumaCrmId`：
   ![在Debugger中验证身份](assets/websdk-debugger-confirmIdentity.png)
1. 使用ECID命名空间查找用户配置文件，然后再次查找值。 在配置文件中，您将看到CRM ID，以及忠诚度ID和配置文件详细信息，如姓名和电话号码。 所有身份和数据都已拼合到单个实时客户个人资料中！
   ![在Platform中验证身份](assets/websdk-platform-lumaCrmIdProfile.png)


## 其他资源

* [利用 Web SDK 实施 Adobe Experience Cloud](/help/tutorial-web-sdk/overview.md)
* [流式摄取文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=zh-Hans)
* [流式引入API引用](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)

做得好！这是关于Web SDK和标签的大量信息。 要全面实施，涉及的范围要大得多，但这些基础知识可帮助您入门，并在Platform中查看结果。

>[!NOTE]
>
>现在您已完成“流式摄取”课程，您可以从[!UICONTROL 产品配置文件中删除]Prod`Luma Tutorial Platform`沙盒


如果您愿意，请跳至[运行查询课程](run-queries.md)。

数据架构师，您可以转到[合并策略](create-merge-policies.md)！
