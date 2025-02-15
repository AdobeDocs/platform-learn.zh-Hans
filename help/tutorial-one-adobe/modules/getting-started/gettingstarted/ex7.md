---
title: 快速入门 — Postman设置
description: 快速入门 — Postman设置
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# 选项1：使用Postman

>[!IMPORTANT]
>
>如果您是Adobe员工，请按照说明[安装PostBuster](./ex8.md)！

## Postman环境下载

转到[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}并打开您的项目。

![Adobe I/O新集成](./images/iopr.png){zoomable="yes"}

单击&#x200B;**Firefly - Firefly服务** API。 然后，单击&#x200B;**下载Postman**&#x200B;并选择&#x200B;**OAuth服务器到服务器**&#x200B;以下载Postman环境。

![Adobe I/O新集成](./images/iopm.png){zoomable="yes"}

## Postman对Adobe I/O的身份验证

在[Postman下载](https://www.postman.com/downloads/){target="_blank"}上下载并安装适用于您的操作系统的相关Postman版本。

![Adobe I/O新集成](./images/getstarted.png){zoomable="yes"}

启动应用程序。

在Postman中，有2个概念：环境和收藏集。

环境文件包含所有比较一致或不太一致的环境变量。 在该环境中，您可以找到Adobe环境的IMSOrg等内容，以及客户端ID和其他安全凭据。 您之前在Adobe I/O设置过程中下载了名为&#x200B;**`oauth_server_to_server.postman_environment.json`**&#x200B;的环境文件。

收藏集包含大量您可以使用的API请求。 我们将使用2个收藏集

- 1个集合用于对Adobe I/O进行身份验证
- 1本模块中的练习的集合

将[postman-ff.zip](./../../../assets/postman/postman-ff.zip)下载到您的本地桌面。

![Adobe I/O新集成](./images/pmfolder.png){zoomable="yes"}

在&#x200B;**postman-ff.zip**&#x200B;文件中包含以下文件：

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`

解压缩&#x200B;**postman-ff.zip**&#x200B;并将以下2个文件存储在您桌面上的文件夹中：

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`
- `oauth_server_to_server.postman_environment.json`

![Adobe I/O新集成](./images/pmfolder1.png){zoomable="yes"}

在Postman中选择&#x200B;**导入**。

![Adobe I/O新集成](./images/postmanui.png){zoomable="yes"}

选择&#x200B;**文件**。

![Adobe I/O新集成](./images/choosefiles.png){zoomable="yes"}

从文件夹中选择三个文件，然后选择&#x200B;**打开**&#x200B;和&#x200B;**导入**。

![Adobe I/O新集成](./images/selectfiles.png){zoomable="yes"}

![Adobe I/O新集成](./images/impconfirm.png){zoomable="yes"}

现在，您已拥有Postman中所需的一切，可以开始通过API与Firefly服务交互。

## 请求访问令牌

接下来，为了确保您经过正确身份验证，您需要请求访问令牌。

通过验证右上角的环境下拉列表，在执行任何请求之前确保选择了正确的环境。 所选环境的名称应与此名称类似，`--aepUserLdap-- One Adobe OAuth Credential`。

![Postman](./images/envselemea1.png){zoomable="yes"}

所选环境的名称应与此名称类似，`--aepUserLdap-- One Adobe OAuth Credential`。

![Postman](./images/envselemea.png){zoomable="yes"}

现在您的Postman环境和收藏集已配置并正在运行，您可以从Postman向Adobe I/O进行身份验证。

在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，选择名为&#x200B;**POST — 获取访问令牌**&#x200B;的请求，然后选择&#x200B;**发送**。

请注意，在&#x200B;**查询参数**&#x200B;下，引用了两个变量： `API_KEY`和`CLIENT_SECRET`。 这些变量取自选定的环境`--aepUserLdap-- One Adobe OAuth Credential`。

![Postman](./images/ioauth.png){zoomable="yes"}

如果成功，将在Postman的&#x200B;**正文**&#x200B;部分中显示一个包含持有者令牌、访问令牌和到期窗口的响应。

![Postman](./images/ioauthresp.png){zoomable="yes"}

您应会看到包含以下信息的类似响应：

| 键 | 值 |
|:-------------:| :---------------:| 
| token_type | **持有人** |
| access_token | **eyJhbGciOiJSUz...** |
| expires_in | **86399** |

Adobe I/O **bearer-token**&#x200B;具有特定值（非常长的access_token）和到期窗口，现在有效期为24小时。 这意味着24小时后，如果您要使用Postman与Adobe API交互，则必须通过再次运行此请求来生成新令牌。

您的Postman环境现已设置完毕，可正常使用。

## 后续步骤

转到[要安装的应用程序](./ex9.md){target="_blank"}

返回[开始使用](./getting-started.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
