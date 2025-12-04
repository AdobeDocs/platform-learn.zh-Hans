---
title: 使用数据收集标记实施Brand Concierge
description: 使用数据收集标记实施Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# 1.4.3使用数据收集标记实施Brand Concierge

>[!IMPORTANT]
>
>此练习正在进行，尚未结束。

## 数据收集标记属性

Brand Concierge需要将数据发送到Adobe Experience Platform。 为此，需要将Web SDK（或alloy.js）部署到您的网站。

要实现此目的，您现在需要创建数据收集标记属性。

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 打开&#x200B;**数据收集**。

![Brand Concierge](./images/aep101.png)

单击&#x200B;**新建属性**。

![Brand Concierge](./images/aep102.png)

输入名称： `--aepUserLdap-- - CitiSignal Website + Brand Concierge`，同时输入网站的域。

单击&#x200B;**保存**。

![Brand Concierge](./images/aep103.png)

搜索您的资产，然后将其打开。

![Brand Concierge](./images/aep104.png)

转到&#x200B;**扩展**，然后转到&#x200B;**目录**。

![Brand Concierge](./images/aep105.png)

搜索`web sdk`，然后单击扩展&#x200B;**Adobe Experience Platform Web SDK**。 单击&#x200B;**安装**。

![Brand Concierge](./images/aep106.png)

您应该会看到此内容。 您只需在此处提供数据流的详细信息。 要执行此操作，请向下滚动一点。

![Brand Concierge](./images/aep107.png)

对于所有3个环境&#x200B;**生产**、**暂存**&#x200B;和&#x200B;**开发**，请选择以下内容：

- **沙盒**： `--aepUserLdap-- - bc`
- **数据流**： `--aepUserLdap-- - Brand Concierge`

单击&#x200B;**保存**。

![Brand Concierge](./images/aep108.png)

您应该会看到此内容。 转到&#x200B;**规则**。

![Brand Concierge](./images/aep108a.png)

单击&#x200B;**创建新规则**。

![Brand Concierge](./images/aep109.png)

输入名称： `Homepage`。 然后，单击&#x200B;**EVENTS**&#x200B;下的&#x200B;**+添加**。

![Brand Concierge](./images/aep110.png)

选择以下选项：

- **扩展**： **核心**
- **事件类型**：**已加载库（页面顶部）**

单击&#x200B;**保留更改**。

![Brand Concierge](./images/aep111.png)

您应该会看到此内容。 单击&#x200B;**条件**&#x200B;下的&#x200B;**+添加**。

![Brand Concierge](./images/aep112.png)

选择以下选项：

- **逻辑类型**： **常规**
- **扩展**： **核心**
- **条件类型**：**路径不含查询字符串**
- **path equals ...**：输入您的网站域，在本例中为`https://vangeluw.adobedemosystem.com/`

单击&#x200B;**保留更改**。

![Brand Concierge](./images/aep113.png)

您应该会看到此内容。 单击&#x200B;**操作**&#x200B;下的&#x200B;**+添加**。

![Brand Concierge](./images/aep114.png)

选择以下选项：

- **扩展**： **核心**
- **操作类型**： **自定义代码**
- **语言**： **JavaScript**

单击&#x200B;**打开编辑器**。

![Brand Concierge](./images/aep115.png)

粘贴以下代码：

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

单击&#x200B;**保存**。

![Brand Concierge](./images/aep116.png)

您应该会看到此内容。 单击&#x200B;**保留更改**。

![Brand Concierge](./images/aep117.png)

您应该会看到此内容。 单击&#x200B;**保存**。

![Brand Concierge](./images/aep118.png)

转到&#x200B;**发布流**。 单击&#x200B;**添加库**。

![Brand Concierge](./images/aep119.png)

输入名称： `Dev`，为环境选择&#x200B;**开发（开发）**，然后单击&#x200B;**添加所有更改的资源**。

单击&#x200B;**保存并构建用于开发**。

![Brand Concierge](./images/aep120.png)

几分钟后，将构建您的库。 等待您看到&#x200B;**Dev**&#x200B;旁边的&#x200B;**绿色圆点**。 然后，转到&#x200B;**环境**。

![Brand Concierge](./images/aep121.png)

单击&#x200B;**开发**&#x200B;环境的&#x200B;**安装**&#x200B;图标。

![Brand Concierge](./images/aep122.png)

您应该看到此内容。 单击&#x200B;**复制**&#x200B;按钮以复制库的路径。 您需要在网站上实施此功能。

库路径应如下所示：
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}