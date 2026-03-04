---
title: 验证Experience Platform Assurance的Web SDK实施
description: 了解如何使用 Adobe Experience Platform Assurance 验证您的 Platform Web SDK 实施。本课程是《使用 Web SDK 实施 Adobe Experience Cloud》教程的一部分。
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: 4e5fe50c1ec7a867fed57700b35851b859680fef
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# 验证Experience Platform Assurance的Web SDK实施

[Adobe Experience Platform Assurance](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/assurance/home)是一项功能，可帮助您检查、校对、模拟和验证收集数据或提供体验的方式。

如您在[配置数据流](configure-datastream.md)课程中所学的，Platform Web SDK会先将数据从您的数字资产发送到Platform Edge Network。 然后，Platform Edge Network会将数据转发到在数据流中启用的服务。 您可以使用Assurance验证传入和传出Platform Edge Network的请求。

![Web SDK和Adobe Experience Platform验证图](assets/dc-websdk-validation.png)


## 学习目标

在本课程结束后，您将能够：

* 启动Assurance会话
* 查看从Platform Edge Network发送或发送到的请求

## 先决条件

您熟悉数据收集标记和[Luma演示网站](https://luma.enablementadobe.com){target="_blank"}，并完成了本教程中以前的课程：

* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)
* [捕获身份](create-identities.md)
* [创建标记规则](create-tag-rule.md)
* [使用Debugger进行验证](validate-with-debugger.md)


## 启动和查看Assurance会话

有多种方法可启动Assurance会话。


### 在Debugger中启用Edge跟踪

要启用Edge跟踪，请执行以下操作：

1. 转到[Luma演示网站](https://luma.enablementadobe.com)并使用调试器[将网站上的标记属性切换到您自己的开发属性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 确保您已使用显示您的组织名称登录Debugger。 如果显示的是您的用户名，请注销并重新尝试登录。
1. 在&#x200B;**[!UICONTROL Experience Platform Debugger]**&#x200B;的左侧导航中，选择&#x200B;**[!UICONTROL 日志]**
1. 选择&#x200B;**[!UICONTROL Edge]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 连接]**

   ![连接Edge跟踪](assets/assurance-edgeTrace-connect.png)

1. 目前为空

   ![连接的Edge跟踪](assets/analytics-debugger-edge-connected.png)

1. 刷新[Luma主页](https://luma.enablementadobe.com/)并再次检查&#x200B;**[!UICONTROL Experience Platform Debugger]**，查看进入Platform Edge Network的数据。 在以后的课程中，当您在数据流中启用服务时，您将能够看到传出请求。

   Edge跟踪中的![请求](assets/validate-edge-trace.png)

   每次在Adobe Experience Platform Debugger中启用Edge跟踪时，都会在后台启动Assurance会话。 虽然您可以查看此处的信息，但您可能会发现Assurance界面更加有用。

1. 启用Edge跟踪后，您会在顶部看到一个传出链接图标。 选择图标以打开Assurance。

   ![启动Assurance会话](assets/validate-debugger-start-assurnance.png)

1. 此时将打开一个新的浏览器选项卡，其中包含Assurance界面。

### 从Assurance界面启动Assurance会话

1. 打开[数据收集接口](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. 在左侧导航中选择Assurance
1. 选择创建会话
   ![创建Assurance会话](assets/assurance-create-session.png)
1. 使用&#x200B;**[!UICONTROL 深层链接连接]**&#x200B;选项
1. 选择&#x200B;**[!UICONTROL 开始]**
1. 为会话命名，例如`Luma Web SDK validation`
1. 作为&#x200B;**[!UICONTROL 基本URL]**，输入`https://luma.enablementadobe.com/`
   ![命名Assurance会话](assets/assurance-name-session.png)
1. 在下一个屏幕中，选择&#x200B;**[!UICONTROL 复制链接]**
1. 选择图标以将链接复制到剪贴板
1. 将URL粘贴到浏览器中，这将打开带有特殊URL参数`adb_validation_sessionid`的Luma网站并启动会话
1. 在Assurance界面中，您应该会看到一条消息，指示已成功连接到会话，并且您应该会看到Assurance界面中捕获的事件。
   ![Assurance会话已连接](assets/assurance-success.png)

## 验证Web SDK实施的当前状态

在实施过程的此阶段，可查看的信息有限，因为我们还未启用数据流中的任何服务。

### 使用`Alloy Request`查看来自Web SDK的传入请求

我们可以查看来自Web SDK的传入点击，因为它已被Edge接收：

1. 选择`Alloy Request`行
1. 查看原始事件（或展开[!UICONTROL 有效负载] > `ACPExtensionEventData`中的节点），直到您找到具有熟悉变量的XDM对象：

   ![Alloy请求](assets/assurance-alloy-request.png)


### 在`Alloy Response Handle`中查看响应

如您所知，在Platform Edge Network上生成Experience Cloud ID (ECID)后，该ID会在Web SDK响应中可见。 我们来查看在Assurance中查看的响应中的ID：

1. 筛选并选择具有名为`Alloy Response Handle`的事件的行。
1. 右侧将显示一个菜单。 选择`+`旁边的`[!UICONTROL ACPExtensionEventData]`符号
1. 选择`[!UICONTROL payload > 0 > payload > 0 > namespace]`进行深入分析。 最后`0`下方显示的ID对应于`ECID`。 您知道根据`namespace`下显示的值与`ECID`匹配

   ![Assurance Alloy响应](assets/assurance-alloy-response.png)

   >[!CAUTION]
   >
   >由于窗口宽度，您可能会看到截断的ECID值。 只需选择界面中的手柄栏并向左拖动即可查看整个ECID。

在将来的课程中，您将使用Assurance验证完全处理的负载，这些负载将到达在数据流中启用的Adobe应用程序。

现在，通过在页面上触发XDM对象，并了解如何验证您的数据收集，您便可以使用Platform Web SDK设置Experience Platform和各个Adobe应用程序。

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848)上分享这些内容
