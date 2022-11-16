---
title: 区段激活到Microsoft Azure事件中心 — 配置Microsoft Azure环境
description: 区段激活到Microsoft Azure事件中心 — 配置Microsoft Azure环境
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 79711c1a-674c-4233-9c6c-af3bad6d0e0c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 13.0配置环境

## 13.0.1创建Azure订阅

>[!NOTE]
>
>如果您已经拥有Azure订阅，则可以跳过此步骤。 请继续练习13.0.2。

转到 [https://portal.azure.com](https://portal.azure.com) 并使用您的Azure帐户登录。 如果您没有Azure帐户，请使用您的个人电子邮件地址创建您的Azure帐户。

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

成功登录后，您将看到以下屏幕：

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

单击左侧菜单，然后选择 **所有资源**，如果您尚未订阅，则会显示Azure订阅屏幕。 在这种情况下，选择 **从Azure免费试用开始**.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

填写Azure订阅表，提供您的手机和信用卡以进行激活（您将有30天的免费套餐，除非升级，否则您无需支付费用）：

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

订阅过程完成后，您便可以：

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 13.0.2安装Visual Code Studio

您将使用Microsoft Visual Code Studio管理Azure项目。 您可以通过 [此链接](https://code.visualstudio.com/download). 按照同一网站上特定操作系统的安装说明进行操作。

## 13.0.3安装可视代码扩展

从安装Visual Studio代码的Azure函数 [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). 单击安装按钮：

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

从安装Azure帐户和Visual Studio代码登录 [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). 单击安装按钮：

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 13.0.4安装node.js

>[!NOTE]
>
>如果您已安装node.js，则可以跳过此步骤。 请继续练习13.0.5。

### macOS

确保 [家酿](https://brew.sh/) 先安装。 按照说明操作 [此处](https://brew.sh/).

![节点](./images/brew.png)

安装Homebrew后，运行以下命令：

```javascript
brew install node
```

### Windows

下载 [Windows安装程序](https://nodejs.org/en/#home-downloadhead) 直接从 [nodejs.org](https://nodejs.org/en/) 网站。

## 13.0.5验证node.js版本

对于此模块，您需要安装node.js版本12。 任何其他版本的node.js都可能导致练习13.5时出现问题。

在继续之前，请立即验证node.js的版本。

运行以下命令以验证node.js版本：

```javascript
node -v
```

如果您的版本低于或高于12，则需要升级或降级。

### 在macOS上升级/降级node.js版本

确保您拥有包 **n** 已安装。

安装包 **n**，运行此命令：

```javascript
sudo npm install -g n
```

如果您的版本低于或高于版本12，请运行此命令以升级或降级：

```javascript
sudo n 12.6.0
```

### 在Windows上升级/降级node.js版本

从Windows >控制面板>添加或删除程序中卸载node.js。

从安装所需版本 [nodejs.org](https://nodejs.org/en/) 网站。

## 13.0.6安装NPM包：请求

您需要安装包 **请求** 作为node.js设置的一部分。

安装包 **请求**，运行此命令：

```javascript
npm install request
```


下一步： [13.1配置Microsoft Azure EventHub环境](./ex1.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
