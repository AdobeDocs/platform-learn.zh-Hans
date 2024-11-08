---
title: 区段激活到Microsoft Azure事件中心 — 配置Microsoft Azure环境
description: 区段激活到Microsoft Azure事件中心 — 配置Microsoft Azure环境
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 2.4.0配置环境

## 2.4.0.1创建Azure订阅

>[!NOTE]
>
>如果您已经拥有Azure订阅，则可以跳过此步骤。 请继续进行13.0.2练习。

转到[https://portal.azure.com](https://portal.azure.com)并使用您的Azure帐户登录。 如果您没有个人电子邮件地址，请使用个人电子邮件地址创建您的Azure帐户。

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

成功登录后，您将看到以下屏幕：

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

单击左侧的菜单并选择&#x200B;**所有资源**，如果您尚未订阅，将显示Azure订阅屏幕。 在这种情况下，请选择&#x200B;**开始使用Azure免费试用**。

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

填写Azure订阅表单，提供用于激活的移动电话和信用卡（您将有30天的免费套餐，除非您升级，否则不会向您收费）：

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

订阅过程完成后，您可以：

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 2.4.0.2安装Visual Code Studio

您将使用Microsoft Visual Code Studio来管理您的Azure项目。 您可以通过[此链接](https://code.visualstudio.com/download)下载它。 按照同一网站上特定操作系统的安装说明进行操作。

## 2.4.0.3安装可视化代码扩展

从[https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)安装Visual Studio代码的Azure函数。 单击安装按钮：

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

安装Azure帐户并从[https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)登录Visual Studio Code。 单击安装按钮：

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 2.4.0.4安装节点.js

>[!NOTE]
>
>如果已安装node.js，则可以跳过此步骤。 在这种情况下，请继续进行练习13.0.5。

### macOS

确保先安装[Homebrew](https://brew.sh/)。 按[此处](https://brew.sh/)的说明操作。

![节点](./images/brew.png)

安装Homebrew后，请运行此命令：

```javascript
brew install node
```

### Windows

直接从[nodejs.org](https://nodejs.org/en/)网站下载[Windows安装程序](https://nodejs.org/en/#home-downloadhead)。

## 2.4.0.5验证node.js版本

对于此模块，您需要安装node.js版本12。 node.js的任何其他版本都可能会导致练习13.5出现问题。

在继续之前，请立即验证您的node.js版本。

运行此命令以验证您的node.js版本：

```javascript
node -v
```

如果您的版本低于12或高于12，则需要升级或降级。

### 在macOS上升级/降级node.js版本

确保您已安装包&#x200B;**n**。

要安装包&#x200B;**n**，请运行此命令：

```javascript
sudo npm install -g n
```

如果版本低于或高于版本12，请运行此命令升级或降级：

```javascript
sudo n 12.6.0
```

### 在Windows上升级/降级node.js版本

从“Windows”>“控制面板”>“添加或删除程序”中卸载node.js。

正在从[nodejs.org](https://nodejs.org/en/)网站安装所需版本。

## 2.4.0.6安装NPM包：请求

您需要在node.js安装程序中安装包&#x200B;**请求**。

要安装包&#x200B;**请求**，请运行此命令：

```javascript
npm install request
```


下一步： [2.4.1配置您的Microsoft Azure EventHub环境](./ex1.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
