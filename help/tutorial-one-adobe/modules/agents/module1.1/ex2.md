---
title: 适用于ChatGPT Enterprise的Adobe Marketing Agent
description: 适用于ChatGPT Enterprise的Adobe Marketing Agent
kt: 5342
doc-type: tutorial
exl-id: 0aa0cef5-bc1d-4cb6-be09-a5964686c963
source-git-commit: 88f0121cd0bf73f2456c349908a7f8193ebddafa
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# 1.1.2适用于ChatGPT Enterprise的Adobe Marketing Agent

[!BADGE Beta 版]

+++Beta详细信息
通过在ChatGPT Enterprise Beta中使用Adobe Marketing Agent，您特此确认Beta是“按原样”提供的，不提供任何形式的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Beta。 建议您谨慎使用，切勿依赖此类Beta和/或随附材料的正确功能或性能。 Beta被视为Adobe的机密信息。  您向Beta提供的任何“反馈”(有关Beta的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐)均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

+++

## 视频

在本视频中，您将获得本练习涉及的所有步骤的解释和演示。

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1在ChatGPT Enterprise for Adobe Marketing Agent中创建自定义应用

>[!NOTE]
>
>在ChatGPT中使用Adobe Marketing Agent需要满足以下条件：
>- OpenAI的ChatGPT Enterprise的付费版本
>- 使用ChatGPT Enterprise Web客户端

转到[https://chatgpt.com/](https://chatgpt.com/){target="_blank"}并使用您的帐户详细信息登录。 登录后，您应该会看到此内容。 单击您的用户名。

![ChatGPT](./images/chatgpt1.png)

选择&#x200B;**设置**。

![ChatGPT](./images/chatgpt2.png)

转到&#x200B;**应用**，然后选择&#x200B;**高级设置**。

![ChatGPT](./images/chatgpt3.png)

打开&#x200B;**开发人员模式**，然后单击&#x200B;**上一步**。

![ChatGPT](./images/chatgpt4.png)

单击&#x200B;**创建应用程序**。

![ChatGPT](./images/chatgpt5.png)

填写以下字段：

- **名称**： `Adobe Marketing Agent`
- **MCP服务器URL**：请与您的Adobe代表核实
- **身份验证**： `OAuth`

选中&#x200B;**我了解并希望继续**&#x200B;的复选框。

单击&#x200B;**创建**。

![ChatGPT](./images/chatgpt6.png)

ChatGPT现在将尝试连接到您的Adobe帐户。 选择&#x200B;**允许访问**，然后您必须使用您的Adobe帐户登录。

![ChatGPT](./images/chatgpt7.png)

成功登录后，您应该会看到Adobe Marketing Agent现在已成功连接。

![ChatGPT](./images/chatgpt8.png)

## 1.1.2.2在Adobe Marketing Agent中设置上下文

关闭此窗口。

![Agent Orchestrator](./images/chatgpt9.png)

您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标，转到&#x200B;**更多**，然后选择&#x200B;**Adobe Marketing Agent**。

![Agent Orchestrator](./images/chatgpt10.png)

在通过ChatGPT与Adobe Marketing Agent进一步交互之前，需要设置上下文。

在本练习中，需要将上下文设置为使用：

- **沙盒**： **Prod — 加速(VA7)**

沙盒设置有助于在询问问题时识别ChatGPT应查看的沙盒。

- **数据视图**： **加速2026 B2C**

数据视图设置有助于在提问时识别ChatGPT应查看的数据视图。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

然后，您应该会看到一个类似的可用沙盒列表。 此示例中的当前沙盒设置为&#x200B;**prod**。

若要将其更改为需要使用的沙盒，请输入以下&#x200B;**提示**，然后单击&#x200B;**发送**&#x200B;按钮。

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

您应该会看到此内容。 单击&#x200B;**设置上下文**。

![Agent Orchestrator](./images/chatgpt13.png)

您应该会看到此内容。 输入以下&#x200B;**Prompt**&#x200B;并单击&#x200B;**send**&#x200B;按钮以设置要使用的数据视图。

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

然后，您应该会看到可用数据视图的类似列表。

要设置需要使用的数据视图，请输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

您应该会看到此内容。 单击&#x200B;**设置上下文**。

![Agent Orchestrator](./images/chatgpt16.png)

您应该会看到此内容。

![Agent Orchestrator](./images/chatgpt17.png)

您的上下文现已设置正确，因此您接下来可以开始发送特定提示。

## 1.1.2.3从总体购买趋势开始，锚定上下文并放大fibre

**意图**

获得全面的类别需求信息 — 移动设备、固定电话、Internet、电视、光纤 — 专门针对最近60天的数据。 这设定了纽约推出后的季节性、促销效果和区域差异的基线。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

您应该会看到以下内容：

![Agent Orchestrator](./images/chatgpt19.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

然后，您应该会看到此内容，其中深入介绍特定于光纤的趋势。

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4将订单与内容首选项关联

**意图**

测试特定类型（例如SciFi、Sports、Drama）的偏好可预测宽带升级行为的假设，特别是对于高带宽需求。

首先，您需要找到用于存储流派首选项的字段。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

您随后应该会看到此消息，其中显示用于流派的字段为&#x200B;**_experienceplatform.individualCharactations.preferences.preferredGenre**。

![Agent Orchestrator](./images/chatgpt23.png)

利用这些信息，您可以开始向下钻取购买数据。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

您应该会看到此内容。 单击&#x200B;**研究**。

![Agent Orchestrator](./images/chatgpt25.png)

您应该会看到此内容。

![Agent Orchestrator](./images/chatgpt26.png)

向下滚动查看更多信息。

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5标识现有光纤历程

**意图**

了解标题中包含“Fiber”的活动历程或最近结束的历程，例如“Fiber Upgrade NYC - September”、“Fiber Trial - Streaming Bundle”。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

您应该会看到此内容。 单击&#x200B;**研究**。

![Agent Orchestrator](./images/chatgpt29.png)

然后，您应该会看到历程列表。

![Agent Orchestrator](./images/chatgpt30.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

您应该会看到此内容。 单击&#x200B;**研究**。

![Agent Orchestrator](./images/chatgpt32.png)

您应该会看到此内容。

![Agent Orchestrator](./images/chatgpt33.png)

向下滚动查看更多详细信息。

![Agent Orchestrator](./images/chatgpt34.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

您应该会看到此内容。

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6通过流失分析验证历程性能

**意图**

您希望了解历程性能流失，以了解历程中是否有任何节点或条件正在经历大量用户档案被删除的情况。 这有助于了解历程中是否需要其他调整。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

您应该会看到此内容。

![Agent Orchestrator](./images/chatgpt38.png)

向下滚动一点。 您现在可以通过检查每个节点及其各自的输入编号、流失编号和流失率来查看表。

![Agent Orchestrator](./images/chatgpt39.png)

再向下滚动一点，以查看观察结果和建议。

![Agent Orchestrator](./images/chatgpt40.png)

您现在已经完成了这个实验。

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
