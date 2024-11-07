---
title: 在Adobe Experience Platform中配置HTTP API端点
description: 在Adobe Experience Platform中配置HTTP API端点
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 6%

---

# 2.6.3在Adobe Experience Platform中配置HTTP API流端点

在Kafka中设置Adobe Experience Platform接收器连接器之前，您需要在Adobe Experience Platform中创建HTTP API Source连接器。 设置Adobe Experience Platform接收器连接器需要HTTP API流端点URL。

要创建HTTP API Source Connector，请转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../modules/datacollection/module1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 您可以通过单击屏幕顶部蓝线中的文本&#x200B;**[!UICONTROL Production Prod]**&#x200B;来执行此操作。 选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左侧菜单中，转到&#x200B;**源**&#x200B;并在&#x200B;**源目录**&#x200B;中向下滚动，直到看到&#x200B;**HTTP API**。 单击&#x200B;**添加数据**。

![数据获取](./images/kaep1.png)

单击&#x200B;**新建帐户**。 使用`--aepUserLdap-- - Kafka`作为您的HTTP API连接的名称，在本例中为&#x200B;**vangeluw - Kafka**。 启用&#x200B;**XDM Compatible**&#x200B;复选框。 单击&#x200B;**连接到源**。

![数据获取](./images/kaep2.png)

你将看到此内容，请单击&#x200B;**下一步**。

![数据获取](./images/kaep3.png)

选择&#x200B;**现有数据集**，打开下拉菜单。 搜索并选择数据集&#x200B;**演示系统 — 呼叫中心事件数据集(Global v1.1)**。

![数据获取](./images/kaep4.png)

单击&#x200B;**下一步**。

![数据获取](./images/kaep6.png)

单击&#x200B;**下一步**。

![数据获取](./images/kaep7.png)

单击&#x200B;**完成**。

![数据获取](./images/kaep8.png)

然后，您将看到刚刚创建的HTTP API Source Connector概述。

![数据获取](./images/kaep9.png)

您需要复制&#x200B;**流式处理终结点** URL，它类似于下面的那个，因为您将在下一个练习中需要它。

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

您已完成此练习。

下一步： [2.6.4安装和配置Kafka连接和Adobe Experience Platform接收器连接器](./ex4.md)

[返回模块2.6](./aep-apache-kafka.md)

[返回所有模块](../../../overview.md)
