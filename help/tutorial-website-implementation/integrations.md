---
title: 实施Experience Cloud与标记的集成
description: 了解如何验证 Adobe Experience Cloud 实施中的受众、A4T 和客户属性集成。本课程是“在网站中实施Experience Cloud”教程的一部分。
exl-id: 1d02efce-a50a-4f4d-a0cf-eb8275cf0faa
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 83%

---

# Experience Cloud 集成

在本课程中，您将回顾刚刚实施的解决方案之间的关键集成。好消息是，通过完成前面的课程，您已经实施了集成的代码方面！在本课程中，除了阅读相关说明并进行验证以外，您无需执行任何其他操作。


>[!WARNING]
>
> 本教程中使用的Luma网站预计将在2026年2月16日这一周内被替换。 作为本教程的一部分完成的工作可能不适用于新网站。

## 学习目标

在本课程结束后，您将能够：

1. 阐述受众共享、Analytics for Target (A4T) 以及客户属性集成的基本用例
1. 验证这些集成的基本客户端实施方面

## 先决条件

您应当先完成本教程中所有之前的课程，然后再按照本课程中的说明操作。

>[!NOTE]
>
>要充分使用这些集成，需要满足许多用户权限要求并完成相应的帐户配置和置备步骤，而这些内容都不在本教程的涵盖范围内。 如果您尚未在当前的 Experience Cloud 实施中使用这些集成，则应考虑以下事项：
>
>* 查看[核心服务集成](https://experienceleague.adobe.com/zh-hans/docs/core-services/interface/services/getting-started)的完整要求
>* 查看 [Analytics for Target 集成](https://experienceleague.adobe.com/zh-hans/docs/target/using/integrate/a4t/before-implement)的完整要求

## 受众

[受众](https://experienceleague.adobe.com/zh-hans/docs/core-services/interface/services/audiences/overview)是人员核心服务的一部分，允许您在解决方案之间共享受众。例如，您可以在 Audience Manager 中创建受众，然后使用它通过 Target 来提供个性化内容。

实施 A4T（您已经完成）的主要要求包括：

1. 实施 Adobe Experience Platform 身份标识服务
1. 实施 Audience Manager
1. 实施您希望接收或创建受众的其他解决方案，例如 Target 和 Analytics

### 验证受众集成

验证受众集成的最佳方法是：实际构建受众，将其共享到其他解决方案，然后在其他解决方案中充分使用该受众（例如，确认符合 AAM 区段条件的访客有资格参与针对该区段的 Target 活动）。但是，这不在本教程的涵盖范围内。

这些验证步骤将主要针对客户端实施中可见的关键部分：访客 ID。

1. 打开 [Luma 网站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 如&#x200B;*前面的课程*&#x200B;中所述，确保Debugger将标记属性映射到[您的](switch-environments.md)开发环境

   ![Debugger中显示的标记开发环境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 转到 Debugger 的“网络”选项卡

1. 单击&#x200B;**[!UICONTROL 清除所有请求]**&#x200B;只进行清除

1. 重新加载 Luma 页面，从而确保您在 Debugger 中看到 Target 请求和 Analytics 请求

1. 再次重新加载 Luma 页面

1. 此时，您应会在 Debugger 的“网络”选项卡中看到四个请求，其中两个是 Target 请求，另外两个是 Analytics 请求。

1. 查看标记为“Experience Cloud 访客 ID”的行。每个解决方案对应的每个请求中的 ID 应始终相同。

   ![确认 SDID 匹配](images/integrations-matchingECIDs.png)

1. 每个访客的 ID 均是唯一的，您可以通过请求同事重复执行上述步骤来进行确认。

## Analytics for Target (A4T)

通过 [Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hans) 集成，您可以将 Analytics 数据作为报告 Target 中的量度的来源。

实施 A4T（您已经完成）的主要要求包括：

1. 实施 Adobe Experience Platform 身份标识服务
1. 在 Analytics 页面查看信标之前触发 Target 页面加载请求

A4T 的工作方式是将从 Target 向 Analytics 发出的服务器端请求与 Analytics 页面查看信标拼合在一起，我们称之为“点击拼合”。“点击拼合”要求用于交付活动（或，递增基于 Target 的目标量度）的 Target 请求中有一个参数与 Analytics 页面查看信标中的参数相匹配。此参数称为补充数据 ID (SDID)。

### 验证 A4T 实施

验证 A4T 集成的最佳方法是：使用 A4T 实际构建 Target 活动并验证报表数据，但这不在本教程的涵盖范围内。本教程将演示如何确认这两个解决方案调用中的补充数据 ID 相匹配。

**验证 SDID**

1. 打开 [Luma 网站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 如&#x200B;*前面的课程*&#x200B;中所述，确保Debugger将标记属性映射到[您的](switch-environments.md)开发环境

   ![Debugger中显示的标记开发环境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 转到 Debugger 的“网络”选项卡

1. 单击&#x200B;**[!UICONTROL 清除所有请求]**&#x200B;只进行清除

1. 重新加载 Luma 页面，从而确保您在 Debugger 中看到 Target 请求和 Analytics 请求

1. 再次重新加载 Luma 页面

1. 此时，您应会在 Debugger 的“网络”选项卡中看到四个请求，其中两个是 Target 请求，另外两个是 Analytics 请求。

1. 查看标记为“补充数据 ID”的行。Target 与 Analytics 中首次页面加载所产生的 ID 应该相匹配。第二次页面加载所产生的 ID 也应该相匹配，但与首次页面加载所产生的 ID 不相同。

   ![确认 SDID 匹配](images/integrations-matchingSDIDs.png)

如果您在 A4T 活动中的一次页面加载（不包括单页面应用程序）中发起了其他 Target 请求，最好为这些请求提供唯一的名称（而不是 target-global-mbox），以便它们可以继续使用初始 Target 请求和 Analytics 请求所使用的相同 SDID。

## 客户属性

[客户属性](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=zh-Hans)是人员核心服务的一部分，允许您上传客户关系管理 (CRM) 数据库中的数据，并在 Adobe Analytics 和 Adobe Target 中利用这些数据。

实施客户属性（您已经完成）的主要要求包括：

1. 实施 Adobe Experience Platform 身份标识服务
1. 在&#x200B;*之前，通过ID服务*&#x200B;设置客户ID。Target和Analytics会触发其请求（您已使用标记中的规则排序功能完成此操作）

### 验证客户属性实施

在前面的课程中，您已经验证客户 ID 会传递到身份标识服务和 Target。您还可以在 Analytics 点击中验证客户 ID。此时，客户 ID 是少数几个未在 Experience Cloud Debugger 中显示的参数之一，但您将使用浏览器的 JavaScript 控制台来查看客户 ID。

1. 打开 Luma 网站
1. 打开浏览器的开发人员工具
1. 转到“网络”选项卡
1. 在筛选器字段中键入 `b/ss`，这将限制您仅可看到 Adobe Analytics 请求

   ![打开开发人员工具并筛选“网络”选项卡，以仅显示 Analytics 请求](images/aam-openTheJSConsole.png)

1. 单击网站右上角的&#x200B;**[!UICONTROL 登录]**&#x200B;链接

   ![单击右上角的“登录”](images/idservice-loginNav.png)

1. 输入 `test@test.com` 作为用户名
1. 输入 `test` 作为密码
1. 单击&#x200B;**[!UICONTROL 登录]**&#x200B;按钮

   ![输入凭据并单击登录](images/idservice-login.png)

1. 系统应使您转到主页，这还将触发可在开发人员工具中看到的信标。如果您转到帐户信息页面，请单击 WE.RETAIL 徽标以返回主页。
1. 单击请求并选择“标头”选项卡
1. 向下滚动直到看到一些嵌套参数为止
   1. cid - 这是请求的客户 ID 部分的标准分隔符
   1. crm_id - 这是您在身份标识服务课程中指定的自定义集成代码
   1. id - 来自您的 `Email (Hashed)` 数据元素中的客户 ID 值
   1. as - 身份验证状态，其中“1”表示已登录

   ![Analytics 客户 ID 验证](images/integrations-analyticsCustomerIDValidation.png)

[下一课程“发布您的资产”>](publish.md)
