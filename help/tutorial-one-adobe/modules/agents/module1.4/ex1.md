---
title: Brand Concierge快速入门
description: Brand Concierge快速入门
kt: 5342
doc-type: tutorial
source-git-commit: 75b76978c2ec2f5b89900dea75083932af608bf4
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# 1.4.1 Brand Concierge快速入门

>[!IMPORTANT]
>
>此练习正在进行，尚未结束。

## 视频

在本视频中，您将获得本练习涉及的所有步骤的解释和演示。

## 1.4.1.1 Brand Concierge概述

在配置Brand Concierge时，您将使用的2个主要元素包括：

- **代理编辑器（配置层）**

  用途：用于构建和配置对话式AI体验的主要UI平台。

  主要职责：

   - 定义和管理数据源和知识库
   - 设置品牌表达式（色调、样式、护栏）
   - 设置Meeting Booking代理

- **Agent Orchestrator（执行引擎）**

  用途：解释用户请求并执行相应代理操作的推理和协调引擎。

  主要职责：

   - 解释自然语言用户意图
   - 生成和执行多步推理计划
   - 选择并调用适当的运算符/工具
   - 强制实施品牌上下文、合规性和护栏
   - 协调多代理工作流
   - 汇总和组合来自多个数据源的响应

- **Brand Concierge对话运行时（服务层）**

  用途：面向客户的对话服务层，用于管理聊天会话、上下文和客户交互。

  关键组件：

   - Web代理（客户端）：使用Web SDK集成的浏览器或移动聊天用户界面
   - 会话服务（后端）：管理会话状态并充当编排网关

  主要职责：

   - 管理用户会话和对话记录
   - 处理用户身份验证和配置文件
   - 在客户端和Agent Orchestrator之间路由消息
   - 保留对话上下文
   - 将行为和操作事件记录到AEP for analytics
   - 应用特定于表面的配置

## 1.4.1.2 Brand Concierge实例配置

要开始创建自己的Brand Concierge实例，请执行以下步骤。

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 打开&#x200B;**Brand Concierge**。

![Brand Concierge](./images/bc1.png)

您应该会看到此内容。 单击&#x200B;**沙盒选择**&#x200B;菜单。

![Brand Concierge](./images/bc2.png)

选择已分配给您的沙盒。 该沙盒应命名为`--aepUserLdap-- - bc`。

![Brand Concierge](./images/bc3.png)

单击&#x200B;**开始**。

![Brand Concierge](./images/bc4.png)

对于您的Brand Concierge实例的名称，请使用： `--aepUserLdap-- - CitiSignal Brand Concierge`。

在&#x200B;**下输入以下文本：您希望礼宾人员做什么？**。

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

单击&#x200B;**创建**。

![Brand Concierge](./images/bc5.png)

您应该会看到此内容。 单击&#x200B;**开始**&#x200B;添加知识源。

![Brand Concierge](./images/bc6.png)

选择&#x200B;**网站链接**&#x200B;并单击&#x200B;**继续**。

![Brand Concierge](./images/bc7.png)

您应该会看到此内容。 输入`CitiSignal website`作为知识源的名称。

您现在需要上传一个包含您网站链接的csv文件。 下载[CitiSignal网站链接CSV文件](./assets/citisignal-website-links.csv)到您的桌面。

单击&#x200B;**浏览文件**。

![Brand Concierge](./images/bc8.png)

打开文件&#x200B;**citisignal-website-links.csv**，并更新链接以指向您自己的CitiSignal网站。

![Brand Concierge](./images/bc8a.png)

选择您刚刚下载和编辑的文件&#x200B;**citisignal-website-links.csv**。 单击&#x200B;**打开**。

![Brand Concierge](./images/bc9.png)

您的文件现已添加到此知识源中。 单击&#x200B;**添加**。

![Brand Concierge](./images/bc10.png)

您应该会看到此内容。 单击&#x200B;**带我回家**。

![Brand Concierge](./images/bc11.png)

您应该会看到此内容。 在&#x200B;**消费者产品咨询**&#x200B;卡片上单击&#x200B;**开始使用**。

![Brand Concierge](./images/bc12.png)

您应该会看到此内容。 使用以下文本填写以下字段。

**在提供推荐之前，门房应该了解产品或受众什么？**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**礼宾员在提供推荐时是否有任何业务规则或限制？**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**礼宾员是否应该遵循或避免任何特定的关键字或短语？**

```
Competitor pricing, competitor products
```

您的更新会自动保存。 单击&#x200B;**箭头**&#x200B;返回上一屏幕。

![Brand Concierge](./images/bc13.png)

您应该会看到此内容。 单击&#x200B;**开始**&#x200B;以自定义您的品牌表达式。

![Brand Concierge](./images/bc14.png)

您可以在&#x200B;**Brand Expression**&#x200B;页面上自行选择，请确保为每个问题选择一个选项。

![Brand Concierge](./images/bc15.png)

向下滚动并选择字段&#x200B;**响应长度**&#x200B;的任何设置。

您的更新会自动保存。

![Brand Concierge](./images/bc16.png)

向上滚动，然后单击&#x200B;**箭头**&#x200B;以返回上一个屏幕。

![Brand Concierge](./images/bc17.png)

你以后会回到这里的。 单击&#x200B;**知识源**。

![Brand Concierge](./images/bc18.png)

单击&#x200B;**构建您的知识源**。

![Brand Concierge](./images/bc19.png)

选择&#x200B;**产品目录**&#x200B;并单击&#x200B;**继续**。

![Brand Concierge](./images/bc20.png)

您应该会看到此内容。 输入`CitiSignal Products`作为知识源的名称。

![Brand Concierge](./images/bc21.png)

您现在需要上传一个包含您网站链接的csv文件。 将[CitiSignal产品目录](./assets/CitiSignal-catalog.json.zip)下载到您的桌面并解压缩。

![Brand Concierge](./images/bc26.png)

单击&#x200B;**浏览文件**，然后从设备中选择&#x200B;**浏览**。

![Brand Concierge](./images/bc22.png)

选择文件&#x200B;**CitiSignal-catalog.json**，然后单击&#x200B;**打开**。

![Brand Concierge](./images/bc23.png)

您应该会看到此内容。 单击&#x200B;**添加**。

![Brand Concierge](./images/bc24.png)

你以后会回到这里的。

![Brand Concierge](./images/bc25.png)

## 1.4.1.3个AEP入门培训步骤

Brand Concierge使用Adobe Experience Platform存储对话中的交互数据。 Brand Concierge与Experience Platform之间的连接需要数据流由Brand Concierge配置和使用。

### 数据流

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 打开&#x200B;**Experience Platform**。

![Brand Concierge](./images/aep1.png)

确保您选择了正确的沙盒，应将其命名为`--aepUserLdap-- - bc`。 在左侧菜单中，向下滚动并选择&#x200B;**数据流**。

![Brand Concierge](./images/aep2.png)

单击&#x200B;**新建数据流**。

![Brand Concierge](./images/aep3.png)

输入&#x200B;**数据流名称** `--aepUserLdap-- - Brand Concierge`，然后选择&#x200B;**映射架构** `cja-brand-concierge-sb-XXX`。

单击&#x200B;**保存**。

![Brand Concierge](./images/aep4.png)

您的数据流现已配置完成。 复制数据流名称和数据流ID，并将其写在计算机上的文本文件中。

![Brand Concierge](./images/aep5.png)

### Brand Concierge配置管理API

下一步是启用Brand Concierge配置管理API以配置您刚刚创建的数据流。 在请求处理期间解决IMS组织ID和沙盒详细信息时需要此信息。

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}