---
title: 使用Cursor.ai开发项目
description: 使用Cursor.ai开发项目
kt: 5342
doc-type: tutorial
source-git-commit: 2bfa7f4bee54df8411c96b001224d2986e9fcaf9
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 1.7.2使用Cursor.ai开发项目

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

接下来，您需要为Cursor.ai设置Commerce可扩展性工具。 输入以下命令，然后执行它。

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

通过为Cursor.ai安装Commerce可扩展性工具，现在有了MCP服务器作为Cursor.ai环境的一部分提供。 在接下来的练习中，您将使用该MCP服务器来帮助您开发和部署App Builder项目。

## 1.7.2.2设置您的webhook

在本练习中，您将需要配置一个webhook，以便在创建订单时，可以将订单事件流式传输到该webhook。 在本练习中，您将使用[https://pipedream.com/requestbin](https://pipedream.com/requestbin)的示例终结点。

转到[https://pipedream.com/requestbin](https://pipedream.com/requestbin)，创建一个帐户，然后创建一个工作区。 创建工作区后，您将看到类似以下的内容。

单击&#x200B;**复制**&#x200B;复制URL。 您需要在下一个练习中指定此URL。 此示例中的URL是`https://eodts05snjmjz67.m.pipedream.net`。

![Cursor.ai + Commerce](./images/webhook1.png)

## 1.7.2.3 Cursor.ai

打开Cursor.ai。 单击&#x200B;**打开项目**。

![Cursor.ai + Commerce](./images/cursorai14.png)

导航到您创建的文件夹，该文件夹应名为`--aepUserLdap---commerce`。 在该文件夹中，选择名为`commerce-integration-starter-kit`的文件夹。 单击&#x200B;**打开**。

![Cursor.ai + Commerce](./images/cursorai15.png)

您应该会看到此内容。 在继续之前，请确保在Cursor.ai中打开的顶级文件夹为`commerce-integration-starter-kit`。

![Cursor.ai + Commerce](./images/cursorai16.png)

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

## 后续步骤

返回到[适用于Adobe Commerce的智能开发人员工具](./aiassisteddev.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}