---
title: Agent Orchestrator快速入门
description: Agent Orchestrator快速入门
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Agent Orchestrator快速入门

## 1.3.1在Agent Orchestrator中设置上下文

导航到AI助手并置于大视图。

确认您是在CJA上下文中执行分析任务。

>[!NOTE]
>
>在Analysis (CJA)和Orchestration (JO)之间移动时使用上下文切换。

## 1.3.2从总体购买趋势开始，锚定上下文并放大光纤

**提示**：

```javascript
Show me purchases by mainCategory over the last 2 month
```

**意图**：获取最新的60天的toplevel pulse on category demand（按类别点播） — 手机、固定电话、互联网、电视、光纤。 这会为NY推出后的季节性、促销效果和区域差异设置基线。

思考：

“Fiber是否正在纽约获得市场份额？ 我们是否看到铜线/DSL互联网相互蚕食？ 与电视捆绑包相比，这种转变又是什么呢？”

“这将有助于我确定维也纳可寻址受众的规模，并设定现实的目标。”

营销人员期望的可操作读数：

按mainCategory显示的栈叠式购买条形/折线图（每日/每周粒度）。

按类别与前期划分的采购百分比。

与促销日期相关的显着峰值。

>[!NOTE]
>
>留意滞后归因 — 在一些旧式架构中，光纤订单可能被捕获到“Internet”下。 如果是，则在决策之前协调分类。

 

**提示**：

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**下一个提示**

`Show me purchases by mainCategory = Fiber over the last 2 months`

深入了解特定于光纤的趋势。

**操作**&#x200B;记下增长曲线和区域峰值。

## 1.3.3将订单与内容首选项关联

**提示**：

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**意图**&#x200B;检验以下假设：内容偏好设置（如SciFi、Sports、Drama）可预测宽带升级行为 — 特别是针对高带宽需求。

**正在思考**

“SciFi粉丝经常观看4K的视频，从多台设备观看视频流，他们可能看重低延迟。”

“让我们量化一下科幻片（或许还有体育）与近期订单是否相关。”

**预期输出**

订单中心（应用了YTD过滤器）按首选流派划分，限制为过去2个月。

按订单转化率和AOV（平均订单值）对流派进行排名。

决策：如果科幻显示强烈信号，这将成为维也纳Fiber Max发布的主要创意支柱（例如，“永远不再缓冲”消息、高级捆绑包）。

**提示**

`Show me ordersYTD by preferred genre for the last 2 months`

**意图**

按流派（例如，科幻小说、体育）分析转化。

**目标**&#x200B;验证Sci-Fi风扇是否对光纤升级过度索引。

## 1.3.4识别现有光纤历程

**提示**：

```javascript
What journey was running and had Fiber in the name
```

**意图**&#x200B;发现标题中包含“Fiber”的活动历程或最近结束的历程，例如“Fiber Upgrade NYC - September”、“Fiber Trial - Streaming Bundle”。

**正在思考**

“哪些历程表现良好，其触发因素是什么？”

“我能否在维也纳重复成功的编排逻辑？”

**预期输出**

具有状态（活动、暂停、已结束）、日期范围、目标区段、KPI（打开率、CTR、转化）的历程列表。

下一步行动：将一两个成功的克隆/适应光纤历程列入候选名单。

**提示**

`What journey was running and had Fiber in the name?`

使用光纤消息传递列出活动或过去的历程。

操作：将高性能历程列入候选名单以进行克隆。

## 1.3.5查看种子受众是否有关于相关历史促销的信息

**提示**：

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**意图**&#x200B;了解“SciFi促销2024 - jl”历程的种子定义 — 哪些特征驱动了定位(例如，“SciFi流派偏好设置”、“4+设备”、“流≥300GB/月”)。

**正在思考**

“我想将久经考验的SciFi创新与Fibre Max性能信息结合起来。”

“如果受众与大量下载者重叠，我们可以栈叠倾向。”

**预期输出**

受众标准（包含/排除）、受众规模、区域过滤器、回访间隔、频率阈值。

>[!NOTE]
>
>将上下文更改为CJA

营销人员从此将切换到分析模式以确保正确报告。

**提示**：

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

审查受众标准（流媒体习惯、设备计数）。

目标：了解高带宽需求的特征。

## 1.3.6通过流失分析验证历程性能

**提示**：

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>将上下文更改为CJA)

**意图**&#x200B;在Customer Journey Analytics中构建分步funnel

