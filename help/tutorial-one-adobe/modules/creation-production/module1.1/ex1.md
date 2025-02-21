---
title: Firefly服务快速入门
description: 了解如何使用Postman和Adobe I/O查询Adobe Firefly服务API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# 1.1.1 Firefly服务快速入门

了解如何使用Postman和Adobe I/O查询Adobe Firefly服务API。

## 1.1.1.1先决条件

在继续此练习之前，您需要完成[您的Adobe I/O项目](./../../../modules/getting-started/gettingstarted/ex6.md)的设置，还需要配置应用程序以与API交互，例如[Postman](./../../../modules/getting-started/gettingstarted/ex7.md)或[PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)。

## 1.1.1.1 firefly.adobe.com

转到[https://firefly.adobe.com](https://firefly.adobe.com)。 单击&#x200B;**个人资料**&#x200B;图标并确保您已登录到正确的&#x200B;**帐户**，即`--aepImsOrgName--`。 如果需要，请单击&#x200B;**切换配置文件**&#x200B;以切换到该帐户。

![Postman](./images/ffui1.png){zoomable="yes"}

输入提示`Horses in a field`并单击&#x200B;**生成**。

![Postman](./images/ffui2.png){zoomable="yes"}

然后，您应该会看到类似以下的内容。

![Postman](./images/ffui3.png){zoomable="yes"}

接下来，在浏览器中打开&#x200B;**开发人员工具**。

![Postman](./images/ffui4.png){zoomable="yes"}

您应该会看到此内容。 转到&#x200B;**网络**&#x200B;选项卡。

![Postman](./images/ffui5.png){zoomable="yes"}

输入搜索词&#x200B;**生成**，然后再次单击&#x200B;**生成**。 然后，您应该会看到名称为&#x200B;**generate-async**&#x200B;的请求。 选择它，然后转到&#x200B;**有效负荷**，您将在其中查看请求的详细信息。

![Postman](./images/ffui6.png){zoomable="yes"}

您在此处看到的请求是发送到Firefly服务的服务器端后端的请求。 它包含几个重要参数：

- **prompt**：这是您的提示，请求Firefly应生成哪种图像

- **种子**：在此请求中，种子是以随机方式生成的。 每当Firefly生成图像时，它都会默认通过选取称为种子的随机数来开始此过程。 此随机数决定了每个图像的唯一性，当您要生成各种图像时，这是非常好的。 但是，有时您可能希望跨多个请求生成彼此相似的图像。 例如，当Firefly生成您要使用Firefly的其他选项（例如样式预设、引用图像等）修改的图像时，请在将来的HTTP请求中使用该图像的种子来限制未来图像的随机性，并关注所需的图像。

![Postman](./images/ffui7.png){zoomable="yes"}

请再次查看UI。 将&#x200B;**长宽比**&#x200B;更改为&#x200B;**横向(4:3)**。

![Postman](./images/ffui8.png){zoomable="yes"}

向下滚动到&#x200B;**效果**，转到&#x200B;**主题**&#x200B;并选择一种效果，如&#x200B;**漫画书**。

![Postman](./images/ffui9.png){zoomable="yes"}

再次在浏览器中打开&#x200B;**开发人员工具**。 然后，单击&#x200B;**生成**&#x200B;并检查正在发送的网络请求。

![Postman](./images/ffui10.png){zoomable="yes"}

现在，当您检查网络请求的详细信息时，将会看到以下内容：

- 与上一个请求相比，**prompt**&#x200B;未发生更改
- 与上一个请求相比，**种子**&#x200B;未发生更改
- 根据&#x200B;**长宽比**&#x200B;中的更改，**大小**&#x200B;已更改。
- 已添加&#x200B;**styles**，并且引用了您选择的&#x200B;**comic_book**&#x200B;效果

![Postman](./images/ffui11.png){zoomable="yes"}

在下一个练习中，您需要使用&#x200B;**seed**&#x200B;编号之一。 写下选择的种子号。

在下一个练习中，您将使用Firefly服务执行类似操作，但随后会使用API而不是UI来执行此操作。 在此示例中，种子号为&#x200B;**45781**。

## 1.1.1.3 Adobe I/O - access_token

在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，选择名为&#x200B;**POST — 获取访问令牌**&#x200B;的请求，然后选择&#x200B;**发送**。 响应应包含新的&#x200B;**accestoken**。

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.4 Firefly Services API，文本2图像

现在您拥有了有效且新鲜的access_token，您可以向Firefly服务API发送您的第一个请求了。

从&#x200B;**FF - Firefly服务技术内部人士**&#x200B;集合中选择名为&#x200B;**POST - Firefly - T2I V3**&#x200B;的请求。

![Firefly](./images/ff1.png){zoomable="yes"}

从响应中复制图像URL，然后在Web浏览器中打开该URL以查看图像。

![Firefly](./images/ff2.png){zoomable="yes"}

您应该会看到一个美妙的图像，其中描绘了`horses in a field`。

![Firefly](./images/ff3.png){zoomable="yes"}

在请求&#x200B;**POST - Firefly - T2I V3**&#x200B;的&#x200B;**Body**&#x200B;中，在字段`"promptBiasingLocaleCode": "en-US"`下添加以下内容，并使用Firefly Services UI随机使用的种子编号之一替换变量`XXX`。 在此示例中，**seed**&#x200B;编号为`45781`。

```json
,
  "seeds": [
    XXX
  ]
```

单击&#x200B;**发送**。 然后，您将收到包含Firefly服务生成的新图像的响应。 打开图像以进行查看。

![Firefly](./images/ff4.png){zoomable="yes"}

然后，您应该会看到基于已使用的&#x200B;**种子**&#x200B;而略有差异的新图像。

![Firefly](./images/ff5.png){zoomable="yes"}

接下来，在请求&#x200B;**POST - Firefly - T2I V3**&#x200B;的&#x200B;**Body**&#x200B;中，将以下&#x200B;**样式**&#x200B;对象粘贴到&#x200B;**seed**&#x200B;对象下。 这会将生成的图像的样式更改为&#x200B;**comic_book**。

```json
,
  "contentClass": "art",
  "styles": {
    "presets": [
      "comic_book"
    ],
    "strength": 50
  }
```

## 后续步骤

转到[使用Microsoft Azure和预签名URL优化您的Firefly进程](./ex2.md){target="_blank"}

返回[Adobe Firefly服务概述](./firefly-services.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
