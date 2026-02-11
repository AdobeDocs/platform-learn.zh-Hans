---
title: 使用光标开发项目
description: 使用光标开发项目
kt: 5342
doc-type: tutorial
exl-id: c73498b6-5e08-41b5-81a9-c0a76a6e2792
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# 1.7.2使用Cursor开发项目

## 1.7.2.1设置您的目录和工具

在您的桌面上，创建一个名为`--aepUserLdap---commerce`的新目录

![Commerce和代理](./images/cursorai1.png)

右键单击您的文件夹，然后选择&#x200B;**在文件夹新建终端**。

![Commerce和代理](./images/cursorai2.png)

您应该会看到此内容。

![Commerce和代理](./images/cursorai3.png)

您现在需要克隆现有的Github存储库，以便查看[https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit)。

此存储库是Adobe的集成入门工具包，它使用Adobe Developer App Builder提高Adobe Commerce与其他后台系统（如ERP、CRM和PIM）的集成的实时连接可靠性并缩短上市时间。

![Commerce和代理](./images/cursorai4.png)

有多种方法可克隆此存储库，在此示例中使用“终端”。

在“终端”窗口中输入以下命令并执行它。

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce和代理](./images/cursorai5.png)

几秒钟后，您应该会看到此结果。

![Commerce和代理](./images/cursorai6.png)

接下来，您应该导航到刚刚创建的文件夹。 输入以下命令，然后执行它。

`cd commerce-integration-starter-kit`

![Commerce和代理](./images/cursorai7.png)

您应该会看到此内容。

![Commerce和代理](./images/cursorai8.png)

接下来，您需要为Cursor设置Commerce可扩展性工具。 输入以下命令，然后执行它。

`aio commerce extensibility tools-setup`

![Commerce和代理](./images/cursorai9.png)

选择&#x200B;**当前目录**。

![Commerce和代理](./images/cursorai10.png)

选择&#x200B;**游标**。

![Commerce和代理](./images/cursorai11.png)

选择&#x200B;**npm**。

![Commerce和代理](./images/cursorai12.png)

几分钟后，您应该会看到此内容。

![Commerce和代理](./images/cursorai13.png)

通过安装用于Cursor的Commerce可扩展性工具，现在可以将MCP服务器作为Cursor环境的一部分提供。 在接下来的练习中，您将使用该MCP服务器来帮助您开发和部署App Builder项目。

## 1.7.2.2设置您的webhook

