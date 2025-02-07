---
title: Firefly服务快速入门
description: 了解如何使用Postman和Adobe I/O查询Adobe Firefly服务API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: e6a549441d425801f2a554da9af803dca646009e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 1.1.1Firefly服务快速入门

了解如何使用Postman和Adobe I/O查询Adobe Firefly服务API。

## 1.1.1.2配置Adobe I/O项目

在本练习中，将使用Adobe I/O根据Firefly服务API进行查询。 按照以下步骤设置Adobe I/O。

1. 转到[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新集成](./images/iohome.png)

1. 确保在屏幕右上角选择正确的实例。 您的实例为`--aepImsOrgName--`。 接下来，选择&#x200B;**新建项目**。

![Adobe I/O新集成](./images/iocomp.png)

1. 选择&#x200B;**+添加到项目**&#x200B;并选择&#x200B;**API**。

![Adobe I/O新集成](./images/adobe_io_access_api.png)

您的屏幕应如下所示。

![Adobe I/O新集成](./images/api1.png)

1. 选择&#x200B;**Creative Cloud**&#x200B;并选择&#x200B;**Firefly-Firefly服务**，然后选择&#x200B;**下一步**。

![Adobe I/O新集成](./images/api3.png)

1. 为您的凭据提供一个名称： `--aepUserLdap-- - Firefly Services OAuth credential`并选择&#x200B;**下一步**。

![Adobe I/O新集成](./images/api4.png)

1. 选择默认配置文件&#x200B;**默认Firefly服务配置**，然后选择&#x200B;**保存配置的API**。

![Adobe I/O新集成](./images/api9.png)

您的Adobe I/O集成现已准备就绪。

![Adobe I/O新集成](./images/api11.png)

## 1.1.1.3下载Postman环境

1. 选择&#x200B;**下载Postman**，然后选择&#x200B;**OAuth服务器到服务器**&#x200B;以下载Postman环境。

![Adobe I/O新集成](./images/iopm.png)

1. 选择您的项目名称。

![Adobe I/O新集成](./images/api13.png)

1. 选择&#x200B;**编辑项目**。

![Adobe I/O新集成](./images/api14.png)

1. 为您的集成输入友好名称： `--aepUserLdap-- Firefly`并选择&#x200B;**保存**。

![Adobe I/O新集成](./images/api15.png)

Adobe I/O集成的设置现已完成。

![Adobe I/O新集成](./images/api16.png)

## 1.1.1.4 Postman对Adobe I/O的身份验证

>[!IMPORTANT]
>
>如果您是Adobe员工，请按照此处的说明使用[PostBuster](./../../../postbuster.md)。

1. 在[Postman下载](https://www.postman.com/downloads/){target="_blank"}上下载并安装适用于您的操作系统的相关Postman版本。

![Adobe I/O新集成](./images/getstarted.png)

1. 启动应用程序。

在Postman中，有2个概念：环境和收藏集。

- 环境文件包含所有比较一致或不太一致的环境变量。 在该环境中，您可以找到Adobe环境的IMSOrg等内容，以及客户端ID和其他安全凭据。 您之前在Adobe I/O设置过程中下载了名为&#x200B;**`oauth_server_to_server.postman_environment.json`**&#x200B;的环境文件。

- 收藏集包含大量您可以使用的API请求。 我们将使用2个收藏集
   - 1个集合用于Adobe I/O的身份验证
   - 1本模块中的练习的集合

1. 将[postman.zip](./../../../assets/postman/postman-ff.zip)下载到本地桌面。

![Adobe I/O新集成](./images/pmfolder.png)

在&#x200B;**postman.zip**&#x200B;文件中包含以下文件：

    - &#39;AdobeIO - OAuth.postman_collection.json&#39;
    - &#39;FF -Firefly服务技术人员.postman_collection.json&#39;

1. 解压缩&#x200B;**postman-ff.zip**&#x200B;并将以下2个文件存储在您桌面上的文件夹中：
- AdobeIO - OAuth.postman_collection.json
- FF -Firefly服务技术人员.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Adobe I/O新集成](./images/pmfolder1.png)

1. 在Postman中选择&#x200B;**导入**。

![Adobe I/O新集成](./images/postmanui.png)

1. 选择&#x200B;**文件**。

![Adobe I/O新集成](./images/choosefiles.png)

1. 从文件夹中选择三个文件，然后选择&#x200B;**打开**&#x200B;和&#x200B;**导入**。

![Adobe I/O新集成](./images/selectfiles.png)

![Adobe I/O新集成](./images/impconfirm.png)

否，您已在Postman中获得开始通过API与Firefly服务交互所需的一切。

## 1.1.1.5请求访问令牌

接下来，为了确保您经过正确身份验证，您需要请求访问令牌。

1. 通过验证右上角的环境下拉列表，在执行任何请求之前确保选择了正确的环境。 所选环境的名称应与此名称类似，`--aepUserLdap-- Firefly Services OAuth Credential`。

![Postman](./images/envselemea1.png)

所选环境的名称应与此名称类似，`--aepUserLdap-- Firefly Services OAuth Credential`。

![Postman](./images/envselemea.png)

现在您的Postman环境和收藏集已配置并正在运行，您可以从Postman对Adobe I/O进行身份验证。

1. 在&#x200B;**AdobeIO - OAuth**&#x200B;集合中，选择名为&#x200B;**POST — 获取访问令牌**&#x200B;的请求，然后选择&#x200B;**发送**。

请注意，在&#x200B;**查询参数**&#x200B;下，引用了两个变量： `API_KEY`和`CLIENT_SECRET`。 这些变量取自选定的环境`--aepUserLdap-- Firefly Services OAuth Credential`。

![Postman](./images/ioauth.png)

如果成功，将在Postman的&#x200B;**正文**&#x200B;部分中显示一个包含持有者令牌、访问令牌和到期窗口的响应。

![Postman](./images/ioauthresp.png)


您应会看到包含以下信息的类似响应：

| 键 | 值 |
|:-------------:| :---------------:| 
| token_type | **持有人** |
| access_token | **eyJhbGciOiJSU...** |
| expires_in | **86399** |

Adobe I/O **bearer-token**&#x200B;具有特定值（非常长的access_token）和到期窗口，现在有效期为24小时。 这意味着24小时后，如果您要使用Postman对Adobe I/O进行身份验证，则必须通过再次运行此请求来生成新令牌。

## 1.1.1.6Firefly服务API，文本2图像

现在，您已准备好将您的第一个请求发送到Firefly服务API。

1. 从&#x200B;**FF - Request Services Tech Insiders**&#x200B;集合中选择名为&#x200B;**POST- Request - T2I V3**&#x200B;的Firefly。Firefly

![Firefly](./images/ff1.png)

1. 从响应中复制图像URL，然后在Web浏览器中打开该URL以查看图像。

![Firefly](./images/ff2.png)

您应该会看到一个美妙的图像，其中描绘了`horses in a field`。

![Firefly](./images/ff3.png)

在继续下一个练习之前，请随时尝试使用API请求。

## 后续步骤

转到[使用Microsoft Azure和预签名URL优化您的Firefly过程](./ex2.md){target="_blank"}

返回[Adobe Firefly服务概述](./firefly-services.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
