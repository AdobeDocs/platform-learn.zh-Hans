---
title: 区段激活到Microsoft Azure事件中心 — 操作
description: 区段激活到Microsoft Azure事件中心 — 操作
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6端到端方案

## 13.6.1启动Azure事件中心触发器

要显示Adobe Experience Platform Real-time CDP在区段鉴别后发送到我们的Azure事件中心的有效负载，我们需要启动简单的Azure事件中心触发器功能。 此函数将简单地在Visual Studio代码中将有效负载“转储”到控制台。 但请记住，此函数可以通过任何方式扩展，以便使用专用API和协议与各种环境进行接口。

### 启动Visual Studio代码并启动项目

确保打开并运行您的Visual Studio代码项目

要在Visual Studio代码中启动/停止/重新启动Azure函数，请参阅以下练习：

- [练习13.5.4 — 启动Azure项目](./ex5.md)
- [练习13.5.5 — 停止Azure项目](./ex5.md)

您的Visual Studio代码 **终端** 应提及类似以下内容：

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2加载您的Luma网站

转到 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](../module0/images/web8.png)

您现在可以按照以下流程访问网站。 单击 **集成**.

![DSN](../module0/images/web1.png)

在 **集成** 页面，您需要选择在练习0.1中创建的数据收集属性。

![DSN](../module0/images/web2.png)

然后，您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../module0/images/web3.png)

打开新的隐身浏览器窗口。

![DSN](../module0/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../module0/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../module0/images/web6.png)

然后，您将在无痕浏览器窗口中看到您的网站已加载。 对于每个演示，您需要使用全新的、隐身的浏览器窗口来加载演示网站URL。

![DSN](../module0/images/web7.png)

## 13.6.3符合您在设备领域的权益

导航到 **设备** 页面一次，和 **不重新加载或刷新**. 此操作应使您符合 `--demoProfileLdap-- - Interest in Equipment` 区段。

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

要进行验证，请打开“配置文件查看器”面板。 您现在应该是 `--demoProfileLdap-- - Interest in Equipment`. 如果您的区段成员关系在配置文件查看器面板中尚未更新，请单击重新加载按钮。

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

切换回Visual Studio代码，然后查看 **终端** 选项卡，您应会看到 **ECID**. 只要您符合 `--demoProfileLdap-- - Interest in Equipment` 区段。

当您仔细查看区段有效负载时，您可以看到 `--demoProfileLdap-- - Interest in Equipment` 处于状态 **实现**.

区段状态为 **实现** 表示我们的用户档案刚刚进入区段。 而 **现有** 状态表示我们的用户档案继续位于区段中。

![6-06-vsc-activation-realized.png](./images/luma3.png)

## 13.6.4再次访问“设备”页面

硬刷新 **设备** 页面。

![6-07-back-to-sports.png](./images/luma1.png)

现在，切换回Visual Studio代码并验证 **终端** 选项卡。 您将看到我们仍然拥有您的区段，但现在处于状态 **现有** 这意味着我们的用户档案将继续保留在区段中。

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 13.6.5第三次访问体育页面

如果您重新访问 **体育** 页面，因为区段视图的状态没有变化，所以不会进行激活。

仅当区段的状态发生更改时，才会进行区段激活：

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

下一步： [摘要和优点](./summary.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
