---
title: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics中的Adobe Experience Platform数据集
description: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics中的Adobe Experience Platform数据集
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 47e02021-019c-4ea4-a7a8-003deef7c9e5
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 4.2连接Customer Journey Analytics中的Adobe Experience Platform数据集

## 目标

- 了解数据连接UI
- 将Adobe Experience Platform数据引入CJA
- 了解人员ID和数据拼接
- 了解Customer Journey Analytics中数据流的概念

## 4.2.1连接

转到 [analytics.adobe.com](https://analytics.adobe.com) 以访问Customer Journey Analytics。

在Customer Journey Analytics主页上，转到 **连接**.

![演示](./images/cja2.png)

在这里，您可以看到CJA与Platform之间建立的所有不同连接。 这些连接具有与Adobe Analytics中的报表包相同的目标。 但是，数据的收集是完全不同的。 所有数据都来自Adobe Experience Platform数据集。

让我们来创建您的第一个连接。 单击&#x200B;**“创建新连接”**。

![演示](./images/cja4.png)

然后您将会看到 **创建连接** UI。

![演示](./images/cja5.png)

您现在可以为您的连接命名。

请使用此命名约定： `yourLastName – Omnichannel Data Connection`.

示例：`vangeluw - Omnichannel Data Connection`

您还需要选择要使用的正确沙盒。 在沙盒菜单中，选择您的沙盒，它应为 `Bootcamp`. 在此示例中，要使用的沙盒是 **Bootcamp**. 您还需要设置 **平均每日事件数** 到 **少于100万**.

![演示](./images/cjasb.png)

选择沙盒后，您可以开始向此连接添加数据集。 单击 **添加数据集**.

![演示](./images/cjasb1.png)

## 4.2.2选择Adobe Experience Platform数据集

搜索数据集 `Demo System - Event Dataset for Website (Global v1.1)`. 单击 **+** 以将数据集添加到此连接。

![演示](./images/cja7.png)

现在搜索并选中以下复选框： `Demo System - Profile Dataset for Loyalty (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

你就能拥有这个了。 单击&#x200B;**下一步**。

![演示](./images/cja9.png)

## 4.2.3人员ID和数据拼接

### 人员 ID

现在的目标是连接这些数据集。 对于您选择的每个数据集，您将看到一个名为的字段 **人员ID**. 每个数据集都有其自己的人员ID字段。

![演示](./images/cja11.png)

如您所见，其中大多数自动选择了人员ID。 这是因为在Adobe Experience Platform的每个架构中都选择了主标识符。 例如，以下是 `Demo System - Event Schema for Call Center (Global v1.1)`，您可以看到主要标识符设置为 `phoneNumber`.

![演示](./images/cja13.png)

但是，您仍然可以影响将用于为连接拼合数据集的数据集的标识符。 您可以使用在链接到数据集的架构中配置的任何标识符。 单击下拉菜单以浏览每个数据集上的可用ID。

![演示](./images/cja14.png)

如前所述，您可以为每个数据集设置不同的人员ID。 这允许您在CJA中将来自多个源的不同数据集聚集在一起。 想象一下，如果能引进国家统计系统或调查数据，将会非常有趣，并且有助于了解背景以及某些事情为什么会发生。

只要人员ID字段中的值对应，“人员ID”字段的名称并不重要。 例如，如果人员ID为 `email` 在一个数据集和 `emailAddress` 在另一个，和 `dnb-bootcamp@adobe.com` 人员ID字段在两个数据集中的值相同，CJA将能够拼合数据。

目前，还存在其他一些限制，例如将匿名行为与已知行为拼合在一起。 请在此处查看常见问题解答： [常见问题解答](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hans).

### 使用人员ID拼合数据

现在您了解了使用人员ID拼合数据集的概念后，让我们选择 `email` 作为每个数据集的人员ID。

![演示](./images/cja15.png)

转到每个数据集以更新人员ID。

![演示](./images/cja12a.png)

现在填写字段人员ID，选择 `email` 下拉列表中的。

![演示](./images/cja17.png)

拼合三个数据集后，我们就可以继续了。

| 数据集 | 人员 ID |
| ----------------- |-------------| 
| 演示系统 — 网站的事件数据集(Global v1.1) | 电子邮件 |
| 演示系统 — 忠诚度用户档案数据集(Global v1.1) | 电子邮件 |
| 演示系统 — 呼叫中心的事件数据集（全局v1.1） | 电子邮件 |

您还需要确保为每个数据集启用以下选项：

- 导入所有新数据
- 回填所有现有数据

单击 **添加数据集**.

![演示](./images/cja16.png)

单击 **保存** 然后继续下一个练习。
创建您的 **连接** 可能需要几个小时，您的数据才会在CJA中可用。

![演示](./images/cja20.png)

下一步： [4.3创建数据视图](./ex3.md)

[返回用户流程4](./uc4.md)

[返回所有模块](./../../overview.md)
