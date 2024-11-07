---
title: 区段激活到Microsoft Azure事件中心 — 操作
description: 区段激活到Microsoft Azure事件中心 — 操作
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.4.6端到端方案

## 2.4.6.1启动Azure事件中心触发器

要显示Adobe Experience Platform Real-time CDP在区段鉴别后发送到我们的Azure事件中心的有效负载，我们需要启动简单的Azure事件中心触发函数。 此函数将简单地将有效负载“转储”到Visual Studio Code中的控制台。 但请记住，此函数可以通过任何方式扩展到使用专用API和协议与各种环境进行接口。

### 启动Visual Studio代码并启动项目

确保已打开并运行您的Visual Studio代码项目

要在Visual Studio Code中启动/停止/重新启动Azure函数，请参阅以下练习：

- [练习13.5.4 — 启动Azure项目](./ex5.md)
- [练习13.5.5 — 停止Azure项目](./ex5.md)

您的Visual Studio代码的&#x200B;**终端**&#x200B;应提及类似以下的内容：

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 2.4.6.2加载您的Luma网站

转到[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

您现在可以按照以下流程访问该网站。 单击&#x200B;**集成**。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

在&#x200B;**集成**&#x200B;页面上，您需要选择在练习0.1中创建的数据收集属性。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个演示，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

## 2.4.6.3符合您在设备领域的兴趣条件

导航到&#x200B;**设备**&#x200B;页面一次，并且&#x200B;**不重新加载或刷新它**。 此操作应该会使您符合`--aepUserLdap-- - Interest in Equipment`区段的条件。

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

要进行验证，请打开“配置文件查看器”面板。 您现在应该是`--aepUserLdap-- - Interest in Equipment`的成员。 如果配置文件查看器面板中尚未更新区段成员资格，请单击重新加载按钮。

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

切换回Visual Studio代码并查看&#x200B;**终端**&#x200B;选项卡，您应该会看到特定&#x200B;**ECID**&#x200B;的区段列表。 此激活有效负载会在您符合`--aepUserLdap-- - Interest in Equipment`区段的资格后立即交付到您的事件中心。

当您更仔细地查看区段有效负载时，可以看到`--aepUserLdap-- - Interest in Equipment`处于&#x200B;**已实现**&#x200B;状态。

区段状态为&#x200B;**已实现**，这意味着我们的用户档案刚刚进入该区段。 而&#x200B;**existing**&#x200B;状态意味着我们的配置文件继续位于区段中。

![6-06-vsc-activation-realized.png](./images/luma3.png)

## 2.4.6.4再次访问“设备”页面

对&#x200B;**设备**&#x200B;页面进行硬刷新。

![6-07-back-to-sports.png](./images/luma1.png)

现在，切换回Visual Studio Code并验证您的&#x200B;**终端**&#x200B;选项卡。 您将看到我们仍然保留您的区段，但现在处于&#x200B;**existing**&#x200B;状态，这意味着我们的配置文件继续保留在区段中。

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 2.4.6.5第三次访问“体育”页面

如果您第三次重新访问&#x200B;**Sports**&#x200B;页面，将不会进行激活，因为从区段角度来看，状态不会发生更改。

区段激活仅在区段的状态发生变化时发生：

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

下一步：[摘要和优点](./summary.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