在本练习中，您将需要配置一个webhook，以便在创建订单时，可以将订单事件流式传输到该webhook。 在本练习中，您将使用[https://pipedream.com/requestbin](https://pipedream.com/requestbin)的示例终结点。

转到[https://pipedream.com/requestbin](https://pipedream.com/requestbin)，创建一个帐户，然后创建一个工作区。 创建工作区后，您将看到类似以下的内容。

单击&#x200B;**复制**&#x200B;复制URL。 您需要在下一个练习中指定此URL。 此示例中的URL是`https://eodts05snjmjz67.m.pipedream.net`。

![Cursor + Commerce](./images/webhook1.png)

## 1.7.2.3使用光标创建应用程序

打开光标。 单击&#x200B;**打开项目**。

![Cursor + Commerce](./images/cursorai14.png)

导航到您创建的文件夹，该文件夹应名为`--aepUserLdap---commerce`。 在该文件夹中，选择名为`commerce-integration-starter-kit`的文件夹。 单击&#x200B;**打开**。

![Cursor + Commerce](./images/cursorai15.png)

您应该会看到此内容。 在继续之前，请确保在Cursor中打开的顶级文件夹为`commerce-integration-starter-kit`。

![Cursor + Commerce](./images/cursorai16.png)

使用键盘快捷键`Cmd + Shift + J`打开“光标”设置。 您应该会看到此内容。 转到&#x200B;**工具&amp; MCP**。

![Cursor + Commerce](./images/cursorai17.png)

启用MCP服务器&#x200B;**commerce-extensibility**。 完成后，单击&#x200B;**X**&#x200B;关闭窗口。

![Cursor + Commerce](./images/cursorai18.png)

复制以下提示并将其粘贴到光标中。 然后，单击&#x200B;**发送**&#x200B;按钮。

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

![Cursor + Commerce](./images/cursorai19.png)

游标将开始推理和执行。 光标会要求您确认几次。 发生这种情况时，请单击&#x200B;**运行**。 根据推理和您的设置，这种情况可能会出现5-10次。

![Cursor + Commerce](./images/cursorai20.png)

几分钟后，您应该会看到类似这样的内容。

![Cursor + Commerce](./images/cursorai21.png)

如Cursor所示，下一步是创建名为`.env`的文件，并在其中提供所需的变量。

## 1.7.2.4创建您的.env文件

选择文件&#x200B;**env.dist**。 输入命令`Cmd + C`，然后输入命令`Cmd + V`。

![Cursor + Commerce](./images/cursorai22.png)

将新创建的文件重命名为`.env`。

![Cursor + Commerce](./images/cursorai23.png)

接下来，您需要为文件&#x200B;**.env**&#x200B;中的所有变量提供值。

![Cursor + Commerce](./images/cursorai24.png)

您可以在此处找到所有必需的信息。

### Commerce端点

您可以通过转到[https://experience.adobe.com](https://experience.adobe.com)找到这些变量。 单击&#x200B;**Commerce**。

![Cursor + Commerce](./images/cursorai25.png)

您应该会看到此内容。 单击ACCS环境旁边的&#x200B;**信息**&#x200B;图标，该图标应命名为`--aepUserLdap-- - ACCS`。 复制REST端点和GraphQL端点的值。

在本例中，这些是要复制的值。 将它们粘贴到文件&#x200B;**.env**&#x200B;第6行和第7行的以下变量旁边。


- **COMMERCE_BASE_URL** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/
- **COMMERCE_GRAPHQL_ENDPOINT** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/graphql

![Cursor + Commerce](./images/cursorai26.png)

然后，您应将它放入文件&#x200B;**.env**&#x200B;中。

![Cursor + Commerce](./images/cursorai26a.png)

### Adobe I/O项目变量

您可以通过转到[https://developer.adobe.com/console](https://developer.adobe.com/console)找到这些变量。 转到&#x200B;**项目**，然后单击以打开您在上一个练习中创建的、应命名为`--aepUserLdap-- Commerce Events`的Adobe I/O项目。

![Cursor + Commerce](./images/cursorai27.png)

转到&#x200B;**生产**。

![Cursor + Commerce](./images/cursorai28.png)

转到&#x200B;**OAuth服务器到服务器**。 您应该会看到此内容。

![Cursor + Commerce](./images/cursorai29.png)

复制字段&#x200B;**客户端ID**、**客户端密钥**、**技术帐户ID**、**技术帐户电子邮件**&#x200B;和&#x200B;**组织ID**&#x200B;的值，并将其粘贴到文件&#x200B;**.env**&#x200B;中第13-17行的以下变量旁边。

- **OAUTH_CLIENT_ID**= **客户端ID**
- **OAUTH_CLIENT_SECRET**= **客户端密钥**
- **OAUTH_TECHNICAL_ACCOUNT_ID**= **技术帐户ID**
- **OAUTH_TECHNICAL_ACCOUNT_EMAIL**= **技术帐户电子邮件**
- **OAUTH_ORG_ID**= **组织ID**

然后，您应将它放入文件&#x200B;**.env**&#x200B;中。

![Cursor + Commerce](./images/cursorai29a.png)

### Commerce_ADOBE_IO_EVENTS_MERCHANT_ID

对于字段&#x200B;**COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID=**，请在文件`--aepUserLdap--_commerce_events`.env **中输入第34行的值**。

然后，您应将它放入文件&#x200B;**.env**&#x200B;中。

![Cursor + Commerce](./images/cursorai30.png)

### Workspace配置

要检索这些变量，请返回您的Adobe I/O项目，然后单击&#x200B;**Workspace概述**。

在转到&#x200B;**Workspace概述**&#x200B;后，请查看URL，它应如下所示： **https://developer.adobe.com/console/projects/133309/4566206088345586770/workspaces/4566206088345619105/details**。

此示例中的第一个数字133309是用于字段&#x200B;**IO_CONSUMER_ID**&#x200B;的值。
此示例中的第二个数字4566206088345586770是用于字段&#x200B;**IO_PROJECT_ID**&#x200B;的值。
此示例中的第三个数字4566206088345619105是用于字段&#x200B;**IO_WORKSPACE_ID**&#x200B;的值。

![Cursor + Commerce](./images/cursorai31.png)

- **IO_CONSUMER_ID**= 133309
- **IO_PROJECT_ID**= 4566206088345586770
- **IO_WORKSPACE_ID**= 4566206088345619105

复制这些值，并将其粘贴到文件&#x200B;**.env**&#x200B;中第42-44行的以下变量旁边。

![Cursor + Commerce](./images/cursorai32.png)

### EVENT_PREFIX

对于字段&#x200B;**EVENT_PREFIX =**，在文件`--aepUserLdap--_`.env **的第47行中输入值**。

然后，您应将它放入文件&#x200B;**.env**&#x200B;中。

![Cursor + Commerce](./images/cursorai33.png)

### Webhook

对于字段&#x200B;**ORDER_WEBHOOK_URL**，您应该粘贴本练习前面创建的webhook的URL，它应该如下所示： `https://eodts05snjmjz67.m.pipedream.net`。

然后，您应将它放入文件&#x200B;**.env**&#x200B;中。

![Cursor + Commerce](./images/cursorai34.png)

### App Builder凭据

您应该更新文件&#x200B;**.env**&#x200B;中第54-55行的以下变量：

- **AIO_RUNTIME_NAMESPACE**=
- **AIO_RUNTIME_AUTH**=

您可以通过返回您的Adobe I/O项目来检索这些变量的值。 转到&#x200B;**Workspace概述**&#x200B;并单击&#x200B;**全部下载**。

![Cursor + Commerce](./images/cursorai35.png)

随后将下载类似这样的文件。 使用文本编辑器打开该文件。

![Cursor + Commerce](./images/cursorai36.png)

向右滚动，直到看到&#x200B;**运行时**。 然后您应该会看到包含&#x200B;**AIO_RUNTIME_NAMESPACE**&#x200B;值的字段&#x200B;**name**。

![Cursor + Commerce](./images/cursorai37.png)

进一步向右滚动直到看到&#x200B;**auth**，其中包含&#x200B;**AIO_RUNTIME_AUTH**&#x200B;的值。

![Cursor + Commerce](./images/cursorai38.png)

将这两个值粘贴到文件&#x200B;**.env**&#x200B;的第54-55行上，然后您应该拥有它。

![Cursor + Commerce](./images/cursorai39.png)

您的&#x200B;**.env**&#x200B;文件现已完全配置。

## 1.7.2.5工作区.json

在上一步中，您从Adobe I/O项目下载了类似这样的文件。

![Cursor + Commerce](./images/cursorai36.png)

重命名该文件并使用名称`workspace.json`。

![Cursor + Commerce](./images/cursorai40.png)

将文件复制到目录&#x200B;**脚本**>**上线**>**配置**&#x200B;中。

![Cursor + Commerce](./images/cursorai41.png)

## 1.7.2.6 Adobe I/O登录

返回您以前使用的终端窗口。 输入命令`aio login`。

![Cursor + Commerce](./images/cursorai44.png)

随后，您应该会在通过浏览器登录后看到此信息。

![Cursor + Commerce](./images/cursorai45.png)

## 1.7.2.7准备部署

复制以下提示并将其粘贴到光标中。 然后，单击&#x200B;**发送**&#x200B;按钮。

`Please deploy this code to Adobe I/O`

![Cursor + Commerce](./images/cursorai42.png)

单击&#x200B;**运行**&#x200B;以允许操作，光标可能会要求您多次确认操作。

![Cursor + Commerce](./images/cursorai43.png)

部署将在几分钟后完成。

![Cursor + Commerce](./images/cursorai46.png)

复制以下提示并将其粘贴到光标中。 然后，单击&#x200B;**发送**&#x200B;按钮。

`run the onboarding to commerce`

![Cursor + Commerce](./images/cursorai50.png)

几分钟后，您应该会看到此内容。

![Cursor + Commerce](./images/cursorai51.png)

复制以下提示并将其粘贴到光标中。 然后，单击&#x200B;**发送**&#x200B;按钮。

`subscribe to commerce events`

![Cursor + Commerce](./images/cursorai47.png)

几分钟后，您应该会看到此内容。

![Cursor + Commerce](./images/cursorai49.png)

## 1.7.2.8在Adobe Commerce as a Cloud Service中验证配置

转到[https://experience.adobe.com](https://experience.adobe.com)。 单击&#x200B;**Commerce**。

![Cursor + Commerce](./images/cursorai60.png)

单击您的Adobe Commerce as a Cloud Service环境以将其打开，然后登录。

![Cursor + Commerce](./images/cursorai61.png)

转到&#x200B;**系统**，然后转到&#x200B;**事件订阅**。

![Cursor + Commerce](./images/cursorai62.png)

然后，您应该会看到此事件订阅列表。

![Cursor + Commerce](./images/cursorai63.png)

转到&#x200B;**商店**，然后转到&#x200B;**配置**。

![Cursor + Commerce](./images/cursorai64.png)

转到&#x200B;**Adobe服务**&#x200B;并选择&#x200B;**Adobe I/O Events**。 然后，您应该看到字段&#x200B;**Adobe I/O Workspace配置**&#x200B;的值包含几个星号，并且字段&#x200B;**贸易商ID**&#x200B;也应该具有类似于`--aepUserLdap--_commerce_events`的值。

![Cursor + Commerce](./images/cursorai65.png)

完成此配置后，您现在可以测试配置。

## 1.7.2.9测试您的方案

打开您的网站。

![Cursor + Commerce](./images/cursorai101.png)

转到&#x200B;**监视**&#x200B;并单击任何产品。

![Cursor + Commerce](./images/cursorai102.png)

配置产品并单击&#x200B;**添加到购物车**。

![Cursor + Commerce](./images/cursorai103.png)

单击&#x200B;**购物车**&#x200B;图标并选择&#x200B;**结帐**。

![Cursor + Commerce](./images/cursorai104.png)

填写您的详细信息，然后单击&#x200B;**下订单**。

![Cursor + Commerce](./images/cursorai105.png)

然后，您应该会看到订单确认。

![Cursor + Commerce](./images/cursorai106.png)

切换到webhook应用程序。 您现在应该会看到刚刚确认的订单的传入事件。

![Cursor + Commerce](./images/cursorai107.png)

## 1.7.2.10 Adobe I/O调试

返回您的Adobe I/O项目。 转到&#x200B;**Workspace概述**。 您应会看到类似以下的内容。 向下滚动一点。

![Cursor + Commerce](./images/cursorai108.png)

单击以打开&#x200B;**Commerce订单同步**。

![Cursor + Commerce](./images/cursorai109.png)

转到&#x200B;**调试跟踪**。 您可以在该处找到最新的传入事件及其有效负载。 这有助于了解已处理哪些事件以及是否成功处理了这些事件。

![Cursor + Commerce](./images/cursorai110.png)

## 后续步骤

返回到[适用于Adobe Commerce的智能开发人员工具](./aiassisteddev.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
