---
title: Agent Orchestrator快速入门
description: Agent Orchestrator快速入门
kt: 5342
doc-type: tutorial
source-git-commit: 121cbb5ea8f8b713c6ebae008f7f0d9b3a79e476
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 0%

---

# 1.1.1 Agent Orchestrator快速入门

## 视频

在本视频中，您将获得本练习涉及的所有步骤的解释和演示。

>[!VIDEO](https://video.tv.adobe.com/v/3477257?quality=12&learn=on)

## 1.1.1.1在Agent Orchestrator中设置上下文

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

您应该会看到此内容。 确保您加入了&#x200B;**Experience Platform International**&#x200B;组织。

![Agent Orchestrator](./images/ao1.png)

单击&#x200B;**上下文**&#x200B;窗口。

![Agent Orchestrator](./images/ao2.png)

将上下文设置为：

- **文档Source**： **Journey Optimizer**

文档Source设置有助于优先处理哪组Experience League文档，以检查与产品知识/Experience League相关的问题。

- **沙盒**： **Prod — 加速(VA7)**

沙盒设置可帮助确定在询问问题时沙盒AI助手应查看哪个沙盒。

- **数据视图**： **加速2026 B2C**

数据视图设置可帮助确定在询问问题时数据视图AI助手应查看的数据视图。

单击&#x200B;**设置上下文**。

![Agent Orchestrator](./images/ao3.png)

## 1.1.1.2从总体购买趋势开始，锚定上下文并放大fibre

**意图**

获得全面的类别需求信息 — 移动设备、固定电话、Internet、电视、光纤 — 专门针对最近60天的数据。 这设定了纽约推出后的季节性、促销效果和区域差异的基线。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/ao5.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/ao6.png)

然后，您应该会看到此内容，其中深入介绍特定于光纤的趋势。

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3将订单与内容首选项关联

**意图**

测试特定类型（例如SciFi、Sports、Drama）的偏好可预测宽带升级行为的假设，特别是对于高带宽需求。

首先，您需要找到用于存储流派首选项的字段。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which field is used to store the preferred genre?
```

![Agent Orchestrator](./images/ao7a.png)

您随后应该会看到此消息，其中显示用于流派的字段为&#x200B;**_experienceplatform.individualCharactations.preferences.preferredGenre**。

![Agent Orchestrator](./images/ao7b.png)

利用这些信息，您可以开始向下钻取购买数据。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

您应该会看到此内容。 单击&#x200B;**推理完成**&#x200B;块上的图标，了解Agent Orchestrator中发生的幕后事件。

![Agent Orchestrator](./images/ao9.png)

您随后应该会看到类似的解释。

![Agent Orchestrator](./images/ao10.png)

## 1.1.1.4标识现有光纤历程

**意图**

了解标题中包含“Fiber”的活动历程或最近结束的历程，例如“Fiber Upgrade NYC - September”、“Fiber Trial - Streaming Bundle”。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

您应该会看到此内容。 单击&#x200B;**显示更多**。

![Agent Orchestrator](./images/ao13.png)

然后，您应该会看到活动历程或过去历程的较大列表。 单击&#x200B;**下载**&#x200B;图标可下载这些历程的列表。

![Agent Orchestrator](./images/ao13a.png)

这将为您生成一个CSV文件，其中包含AI助手的所有输出。

![Agent Orchestrator](./images/ao13b.png)

单击以关闭右窗格。 输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

您应该会看到此内容。 单击其中一个历程的链接，然后选择&#x200B;**历程详细信息**。

![Agent Orchestrator](./images/ao15.png)

随后将打开一个新窗口，您将立即转到历程详细信息概述。

![Agent Orchestrator](./images/ao15a.png)

## 1.1.1.5检查使用的受众

**意图**：

了解“CitiSignal — 光纤最大发布促销活动”历程的种子定义 — 哪些特征会推动定位(例如，“SciFi流派偏好设置”、“4+设备”、“流≥300GB/月”)。

输入以下&#x200B;**提示**：

```javascript
What was the initial audience in the journey named 
```

然后手动键入`+CitiSignal fib`以启用自动完成。 选择历程&#x200B;**CitiSignal - Fiber Max启动项促销活动**。

![Agent Orchestrator](./images/ao16.png)

您应该会看到此内容。 单击&#x200B;**发送**&#x200B;按钮。

![Agent Orchestrator](./images/ao17.png)

您应该会看到此内容。

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6通过流失分析验证历程性能

**意图**

您希望了解历程性能流失，以了解历程中是否有任何节点或条件正在经历大量用户档案被删除的情况。 这有助于了解历程中是否需要其他调整。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

您应该会看到此内容。

![Agent Orchestrator](./images/ao20.png)

向下滚动一点。 您现在可以通过检查每个节点及其各自的输入编号、流失编号和流失率来查看表。

AI Assistant可为您提供意见和建议。

单击句子&#x200B;**以下是我获得结果的方式**。

![Agent Orchestrator](./images/ao21.png)

然后，您可以查看AI Assistant获得结果的步骤。

![Agent Orchestrator](./images/ao22.png)

## 1.1.1.7创建新受众

**意图**

根据上述发现和研究，消费大量数据的客户与更喜欢科幻或幻想类型的客户之间存在相关性。 现在，您将在受众中组合这些属性。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create an audience that combines people with an average download usage per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

查看计划。 输入`yes`并单击&#x200B;**发送**。

>[!NOTE]
>
>此计划是根据系统中的参考指南生成的。 客户最终能够自定义计划和添加自己的计划，但目前它们是静态的。

![Agent Orchestrator](./images/ao33.png)

查看区段查询表达式。 输入`yes`并单击&#x200B;**发送**&#x200B;按钮。

![Agent Orchestrator](./images/ao34.png)

审阅分部规模估计。 输入`yes`并单击&#x200B;**发送**&#x200B;按钮。

![Agent Orchestrator](./images/ao35.png)

单击&#x200B;**审阅**。

![Agent Orchestrator](./images/ao36.png)

查看区段定义。 单击&#x200B;**创建**。

![Agent Orchestrator](./images/ao37.png)

您的受众现已创建。

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>创建新受众时，需要24小时才能使AI Assistant进一步使用这些受众。

## 1.1.1.8查找与高使用率对应的现有受众，并检查它们是否在使用中

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

## 1.1.1.9为Fiber Max启动项创建新历程

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

## 1.1.1.10历程冲突管理

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

## 1.1.1.11个试验

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

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}