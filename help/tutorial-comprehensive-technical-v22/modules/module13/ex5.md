---
title: 区段激活到Microsoft Azure事件中心 — 定义Azure函数
description: 区段激活到Microsoft Azure事件中心 — 定义Azure函数
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b4a76dbc-bcea-47f6-bee3-889982f26ba8
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# 13.5创建Microsoft Azure项目

## 13.5.1熟悉Azure事件中心功能

Azure函数允许您运行小段代码(称为 **函数**)，而无需担心应用程序基础架构。 借助Azure功能，云基础架构提供您需要的所有最新服务器，以使应用程序能够大规模运行。

函数为 **触发** 按特定类型的事件。 支持的触发器包括响应数据中的更改、响应消息（例如事件中心）、按计划运行或由HTTP请求产生。

Azure函数是一种无服务器的计算服务，它允许您运行事件触发的代码，而无需显式配置或管理基础结构。

Azure事件中心与Azure函数集成，用于无服务器架构。

## 13.5.2打开Visual Studio代码并登录Azure

Visual Studio代码可轻松地……

- 定义Azure函数并将其绑定到事件中心
- 在本地测试
- 部署到Azure
- 远程日志功能执行

### 打开Visual Studio代码

要打开Visual Studio代码，请输入 **visual** 在操作系统的搜索中（OSX上的焦点搜索，在窗口的任务栏中搜索）。 如果未找到它，则需要重复 [练习0 — 先决条件](./ex0.md).

![visual-studio-code-icon.png](./images/visual-studio-code-icon.png)

### 登录到Azure

当您使用您用于注册的Azure帐户登录时 [练习0 — 先决条件](./ex0.md), Visual Studio代码将允许您查找和绑定所有事件中心资源。

单击 **Azure** 图标。 如果没有此选项，则安装所需的扩展时可能出现问题。

下一选择 **登录到Azure**:

![3-01-vsc-open.png](./images/3-01-vsc-open.png)

系统会将您重定向到浏览器以登录。 请记住选择用于注册的Azure帐户。

![3-02-vsc-pick-account.png](./images/3-02-vsc-pick-account.png)

当您在浏览器中看到以下屏幕时，您将使用Visual Code Studio登录：

![3-03-vsc-login-ok.png](./images/3-03-vsc-login-ok.png)

返回到Visual Code Studio（例如，您将看到Azure订阅的名称） **Azure订阅1**):

![3-04-vsc-logged-in.png](./images/3-04-vsc-logged-in.png)

## 13.5.3创建Azure项目

当您将鼠标悬停在 **Azure订阅1**，则会在部分上方显示一个菜单，选择 **新建项目……**:

![3-05-vsc-create-project.png](./images/vsc2.png)

选择您选择的本地文件夹以保存项目，然后单击 **选择**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

您现在将进入项目创建向导。 选择 **Javascript** 作为项目的语言：

![3-07-vsc-select-language.png](./images/vsc4.png)

选择 **Azure事件中心触发器** 作为您项目的第一个功能模板：

![3-08-vsc-function-template.png](./images/vsc5.png)

输入函数的名称，使用以下格式 `--demoProfileLdap---aep-event-hub-trigger` 然后按enter键：

![3-09-vsc-function-name.png](./images/vsc6.png)

选择 **创建新的本地应用程序设置**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

选择一个事件中心命名空间，您应会看到您在 **练习2**. 在此示例中，事件中心命名空间为 **vangeluw-aep启用**:

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

选择您的事件中心，您应会看到您在 **练习2**. 以我为例 **vangeluw-aep-enablement-event-hub**:

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

选择 **RootManageSharedAccessKey** 作为事件中心策略：

![3-13-vsc-function-select-eventhub-policy.png](./images/vsc10.png)

输入以使用 **$默认**:

![3-14-vsc-eventhub-consumer-group.png](./images/vsc11.png)

选择 **添加到工作区** 关于如何打开项目：

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

创建项目后，单击 **index.js** 要在编辑器中打开文件，请执行以下操作：

![3-16-vsc-open-index-js.png](./images/vsc13.png)

由Adobe Experience Platform发送到事件中心的有效负载将包含区段ID:

```json
[{
"segmentMembership": {
"ups": {
"ca114007-4122-4ef6-a730-4d98e56dce45": {
"lastQualificationTime": "2020-08-31T10:59:43Z",
"status": "realized"
},
"be2df7e3-a6e3-4eb4-ab12-943a4be90837": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
},
"39f0feef-a8f2-48c6-8ebe-3293bc49aaef": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
}
}
},
"identityMap": {
"ecid": [{
"id": "08130494355355215032117568021714632048"
}]
}
}]
```

将Visual Studio代码的index.js中的代码替换为以下代码。 每次Real-time CDP将区段资格发送到您的Event Hub目标时，都会执行此代码。 在我们的示例中，代码仅用于显示和增强接收的有效负载。 但您可以想象任何一种功能来实时处理区段资格。

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 13

// Main function
// -------------
// This azure function is fired for each segment activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received segment payload with the name fo the segment. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform segments in real-time to any application or platform that 
// would need to act upon an AEP segment qualiification.
// 

module.exports = async function (context, eventHubMessages) {

    return new Promise (function (resolve, reject) {

        context.log('Message : ' + JSON.stringify(eventHubMessages, null, 2));

        resolve();

    });    

};
```

结果应如下所示：

![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## 13.5.4运行Azure项目

现在是运行项目的时候了。 目前，我们不会将项目部署到Azure。 我们将在调试模式下在本地运行它。 选择运行图标，单击绿色箭头。

![3-17-vsc-run-project.png](./images/vsc14.png)

首次在调试模式下运行项目时，您需要附加Azure存储帐户，单击 **选择存储帐户**.

![3-17-vsc-run-project.png](./images/vsc15.png)

从存储帐户列表中，选择您在 [13.1.4设置您的Azure存储帐户](./ex1.md). 您的存储帐户已命名 `--demoProfileLdap--aepstorage`，例如： **meewisaepstorage**.

![3-22-vsc-select-storage-account.png](./images/vsc16.png)

您的项目现已启动并正在运行，并且正在列出事件中心中的事件。 在下一个练习中，您将演示Luma演示网站上将使您有资格访问这些区段的行为。 因此，您将在Event Hub触发功能的终端中收到区段鉴别有效负载：

![3-23-vsc-application-started.png](./images/vsc17.png)

## 13.5.5停止Azure项目

要停止项目，请选择 **终端** ，单击“终端”窗口并按 **CMD-C** 在OSX或 **CTRL-C** 在Windows上：

![3-24-vsc-application-stop.png](./images/vsc18.png)

下一步： [13.6端到端方案](./ex6.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
