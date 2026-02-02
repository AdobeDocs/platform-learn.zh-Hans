---
title: 带有MCP服务器的Adobe Analytics和Claude.ai
description: 带有MCP服务器的Adobe Analytics和Claude.ai
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 1.5.3 Adobe Analytics和Claude.ai与MCP服务器

[!BADGE Alpha]

+++Alpha详细信息
通过将CJA和Claude.ai与MCP服务器Alpha结合使用，您在此确认Alpha是“按原样”提供的，不提供任何形式的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Alpha。 建议您谨慎使用，切勿依赖此类Alpha和/或随附材料的正确功能或性能。 Alpha被视为Adobe的机密信息。 您向Alpha提供的任何“反馈”(有关Alpha的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐)均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

+++

## 视频

在本视频中，您将获得本练习涉及的所有步骤的解释和演示。

>[!VIDEO](https://video.tv.adobe.com/v/3479562?quality=12&learn=on)

## 1.5.3.1在Claude.ai中为Adobe Analytics创建自定义应用程序

>[!NOTE]
>
>在Claude.ai中使用Adobe Analytics需要满足以下条件：
>- 付费版本的Claude.ai
>- 使用Claude.ai Web客户端

转到[https://claude.ai/](https://claude.ai/){target="_blank"}并使用您的帐户详细信息登录。 登录后，您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标。

![克劳德.ai](./images/claudeaa1.png)

选择&#x200B;**添加连接器**。

![克劳德.ai](./images/claudeaa2.png)

单击&#x200B;**添加自定义标记**。

![克劳德.ai](./images/claudeaa3.png)

填写以下字段：

- **名称**： `CJA`
- **MCP服务器URL**：请与您的Adobe代表核实

单击&#x200B;**添加**。

![克劳德.ai](./images/claudeaa4.png)

您应该会看到此内容。 单击&#x200B;**连接**。

![克劳德.ai](./images/claudeaa5.png)

成功进行身份验证后，您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标开始新聊天。

![克劳德.ai](./images/claudeaa6.png)

转到&#x200B;**+**&#x200B;和&#x200B;**连接器**，您应该会看到现在已启用&#x200B;**Adobe Analytics**&#x200B;连接器。

![克劳德.ai](./images/claudeaa7.png)

您现在可以开始数据分析了。

![克劳德.ai](./images/claudeaa8.png)

## 1.5.3.2在Adobe Analytics中设置上下文

在通过Claude.ai与CJA进一步交互之前，需要设置上下文。

在本练习中，需要将上下文设置为使用：

- **报告包**： **CID — 演示数据**

报表包设置有助于确定在询问问题时Claude.ai应查看哪些数据。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
list report suites
```

![克劳德.ai](./images/claudeaa9.png)

选择&#x200B;**始终允许**。

![克劳德.ai](./images/claudeaa10.png)

选择&#x200B;**始终允许**。

![克劳德.ai](./images/claudeaa11.png)

然后您应该会看到类似这样的内容。

![克劳德.ai](./images/claudeaa12.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
use report suite CID Demo Data
```

![克劳德.ai](./images/claudeaa13.png)

选择&#x200B;**始终允许**。

![克劳德.ai](./images/claudeaa14.png)

您的报表包现已选定。

![克劳德.ai](./images/claudeaa15.png)

## 1.5.2.3浏览报表包

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮以浏览哪些量度和维度可供您使用。

```javascript
list the available metrics and dimensions
```

![Claude.ai和CJA](./images/claudeaa101.png)

选择&#x200B;**始终允许**。

![Claude.ai和CJA](./images/claudeaa102.png)

再次选择&#x200B;**始终允许**。

![Claude.ai和CJA](./images/claudeaa103.png)

然后，您应该会看到此响应，其中包括在此报表包中设置的量度和维度。

![Claude.ai和CJA](./images/claudeaa104.png)

## 1.5.2.4报告

您现在可以开始浏览数据。 首先输入以下提示，然后单击&#x200B;**发送**&#x200B;以提交您的报告请求。

```javascript
show me pageviews for Feb 2?
```

![Claude.ai和CJA](./images/claudeaa105.png)

然后您应该会看到类似这样的内容。

![Claude.ai和CJA](./images/claudeaa106.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
break down pageviews by page name
```

![Claude.ai和CJA](./images/claudeaa107.png)

您应该会看到此内容。

![Claude.ai和CJA](./images/claudeaa108.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
give me an overview of page names, page views by marketing channel
```

![Claude.ai和CJA](./images/claudeaa109.png)

然后您应该会看到类似这样的内容。

![Claude.ai和CJA](./images/claudeaa110.png)

向下滚动一点以查看分析。

![Claude.ai和CJA](./images/claudeaa111.png)

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
Analyze different metrics by marketing channel
```

![Claude.ai和CJA](./images/claudeaa112.png)

然后您应该会看到类似这样的内容。

![Claude.ai和CJA](./images/claudeaa113.png)

您现在已经完成了此练习。

返回[Analytics和代理](./analyticsagents.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}