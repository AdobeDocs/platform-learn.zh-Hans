---
title: —
description: —
kt: 5342
doc-type: tutorial
exl-id: ce845231-17d1-40ab-96f7-bd386753e625
source-git-commit: 5f30a0e941c8260af954ee2b1b289cc8a863b5bb
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 0%

---

# 1.1.6 —

[!BADGE Beta 版]

+++Beta详细信息
通过使用Agent Orchestrator Beta，您在此确认Beta是“按原样”提供的，不提供任何形式的保证。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Beta。 建议您谨慎使用，切勿依赖此类Beta和/或随附材料的正确功能或性能。 Beta被视为Adobe的机密信息。  您向Beta提供的任何“反馈”（有关Beta的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐）均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

+++

## 先决条件

要按照本实验中的以下步骤进行操作，需要以下访问权限：

- 访问Real-Time CDP、Journey Optimizer和Customer Journey Analytics
- 访问Adobe Experience Cloud中的AI助手
- 对AEP Agent Orchestrator的访问权限
- 需要在系统上安装Node.js 18+

## 1.1.6.1设置Agent Orchestrator

### IAM

使用IAM将您自己添加到以下组以获取对LLM凭据的访问权限。

>[!NOTE]
>
>以下某些说明特定于Adobe。 请向您的Adobe代表询问有关要使用的GRP的信息。

```
GRP-XXX
```

### 安装Agent Orchestrator

在计算机上打开新的终端窗口。

![AO](./images/aov2lab1.png)

>[!NOTE]
>
>以下命令需要使用特定的URL。 请向您的Adobe代表询问要使用的URL。

执行以下命令。

```
npm login --registry=https://XXX/ --auth-type=web
```

![AO](./images/aov2lab2.png)

您应该会看到此内容。 按&#x200B;**Enter**。

![AO](./images/aov2lab3.png)

选择&#x200B;**SAML SSO**。

![AO](./images/aov2lab4.png)

单击&#x200B;**是**。

![AO](./images/aov2lab5.png)

您应该会看到此内容。

![AO](./images/aov2lab6.png)

执行以下命令。

```
npm install -g ao --no-fund --registry=https://XXX/
```

![AO](./images/aov2lab7.png)

您应该会看到此内容。 执行以下命令：

```
ao --help
```

![AO](./images/aov2lab8.png)

现已安装Agent Orchestrator。 执行以下命令以启动&#x200B;**Agent Orchestrator**。

```
ao web
```

您应该会看到此内容。 按&#x200B;**Enter**&#x200B;以打开Agent Orchestrator Web UI。

![AO](./images/aov2lab9.png)

## 1.1.6.2配置Agent Orchestrator

单击&#x200B;**使用AO LLM**。

![AO](./images/aov2lab11.png)

单击&#x200B;**登录到生产环境**。

![AO](./images/aov2lab12.png)

单击&#x200B;**图层**&#x200B;图标。

![AO](./images/aov2lab13.png)

选择&#x200B;**AEP AI助手（代码执行 — BashKit）**。

![AO](./images/aov2lab14.png)

单击您的&#x200B;**配置文件**&#x200B;图标，然后选择&#x200B;**设置**。

![AO](./images/aov2lab15.png)

转到&#x200B;**插件**&#x200B;并单击&#x200B;**cja**。

![AO](./images/aov2lab16.png)

单击&#x200B;**安装**。

![AO](./images/aov2lab17.png)

## 1.1.6.3设置您的上下文

单击&#x200B;**新建聊天**。

验证您的实例是否设置为使用实例&#x200B;**Experience Platform International**&#x200B;和沙盒&#x200B;**加速**。

输入以下命令并单击&#x200B;**发送**。

```
list dataviews
```

![AO](./images/aov2lab18.png)

输入以下命令并单击&#x200B;**发送**。

```
switch to dataview Accelerate 2026 B2C
```

![AO](./images/aov2lab20.png)

您应该会看到此内容。

![AO](./images/aov2lab19.png)

## 1.1.6.4从总体购买趋势开始，锚定上下文并放大fibre

**意图**

获得全面的类别需求信息 — 移动设备、固定电话、Internet、电视、光纤 — 专门针对最近60天的数据。 这设定了纽约推出后的季节性、促销效果和区域差异的基线。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me purchases by mainCategory over the last 7 months.
```

![Agent Orchestrator](./images/aotechlab4.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/aotechlab5.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me purchases by mainCategory = Fiber over the last 7 months per week
```

![Agent Orchestrator](./images/aotechlab6.png)

然后，您应该会看到此内容，其中深入介绍特定于光纤的趋势。

![Agent Orchestrator](./images/aotechlab7.png)

## 1.1.6.5将订单与内容首选项关联

**意图**

测试特定类型（例如SciFi、Sports、Drama）的偏好可预测宽带升级行为的假设，特别是对于高带宽需求。

首先，您需要找到用于存储流派首选项的字段。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which field is used to store the preferred genre?
```

![Agent Orchestrator](./images/aotechlab7a.png)

您随后应该会看到此消息，其中显示用于流派的字段为&#x200B;**_experienceplatform.individualCharactations.preferences.preferredGenre**。

![Agent Orchestrator](./images/aotechlab7b.png)

利用这些信息，您可以开始向下钻取购买数据。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me ordersYTD by preferredGenre for the last 7 months
```

![Agent Orchestrator](./images/aotechlab8.png)

您应该会看到此内容。

![Agent Orchestrator](./images/aotechlab9.png)


## 1.1.6.6标识现有光纤历程

**意图**

