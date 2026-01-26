---
title: CJA和ChatGPT与MCP服务器
description: CJA和ChatGPT与MCP服务器
kt: 5342
doc-type: tutorial
source-git-commit: ca2812e14a22b80b7f00066f9cc482e708b4ac6a
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 1.5.1 CJA和ChatGPT带MCP服务器

>[!IMPORTANT]
>
>本实验使用的功能尚未发布。 该功能仍在开发中，因此尚未公开发布。


>[!NOTE]
>
>有关设置和使用MCP服务器与ChatGPT连接至CJA的本练习与此练习[1.1 Customer Journey Analytics：在Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)之上使用Analysis Workspace构建仪表板。 以下练习中使用的CJA数据视图和连接是在该练习中设置的数据视图和连接。 如果要复制以下结果，应首先按照这些说明操作。

## 视频

在本视频中，您将获得本练习涉及的所有步骤的解释和演示。

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1在ChatGPT中为CJA创建自定义应用

>[!NOTE]
>
>在ChatGPT中使用CJA需要满足以下条件：
>- OpenAI的ChatGPT的付费版本
>- 使用ChatGPT Web客户端

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

- **名称**： `CJA`
- **MCP服务器URL**：请与您的Adobe代表核实
- **身份验证**： `OAuth`

选中&#x200B;**我了解并希望继续**&#x200B;的复选框。

单击&#x200B;**创建**。

![ChatGPT](./images/chatgpt6.png)

成功登录后，您应该会看到您的CJA应用程序现在已成功连接。

![ChatGPT](./images/chatgpt8.png)

## 1.5.1.2在CJA中设置上下文

关闭此窗口。

![ChatGPT和CJA](./images/chatgpt9.png)

您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标，转到&#x200B;**更多**，然后选择&#x200B;**CJA**。

![ChatGPT和CJA](./images/chatgpt10.png)

在通过ChatGPT与CJA进一步交互之前，需要设置上下文。

在本练习中，需要将上下文设置为使用：

- **数据视图**： **—aepUserLdap— 全渠道数据视图**

数据视图设置有助于在提问时识别ChatGPT应查看的数据视图。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
list dataviews
```

![ChatGPT和CJA](./images/chatgpt11.png)

然后，您应该会看到可用数据视图的类似列表。

![ChatGPT和CJA](./images/chatgpt11a.png)

若要将其更改为需要使用的数据视图，请输入以下&#x200B;**提示**，然后单击&#x200B;**发送**&#x200B;按钮。

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT和CJA](./images/chatgpt12.png)

您应该会看到此内容。

![ChatGPT和CJA](./images/chatgpt16.png)

您的上下文现已正确设置，因此您可以开始在下一步发送特定提示。

## 1.5.1.3浏览数据视图

>[!NOTE]
>
>此处使用的数据视图已设置为练习[创建数据视图](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)的一部分。

输入以下&#x200B;**提示**&#x200B;并单击&#x200B;**发送**&#x200B;按钮以浏览哪些量度和维度可供您使用。

```javascript
list the available metrics and dimensions
```

![ChatGPT和CJA](./images/chatgpt101.png)

然后，您应该会看到此响应，其中包含在[创建数据视图](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)练习中设置的量度和维度。

![ChatGPT和CJA](./images/chatgpt102.png)

## 1.5.1.4自由格式表 — 产品查看

您现在可以开始浏览数据。 首先输入以下提示，然后单击&#x200B;**发送**&#x200B;以提交您的报告请求。

```javascript
how many product views happened on January 21?
```

![ChatGPT和CJA](./images/chatgpt103.png)

选择&#x200B;**运行报告**。

![ChatGPT和CJA](./images/chatgpt104.png)

然后，您应该会看到如下响应。

![ChatGPT和CJA](./images/chatgpt105.png)

您现在可以通过添加维度来细分响应。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
break down product views by product name
```

![ChatGPT和CJA](./images/chatgpt106.png)

然后，您应该会看到如下响应。

![ChatGPT和CJA](./images/chatgpt107.png)

您现在还可以创建可视化图表。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT和CJA](./images/chatgpt108.png)

选择&#x200B;**UpsertProject**。

![ChatGPT和CJA](./images/chatgpt109.png)

选择&#x200B;**运行报告**。

![ChatGPT和CJA](./images/chatgpt110.png)

您应该会看到此内容。

![ChatGPT和CJA](./images/chatgpt111.png)

向下滚动。

![ChatGPT和CJA](./images/chatgpt112.png)

您现在还可以下载此折线图。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
export this chart to PNG
```

![ChatGPT和CJA](./images/chatgpt113.png)

您应该会看到此内容。 单击&#x200B;**下载PNG**。

![ChatGPT和CJA](./images/chatgpt114.png)

输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
can you breakdown product views by user agent?
```

![ChatGPT和CJA](./images/chatgpt115.png)

选择&#x200B;**运行报告**。

![ChatGPT和CJA](./images/chatgpt116.png)

您应该会看到此内容。

![ChatGPT和CJA](./images/chatgpt117.png)

## 1.5.1.5流失可视化图表

输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT和CJA](./images/chatgpt118.png)

选择&#x200B;**UpsertProject**。

![ChatGPT和CJA](./images/chatgpt119.png)

选择&#x200B;**运行报告**。

![ChatGPT和CJA](./images/chatgpt120.png)

然后您应该会看到类似这样的内容。 输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT和CJA](./images/chatgpt120a.png)

单击&#x200B;**下载PNG**。

![ChatGPT和CJA](./images/chatgpt121.png)

您现在可以看到流失分析的可视化图表。

![ChatGPT和CJA](./images/chatgpt122.png)

输入以下&#x200B;**提示符**&#x200B;并单击&#x200B;**发送**&#x200B;按钮。

```javascript
break down the fallout analysis at the touchpoint of the add to carts
```

![ChatGPT和CJA](./images/chatgpt123.png)

选择&#x200B;**运行报告**。

![ChatGPT和CJA](./images/chatgpt124.png)

返回[Analytics和代理](./analyticsagents.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}