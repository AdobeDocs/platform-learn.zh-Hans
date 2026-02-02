---
title: 带有MCP服务器的CJA和Claude.ai
description: 带有MCP服务器的CJA和Claude.ai
kt: 5342
doc-type: tutorial
source-git-commit: b8906d1995dcb470789be2a1297eb48cb7690a9c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# 1.5.2 CJA和Claude.ai与MCP服务器

[!BADGE Alpha]

+++Alpha详细信息
通过将CJA和Claude.ai与MCP服务器Alpha结合使用，您在此确认Alpha是“按原样”提供的，不提供任何形式的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Alpha。 建议您谨慎使用，切勿依赖此类Alpha和/或随附材料的正确功能或性能。 Alpha被视为Adobe的机密信息。 您向Alpha提供的任何“反馈”(有关Alpha的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐)均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

+++


>[!NOTE]
>
>有关设置和使用MCP服务器与Claude.ai连接至CJA的本练习与此练习[1.1 Customer Journey Analytics：在Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)之上使用Analysis Workspace构建仪表板。 以下练习中使用的CJA数据视图和连接是在该练习中设置的数据视图和连接。 如果要复制以下结果，应首先按照这些说明操作。

## 视频

在本视频中，您将获得本练习涉及的所有步骤的解释和演示。

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1在Claude.ai中为CJA创建自定义应用程序

>[!NOTE]
>
>在Claude.ai中使用CJA需要满足以下条件：
>- 付费版本的Claude.ai
>- 使用Claude.ai Web客户端

转到[https://claude.ai/](https://claude.ai/){target="_blank"}并使用您的帐户详细信息登录。 登录后，您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标。

![克劳德.ai](./images/claude1.png)

选择&#x200B;**添加连接器**。

![克劳德.ai](./images/claude2.png)

单击&#x200B;**添加自定义标记**。

![克劳德.ai](./images/claude3.png)

填写以下字段：

- **名称**： `CJA`
- **MCP服务器URL**：请与您的Adobe代表核实

单击&#x200B;**添加**。

![克劳德.ai](./images/claude4.png)

您应该会看到此内容。 单击&#x200B;**添加**。

![克劳德.ai](./images/claude5.png)

成功进行身份验证后，您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标开始新聊天。

![克劳德.ai](./images/claude6.png)

转到&#x200B;**+**&#x200B;和&#x200B;**连接器**，您应该会看到现在已启用&#x200B;**CJA**&#x200B;连接器。

![克劳德.ai](./images/claude8.png)

您现在可以开始数据分析了。

![克劳德.ai](./images/claude7.png)


## 1.5.1.2在CJA中设置上下文

在通过Claude.ai与CJA进一步交互之前，需要设置上下文。

在本练习中，需要将上下文设置为使用：

- **数据视图**： **—aepUserLdap— 全渠道数据视图**

数据视图设置可帮助确定在询问问题时Claude.ai应查看的数据视图。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
list dataviews
```

![Claude.ai和CJA](./images/claude9.png)

选择&#x200B;**始终允许**。

![Claude.ai和CJA](./images/claude10.png)

然后，您应该会看到可用数据视图的类似列表。

![Claude.ai和CJA](./images/claude11.png)

若要将其更改为需要使用的数据视图，请输入以下&#x200B;**提示**，然后单击&#x200B;**发送**&#x200B;按钮。

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![Claude.ai和CJA](./images/claude11a.png)

选择&#x200B;**始终允许**。

![Claude.ai和CJA](./images/claude12.png)

您应该会看到此内容。

![Claude.ai和CJA](./images/claude16.png)

您的上下文现已正确设置，因此您可以开始在下一步发送特定提示。

## 1.5.1.3浏览数据视图

>[!NOTE]
>
>此处使用的数据视图已设置为练习[创建数据视图](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)的一部分。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮以浏览哪些量度和维度可供您使用。

```javascript
list the available metrics and dimensions
```

![Claude.ai和CJA](./images/claude101.png)

选择&#x200B;**始终允许**&#x200B;两次，一次用于检索&#x200B;**个量度**，另一次用于检索&#x200B;**个维度**。

![Claude.ai和CJA](./images/claude101a.png)

然后，您应该会看到此响应，其中包含在[创建数据视图](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)练习中设置的量度和维度。

![Claude.ai和CJA](./images/claude102.png)

## 1.5.1.4自由格式表 — 产品查看

您现在可以开始浏览数据。 首先输入以下提示，然后单击&#x200B;**发送**&#x200B;以提交您的报告请求。

```javascript
how many product views happened on January 21, 2026?
```

![Claude.ai和CJA](./images/claude103.png)

选择&#x200B;**始终允许**。

![Claude.ai和CJA](./images/claude104.png)

然后，您应该会看到如下响应。

![Claude.ai和CJA](./images/claude105.png)

您现在可以通过添加维度来细分响应。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
break down product views by product name
```

![Claude.ai和CJA](./images/claude106.png)

然后，您应该会看到如下响应。

![Claude.ai和CJA](./images/claude107.png)

您现在还可以创建可视化图表。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
create a line visualization by hour for product views on January 21
```

![Claude.ai和CJA](./images/claude108.png)

您应该会看到此内容。

![Claude.ai和CJA](./images/claude109.png)

您现在还可以下载此折线图。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
export this chart to PNG
```

![Claude.ai和CJA](./images/claude113.png)

您应该会看到此内容。 单击&#x200B;**下载**。

![Claude.ai和CJA](./images/claude114.png)

然后，您可以打开下载的PNG并在其他文档中使用它。

![Claude.ai和CJA](./images/claude114a.png)

输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
can you breakdown product views by user agent?
```

![Claude.ai和CJA](./images/claude115.png)

您应该会看到此内容。

![Claude.ai和CJA](./images/claude117.png)

## 1.5.1.5流失可视化图表

输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![Claude.ai和CJA](./images/claude118.png)

然后，您应该看到类似这样的内容，其中包括Claude.ai根据Customer Journey Analytics提供的数据生成的可视化图表。

![Claude.ai和CJA](./images/claude119.png)

返回[Analytics和代理](./analyticsagents.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}