了解标题中包含“Fiber”的活动历程或最近结束的历程，例如“Fiber Upgrade NYC - September”、“Fiber Trial - Streaming Bundle”。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/aotechlab12.png)

您应该会看到此内容。

![Agent Orchestrator](./images/aotechlab13.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/aotechlab14.png)

您应该会看到此内容。 单击其中一个历程上的链接。

![Agent Orchestrator](./images/aotechlab15.png)

随后将打开一个新窗口，您将立即转到历程详细信息概述。

![Agent Orchestrator](./images/aotechlab15a.png)

## 1.1.6.7检查使用的受众

**意图**：

了解“CitiSignal — 光纤最大发布促销活动”历程的种子定义 — 哪些特征会推动定位（例如，“SciFi流派偏好设置”、“4+设备”、“流≥300GB/月”）。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
What was the initial audience in the journey named CitiSignal - Fiber Max Launch Promotion Winter 2026?
```

![Agent Orchestrator](./images/aotechlab16.png)

您应该会看到此内容。

![Agent Orchestrator](./images/aotechlab18.png)

## 1.1.6.8通过流失分析验证历程性能

**意图**

您希望了解历程性能流失，以了解历程中是否有任何节点或条件正在经历大量用户档案被删除的情况。 这有助于了解历程中是否需要其他调整。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aotechlab19.png)

您应该会看到此内容。

![Agent Orchestrator](./images/aotechlab20.png)

## 1.1.6.9创建新受众

**意图**

根据上述发现和研究，消费大量数据的客户与更喜欢科幻或幻想类型的客户之间存在相关性。 现在，您将在受众中组合这些属性。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create an audience that combines people with an average download usage per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/aotechlab32.png)

查看计划。 单击&#x200B;**接受计划**。

![Agent Orchestrator](./images/aotechlab33.png)

您的受众现已创建。

![Agent Orchestrator](./images/aotechlab38.png)

>[!NOTE]
>
>创建新受众时，需要24小时才能使AI Assistant进一步使用这些受众。

## 1.1.6.10查找与高使用率对应的现有受众，并检查它们是否在使用中

**意图**：

找到任何名为“大量下载者”的受众（由每月数据使用阈值定义）。

>[!NOTE]
>
>在上一步中，您创建了一个新受众，请记住，需要24小时，该受众才可供AI助手进一步使用。 现在，您应该改用另一个已存在的受众。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

您应该会看到此内容。 您现在想要查看您的所有受众以及他们在过去几天中的更改情况。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

您应该会看到此内容。 单击&#x200B;**显示更多**。

![Agent Orchestrator](./images/ao31a.png)

您应该会看到此内容。 单击以关闭右窗格。

![Agent Orchestrator](./images/ao31b.png)

向下滚动一点以查看AI Assistant执行的步骤。

![Agent Orchestrator](./images/ao31c.png)

有一些现有的受众已支持“大量下载者”。 让我们看看它们是否已在使用中。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

然后，您应该会看到类似以下的内容。

![Agent Orchestrator](./images/ao51.png)

您现在应该验证该历程是否处于活动状态。 输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

然后，您应该会看到类似以下的内容。 这些历程当前均未运行。

![Agent Orchestrator](./images/ao53.png)

对于即将推出的Fiber Max，您现在应创建一个新历程。

## 1.1.6.11为Fiber Max启动项创建新历程

**意图**：

构建以复合受众为目标的新历程：

喜欢科幻片∩大量下载者。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

您应该会看到此内容。 输入`yes`并单击“生成”。

![Agent Orchestrator](./images/aocj2.png)

您应该会看到此内容。 输入`yes`并单击“生成”。

![Agent Orchestrator](./images/aocj3.png)

您应该会看到此内容。 输入`The first one`并单击“发送”。

![Agent Orchestrator](./images/aocj4.png)

您应该会看到此内容。 输入`yes`并单击“发送”。

![Agent Orchestrator](./images/aocj5.png)

查看响应。 输入`yes`并单击“发送”。

![Agent Orchestrator](./images/aocj6.png)

单击&#x200B;**审阅**。

![Agent Orchestrator](./images/aocj7.png)

使用您的LDAP更新历程名称以使其唯一。 单击&#x200B;**保存**。

![Agent Orchestrator](./images/aocj8.png)

您的历程现在已在草稿模式下创建。

![Agent Orchestrator](./images/aocj9.png)

## 1.1.6.12历程冲突管理

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

查看信息。

![Agent Orchestrator](./images/aocj81.png)

向下滚动并选择&#x200B;**源**&#x200B;以查找该信息源自Experience League。

![Agent Orchestrator](./images/aocj82.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
List any conflicts for the journey +CitiSignal Fiber Max
```

然后从列表中手动选择历程&#x200B;**CitiSignal - Fiber Max启动项促销活动**。

![Agent Orchestrator](./images/aocj70.png)

您应该会看到此内容。 单击&#x200B;**发送**。

![Agent Orchestrator](./images/aocj70a.png)

查看历程冲突信息。

![Agent Orchestrator](./images/aocj71.png)

向下滚动以查找更多历程冲突详细信息。

![Agent Orchestrator](./images/aocj72.png)

## 1.1.6.13个试验

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/aoea1.png)

向下滚动，然后单击建议之一。 单击&#x200B;**发送**。

>[!NOTE]
>
>建议是动态的，因此在每次生成响应时，您应该会看到不同的建议。 您的建议可能不同于此屏幕快照中显示的建议。

![Agent Orchestrator](./images/aoea2.png)

然后，您应该会看到与所选建议相关的详细答案。

![Agent Orchestrator](./images/aoea4.png)

您现在已经完成了这个实验。

## 后续步骤

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
