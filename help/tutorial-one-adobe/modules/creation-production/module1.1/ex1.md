---
title: Firefly服务快速入门
description: 了解如何使用Postman和Adobe I/O查询Adobe Firefly服务API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Firefly服务快速入门

了解如何使用Postman和Adobe I/O查询Adobe Firefly服务API。

## 1.1.1.1先决条件

在继续此练习之前，您需要完成[您的Adobe I/O项目](./../../../modules/getting-started/gettingstarted/ex6.md)的设置，还需要配置应用程序以与API交互，例如[Postman](./../../../modules/getting-started/gettingstarted/ex7.md)或[PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)。

## 1.1.1.2 Adobe I/O - access_token

在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，选择名为&#x200B;**POST — 获取访问令牌**&#x200B;的请求，然后选择&#x200B;**发送**。 响应应包含新的&#x200B;**accestoken**。

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 Firefly Services API，文本2图像

现在您拥有了有效且新鲜的access_token，您可以向Firefly服务API发送您的第一个请求了。

从&#x200B;**FF - Firefly服务技术内部人士**&#x200B;集合中选择名为&#x200B;**POST - Firefly - T2I V3**&#x200B;的请求。

![Firefly](./images/ff1.png){zoomable="yes"}

从响应中复制图像URL，然后在Web浏览器中打开该URL以查看图像。

![Firefly](./images/ff2.png){zoomable="yes"}

您应该会看到一个美妙的图像，其中描绘了`horses in a field`。

![Firefly](./images/ff3.png){zoomable="yes"}

在继续下一个练习之前，请随时尝试使用API请求。

## 后续步骤

转到[使用Microsoft Azure和预签名URL优化您的Firefly进程](./ex2.md){target="_blank"}

返回[Adobe Firefly服务概述](./firefly-services.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
