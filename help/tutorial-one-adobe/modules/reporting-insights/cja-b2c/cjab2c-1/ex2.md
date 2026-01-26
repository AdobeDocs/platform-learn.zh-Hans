---
title: Customer Journey Analytics — 在Customer Journey Analytics中连接Adobe Experience Platform数据集
description: Customer Journey Analytics — 在Customer Journey Analytics中连接Adobe Experience Platform数据集
kt: 5342
doc-type: tutorial
exl-id: 0f8dbf05-c96f-4cb9-b038-7576a4a91bcb
source-git-commit: 58c89444d36f92d8df7546964eb4b2b5cea8c82c
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# 1.1.2在Customer Journey Analytics中连接Adobe Experience Platform数据集

## 目标

- 了解Data Connection UI
- 将Adobe Experience Platform数据引入CJA
- 了解人员ID和数据拼接
- 了解Customer Journey Analytics中数据流的概念

## 1.1.2.1连接

转到[analytics.adobe.com](https://analytics.adobe.com)以访问Customer Journey Analytics。

在Customer Journey Analytics主页上，转到&#x200B;**连接**。

![演示](./images/cja2.png)

在这里，您可以看到CJA与Platform之间建立的所有不同连接。 这些连接与Adobe Analytics中的报表包具有相同的目标。 然而，数据的收集是完全不同的。 所有数据都来自Adobe Experience Platform数据集。

让我们来创建您的第一个连接。 单击&#x200B;**新建连接**。

![演示](./images/cja4.png)

您随后将看到&#x200B;**创建连接**&#x200B;用户界面。

![演示](./images/cja5.png)

您现在可以为您的连接提供一个名称。

请使用此命名约定： `--aepUserLdap-- – Omnichannel Data Connection`。

您还需要选择要使用的正确沙盒。 在沙盒菜单中，选择您的沙盒，应为`--aepSandboxName--`。 在此示例中，沙盒是&#x200B;**技术内幕**。 您还需要将&#x200B;**平均每日事件数**&#x200B;设置为&#x200B;**小于100万**。

![演示](./images/cjasb.png)

选择沙盒后，您可以开始添加数据集。 单击&#x200B;**添加数据集**。

![演示](./images/cjasb1.png)

## 1.1.2.2选择Adobe Experience Platform数据集

搜索数据集`Demo System - Event Dataset for Website (Global v1.1)`。 启用此数据集的框以将其添加到此连接。

![演示](./images/cja7.png)

停留在同一屏幕中，现在搜索并选中`Demo System - Event Dataset for Call Center (Global v1.1)`的复选框。

你就能拥有这个了。 单击&#x200B;**下一步**。

![演示](./images/cja9.png)

## 1.1.2.3个人ID和数据拼接

### 人员 ID

现在的目标是连接这些数据集。 对于您选择的每个数据集，您将看到一个名为&#x200B;**人员ID**&#x200B;的字段。 每个数据集都有其自己的人员ID字段。

![演示](./images/cja11.png)

如您所见，其中大多数都会自动选择人员ID。 这是因为在Adobe Experience Platform的每个架构中都选择了主身份。 例如，这是`Demo System - Event Schema for Website (Global v1.1)`的架构，您可以看到主标识设置为`ecid`。

![演示](./images/cja13.png)

但是，您仍然可以影响将用于为连接拼合数据集的标识符。 您可以使用在链接到数据集的架构中配置的任何标识符。 单击下拉菜单以浏览每个数据集上的可用ID。

![演示](./images/cja14.png)

如前所述，您可以为每个数据集设置不同的人员ID。 这允许您在CJA中将来自多个源的不同数据集整合在一起。 想象一下，如果能引入NPS或调查数据，那将非常有趣，并且有助于了解背景以及某些事情为什么会发生。

人员ID字段的名称并不重要，只要人员ID字段中的值相对应。 假设我们在一个数据集中有`email`，在另一个定义为“人员ID”的数据集中有`emailAddress`。 如果两个数据集上的人员ID字段的`delaigle@adobe.com`值相同，CJA将能够拼合数据。

请在此处查看CJA常见问题解答，以了解身份拼接的细微差别： [常见问题解答](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hans)。

### 使用人员ID拼合数据

现在您已经了解了使用人员ID拼合数据集的概念，让我们选择`email`作为每个数据集的人员ID。

![演示](./images/cja15.png)

转到每个数据集以更新人员ID。 现在，在下拉列表中选择`email`以填写人员ID字段。

![演示](./images/cja12a.png)

拼合两个数据集后，即可继续。

| 数据集 | 人员 ID |
| ----------------- |-------------| 
| 演示系统 — 网站的事件数据集(Global v1.1) | 电子邮件 |
| 演示系统 — 呼叫中心的事件数据集(Global v1.1) | 电子邮件 |

您还需要确保为这两个数据集启用以下选项：

- 导入所有新数据
- 回填所有现有数据

（请不要忘记为第二个数据集启用这两个选项）

您还需要为每个数据集选择&#x200B;**数据源类型**。

这些是数据集&#x200B;**演示系统 — 网站(Global v1.1)**&#x200B;的事件数据集的设置。

![演示](./images/cja16a.png)

这些是数据集&#x200B;**演示系统 — 网站(Global v1.1)**&#x200B;的事件数据集的设置。

单击&#x200B;**添加数据集**。

![演示](./images/cja16.png)

单击&#x200B;**保存**，然后转到下一个练习。

创建&#x200B;**Connection**&#x200B;后，可能需要几个小时才能在CJA中使用您的数据。

![演示](./images/cja20.png)

## 后续步骤

转到[1.1.3创建数据视图](./ex3.md){target="_blank"}

返回[Customer Journey Analytics](./customer-journey-analytics-build-a-dashboard.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