已投放→已打开→已单击→已抵达→产品视图→添加到购物车→结帐→完成订单

包括作为分支的光纤相关SKU视图。

思考：

“我们在哪里失去人 — 电子邮件打开、登陆页面加载、PDP、结账摩擦？”

“SciFi用户在Fibre PDP上的跳出率是否高于或低于平均水平？”

预期产出：

包含每个步骤的流失率的可视化图表。

区段叠加图（SciFi与体育对比其他）。

设备/浏览器故障导致技术冲突。

决策：

如果结账流失率高，请与product/UX协调以修复付款流程。

如果PDP退出率很高，请重写声明清晰度（速度、安装时间、捆绑包价值）。

>[!NOTE]
>
>将上下文更改为JO

现在，营销人员开始使用Adobe Journey Optimizer进行编排和受众操作。

**提示**：

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

构建funnel可视化图表：按顺序打开→单击→投放→签→。

操作：确定流失点并优化消息传送或UX。


## 1.3.7查找符合高使用率的现有受众

**提示**：

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>将上下文更改为Adobe Journey Optimizer

意图：找到任何名为“大量下载者”的JO受众 — 可能由每月数据使用阈值、流式处理小时数或设备并发定义。

思考：

“如果存在像‘重载下载器’这样的受众，它非常适合‘光纤最大值’的定位：速度、可靠性、无限层级。”

预期产出：

受众元数据：定义标准、大小、上次刷新、治理标记、区域可用性。

**提示**：

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

找到具有高数据使用率的受众。

目标：与Sci-Fi偏好设置结合使用，以实现Fiber Max定位。

## 1.3.8确定这些受众是否已使用

**提示**：

```javascript
Which of the above are used in a journey? 
```

意图：检查受众与历程的关联 — 确保我们不会发送双消息或与当前程序发生冲突。

思考：

“如果大量下载者已处于保留历程中，我们需要抑制逻辑或频率上限以避免疲劳。”

预期产出：

映射：受众→历程名称、状态、联系策略、上次发送、性能。

决定：

如果正在使用中，请为维也纳启动项创建排除项或共享禁止显示。

如果未使用，则为新的旅程提供绿光。

提示：

历程中使用了以上哪项？

确保与活跃的营销活动无重叠。

操作：根据需要应用隐藏。

## 1.3.9为Fiber Max Launch创建新历程

**提示**：

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

意图：构建面向复合受众的新JO历程：

大量下载者∩SciFi偏好设置（kbaa_5207bf受众密钥）。

思考：

“这是Fiber Max的最佳选择：高倾向性和创造关联性。”

“我们将打造一种与维也纳供应紧密联系的多点体验。”

历程设计(JO)：

进入标准：

受众：大量下载者 — 科幻偏好设置_kbaa_5207bf

地理位置：维也纳地铁（邮政编码列表或地理多边形）

资格：不在活动的“Fiber Upgrade NYC - Sept”活动中；不是当前的Fiber订阅者。

触发器和计时：

维也纳发布前T14天（2026年1月）：预览电子邮件 — “Fiber Max即将推出”。

启动周：主电子邮件+应用程序内横幅+付费媒体同步（通过CDP目标）。

T+3天：行为拆分 — 如果未单击，则短信轻推；如果已单击但未订购，则使用安装程序可用性CTA重新定位。

T+10天：选件测试 — 免费安装与第1个月折扣(A/B)。

Personalization：

适用于SciFi爱好者的动态复制（延迟/4K流挂钩）。

针对设备组合（游戏机、流媒体盒）定制的速度/延迟声明。

捆绑推荐：Fiber Max +高级TV脚本内容包。

治理：

频率上限：每10天最多3次接触。

如果当前的Fiber订阅者或存在安装票证，则禁止显示。

尊重选择退出偏好设置。

衡量计划(CJA)：

跟踪：投放、打开、单击、PDP查看、结帐开始、订单完成。

KPI：光纤最大转化率、提升与控制、安装时间。

诊断：按设备/流派区段显示流失报表。

形状

所有这些如何融为一体（营销人员的思维模式）

诊断需求(具体是光纤→总体类别)。

证明内容到转换信号（按流派排序）。

我的成功历程（查找Fibernamed历程和SciFi促销受众）。

验证摩擦点(SciFi历程中的CJA流失)。

针对高倾向区段(大量下载者∩SciFi)激活。


返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}