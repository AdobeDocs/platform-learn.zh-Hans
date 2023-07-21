---
title: Bootcamp -Customer Journey Analytics- Analysis Workspace中的数据准备
description: Bootcamp -Customer Journey Analytics- Analysis Workspace中的数据准备
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: 6a9fc1a4-9a6a-43f2-9393-815f9dc2cb4e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 2%

---

# 4.4 Analysis Workspace中的数据准备

## 目标

- 了解CJA中的Analysis Workspace UI
- 了解Analysis Workspace中的数据准备概念
- 了解如何进行数据计算

## 4.4.1 CJA中的Analysis Workspace UI

Analysis Workspace删除了单个Analytics报表的所有典型限制。 它为构建自定义分析项目提供了强大、灵活的画布。 将任意数量的数据表、可视化图表和组件（维度、量度、区段和时间粒度）拖放到项目中。 即时创建划分和区段，创建用于分析的同类群组，创建警报，比较区段，进行流量和流失分析，以及组织和计划报表以与业务中的任何人员共享。

Customer Journey Analytics将这个解决方案引入到Platform数据之上。 我们强烈建议观看这段时长为四分钟的概述视频：

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

如果您以前未使用Analysis Workspace，我们强烈建议您观看此视频：

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 创建项目

现在该创建您的第一个CJA项目了。 转到CJA中的“项目”选项卡。
单击**新建**。

![演示](./images/prmenu.png)

你就能看到这个了。 选择 **空白项目** 然后单击 **创建**.

![演示](./images/prmenu1.png)

然后，您将看到一个空项目。

![演示](./images/premptyprojects.png)

首先，确保选择屏幕右上角的正确数据视图。 在此示例中，要选择的数据视图是 `CJA Bootcamp - Omnichannel Data View`.

接下来，您将保存项目并为其命名。 可以使用以下命令进行保存：

| 操作系统 | 快捷键 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

您将看到此弹出窗口：

![演示](./images/prsave.png)

请使用此命名约定：

| 名称 | 描述 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

接下来，单击 **保存**.

![演示](./images/prsave2.png)

## 4.4.2计算指标

虽然我们已在数据视图中组织了所有组件，但您仍需要调整其中一些组件，以便业务用户可以开始他们的分析。 此外，在任何分析期间，您可以创建计算量度以更深入地了解洞察发现。

例如，我们将创建一个计算实例 **转化率** 使用 **购买** 在数据视图中定义的量度/事件。

### 转化率

让我们开始打开计算指标生成器。 单击 **+** 以在Analysis Workspace中创建第一个计算指标。

![演示](./images/pradd.png)

此 **计算指标生成器** 将显示为：

![演示](./images/prbuilder.png)

查找 **购买** 左侧菜单的量度列表中。 下 **量度** 点击 **全部显示**

![演示](./images/calcbuildercr1.png)

现在，拖放 **购买** 量度定义中的量度。

![演示](./images/calcbuildercr2.png)

通常，转化率意味着 **转化/会话**. 因此，让我们在计算量度定义画布中执行相同的计算。 查找 **会话** 量度并将其拖放到定义生成器中的 **购买** 事件。

![演示](./images/calcbuildercr3.png)

请注意，将自动选择除法运算符。

![演示](./images/calcbuildercr4.png)

转化率通常以百分比表示。 因此，让我们将格式更改为百分比，并且选择2位小数。

![演示](./images/calcbuildercr5.png)

最后，更改计算指标的名称和描述：

| 标题 | 描述 |
| ----------------- |-------------| 
| yourLastName — 转化率 | yourLastName — 转化率 |

您的屏幕上将显示类似以下的内容：

![演示](./images/calcbuildercr6.png)

别忘了 **保存** 计算指标。

![演示](./images/pr9.png)

## 4.4.3计算Dimension：过滤器（分段）和日期范围

### 筛选器：计算Dimension

计算并不只适用于量度。 在开始任何分析之前，创建一些 **计算Dimension**. 这基本上意味着 **区段** 回到Adobe Analytics。 在Customer Journey Analytics中，这些区段称为 **筛选器**.

![演示](./images/prfilters.png)

创建筛选器将有助于商业用户开始分析一些有价值的计算维度。 这将使某些任务实现自动化并帮助进行采用。 下面给出了一些示例：

1. 自有媒体、付费媒体、
2. 新访问与回访
3. 具有已放弃购物车的客户

这些过滤器可以在分析部件之前或分析部件期间创建（您将在下一个练习中进行此操作）。

### 日期范围：计算的时间Dimension

时间Dimension是另一种计算维度。 虽然已创建了一些时间量度，但您还能够在数据准备阶段创建自己的自定义时间Dimension。

这些计算时间Dimension可帮助分析人员和业务用户记住重要日期，并使用它们来过滤和更改报表时间。 当我们进行分析时，脑海中浮现出一些典型的问题和疑问：

- 去年的“黑色星期五”是什么时候？ 21日到29日？
- 12月我们什么时候搞这个电视广告的？
- 我们何时举办2018夏季销售会？ 我想把它与2019年进行比较。 顺便问一下，你知道2019年的确切日期吗？

![演示](./images/timedimensions.png)

现在，您已使用CJA Analysis Workspace完成数据准备练习。

下一步： [4.5使用Customer Journey Analytics实现可视化](./ex5.md)

[返回用户流程4](./uc4.md)

[返回所有模块](./../../overview.md)
