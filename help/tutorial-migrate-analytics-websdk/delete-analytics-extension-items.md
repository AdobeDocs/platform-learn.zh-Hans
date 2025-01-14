---
title: 删除Adobe Analytics扩展项目
description: 调试和验证完成后，请删除对Adobe Analytics扩展项的所有引用，并删除扩展本身。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16766
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# 删除Adobe Analytics扩展项目

调试和验证完成后，请删除对Adobe Analytics扩展项的所有引用，并删除扩展本身。

## 概述

如果您对资产中的所有内容已迁移到Web SDK并且（在您的开发环境中）已完成调试和验证感到满意，则可以删除对Adobe Analytics扩展的引用。 删除这些项目的速度以及执行测试时测试的次数取决于您。 如果您希望更加小心翼翼，请慢慢移除参照，并在每次移除之间测试。 如果您确信一切工作正常，迁移正确，可以“撕掉创可贴”并删除所有项目。 当然，我们仍会建议在练习结束时进行测试。

## 从规则中删除旧操作

同样，我们将假定您已测试所有内容，并且一切运行正常。 此时，您可以逐个进入您的规则，并删除属于Adobe Analytics扩展的操作。

1. 打开其中一个规则，例如默认页面加载规则。
1. 完成此规则的迁移后，您可能执行了4个（或更多）操作。

   ![所有4个操作](assets/all-four-actions.jpg)

1. 您可以看到前两个标记上具有“Adobe Analytics”标识符。 我们会删除这些操作。
1. 将鼠标悬停在第一个(如“Adobe Analytics — 设置变量”操作)上，将显示X以允许删除。 单击X看到操作消失。 移除规则中的任意和所有Adobe Analytics操作，在本例中为Set Variable操作和Send Beacon操作。
1. 这将仅保留Web SDK操作

   ![仅限Web SDK操作](assets/websdk-actions-only.jpg)

1. 保存到库
1. 构建库并测试您的网站，确保没有新错误，并且一切正常
1. 对您的其他规则重复此操作，向开发库构建，并在每次删除之间测试（或者根据您的意愿尽可能频繁地测试）。 您只需在Debugger中测试，也可查看迁移报表包中的报表，这同样取决于您的舒适级别。

## 删除扩展

现在，您已删除对Adobe Analytics扩展的引用，接下来可以删除（或禁用）该扩展以及使用该扩展或依赖该扩展的任何其他扩展。 我个人喜欢谨慎的方法，因此“禁用”是我的选择，而不是卸载，至少在一开始是这样。

1. 从UI的左边栏中选择&#x200B;**扩展**。
1. 确保选中&#x200B;**已安装**&#x200B;选项卡。
1. 选择Adobe Analytics扩展。
1. 在右边栏中，选择禁用该扩展(或者，单击三个圆点，然后卸载（如果需要）。

   ![禁用Analytics扩展](assets/disable-analytics-extension.jpg)

1. 对Experience CloudID服务扩展执行相同的操作，因为您将不再需要此操作。 Web SDK扩展可处理ID，因此您不需要其他扩展。
1. 对与Adobe Analytics扩展关联的任何其他扩展执行相同操作，但前提是您已进行必要的迁移更改。
1. 生成对开发环境的更改。

