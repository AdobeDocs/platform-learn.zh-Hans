---
title: Agent Orchestrator快速入门
description: Agent Orchestrator快速入门
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# 1.1.1 Agent Orchestrator快速入门

## 1.1.1.1在Agent Orchestrator中设置上下文

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

您应该会看到此内容。 确保您加入了&#x200B;**Experience Platform International**&#x200B;组织。

![Agent Orchestrator](./images/ao1.png)

单击&#x200B;**上下文**&#x200B;窗口。

![Agent Orchestrator](./images/ao2.png)

将上下文设置为：

- **文档Source**： **Customer Journey Analytics**
- **沙盒**： **加速**
- **数据视图**： **加速2026 B2C**

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

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

然后，您应该会看到此内容，其中深入介绍特定于光纤的趋势。

**操作**：请注意增长曲线和区域峰值。

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3将订单与内容首选项关联

**意图**

测试内容偏好设置（例如SciFi、Sports、Drama）预测宽带升级行为的假设 — 特别是对于高带宽需求。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4标识现有光纤历程

**意图**

了解标题中包含“Fiber”的活动历程或最近结束的历程，例如“Fiber Upgrade NYC - September”、“Fiber Trial - Streaming Bundle”。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/ao13.png)

使用光纤消息传递列出活动或过去的历程。

操作：将高性能历程列入候选名单以进行克隆。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5检查种子

**意图**：

了解“CitiSignal — 光纤最大发布促销活动”历程的种子定义 — 哪些特征会推动定位(例如，“SciFi流派偏好设置”、“4+设备”、“流≥300GB/月”)。

输入以下&#x200B;**Prompt**，然后键入&#x200B;**+CitiSignal文件**&#x200B;以启用自动完成。 选择历程&#x200B;**CitiSignal - Fiber Max启动项促销活动**。

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

您应该会看到此内容。 单击&#x200B;**发送**&#x200B;按钮。

![Agent Orchestrator](./images/ao17.png)

您应该会看到此内容。

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6通过流失分析验证历程性能

**意图**

在Customer Journey Analytics中构建分步funnel

已投放→已打开→已单击→已抵达→产品视图→添加到购物车→结帐→完成订单

包括作为分支的光纤相关SKU视图。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7创建新受众

**意图**

基于上述发现，消费大量数据的客户与更喜欢科幻或幻想类型的客户之间存在相关性。 现在，您将在受众中组合这些属性。

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

>[!NOTE]
>
>请验证该助理的上下文是否指向沙盒&#x200B;**Accelerate**&#x200B;和数据视图&#x200B;**Accelerate 2026 B2C**

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

查看计划。 输入`yes`并单击&#x200B;**发送**。

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
>创建新受众时，需要24小时才能将受众提供给助理进一步使用。

## 1.1.1.8查找与高使用率对应的现有受众，并检查它们是否在使用中

**意图**：

找到任何名为“大量下载者”的受众（由每月数据使用阈值定义）。

>[!NOTE]
>
>在上一个步骤中，您创建了一个新受众，请记住，该受众需要24小时才能供助理进一步使用。 现在，您应该改用另一个已存在的受众。

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

您应该会看到此内容。 确保您加入了&#x200B;**Experience Platform International**&#x200B;组织。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

>[!NOTE]
>
>请验证该助理的上下文是否指向沙盒&#x200B;**Accelerate**&#x200B;和数据视图&#x200B;**Accelerate 2026 B2C**

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

您应该会看到此内容。

![Agent Orchestrator](./images/ao31.png)

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
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

然后，您应该会看到类似以下的内容。 这段旅程目前没有进行。

![Agent Orchestrator](./images/ao53.png)

对于即将推出的Fiber Max，您现在应创建一个新历程。

## 1.1.1.9为Fiber Max启动项创建新历程

**意图**：

构建以复合受众为目标的新历程：

大量下载者∩SciFi偏好设置（kbaa_5207bf受众密钥）。

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

您应该会看到此内容。 确保您加入了&#x200B;**Experience Platform International**&#x200B;组织。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

>[!NOTE]
>
>请验证该助理的上下文是否指向沙盒&#x200B;**Accelerate**&#x200B;和数据视图&#x200B;**Accelerate 2026 B2C**

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

您应该会看到此内容。 输入`yes`并单击“生成”。

![Agent Orchestrator](./images/aocj2.png)

您应该会看到此内容。 输入`yes`并单击“生成”。

![Agent Orchestrator](./images/aocj3.png)

您应该会看到此内容。 输入`The first one`并单击“生成”。

![Agent Orchestrator](./images/aocj4.png)

您应该会看到此内容。 输入`yes`并单击“生成”。

![Agent Orchestrator](./images/aocj5.png)

查看响应。 输入`yes`并单击“生成”。

![Agent Orchestrator](./images/aocj6.png)

单击&#x200B;**审阅**。

![Agent Orchestrator](./images/aocj7.png)

使用您的LDAP更新历程名称以使其唯一。 单击&#x200B;**保存**。

![Agent Orchestrator](./images/aocj8.png)

您的历程现在已在草稿模式下创建。

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10历程冲突管理

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

您应该会看到此内容。 确保您加入了&#x200B;**Experience Platform International**&#x200B;组织。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

>[!NOTE]
>
>请验证助理的上下文是否指向文档源&#x200B;**Journey Optimizer**、沙盒&#x200B;**Accelerate**&#x200B;和数据视图&#x200B;**Accelerate 2026 B2C**

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

查看信息。

![Agent Orchestrator](./images/aocj81.png)

向下滚动并选择&#x200B;**源**&#x200B;以查找信息源自Experience League。

![Agent Orchestrator](./images/aocj82.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

查看历程冲突信息。

![Agent Orchestrator](./images/aocj71.png)

向下滚动以查找更多历程冲突详细信息。

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11个试验

转到[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)。

您应该会看到此内容。 确保您加入了&#x200B;**Experience Platform International**&#x200B;组织。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

>[!NOTE]
>
>请验证该助理的上下文是否指向沙盒&#x200B;**Accelerate**&#x200B;和数据视图&#x200B;**Accelerate 2026 B2C**

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/aoea1.png)

单击建议以比较每个处理的转化率，然后单击&#x200B;**发送**。

![Agent Orchestrator](./images/aoea2.png)

然后，您应该会看到如下详细比较：

![Agent Orchestrator](./images/aoea4.png)

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}