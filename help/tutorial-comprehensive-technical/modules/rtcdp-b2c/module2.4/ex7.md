---
title: Audience Activation到Microsoft Azure事件中心 — 操作
description: Audience Activation到Microsoft Azure事件中心 — 操作
kt: 5342
doc-type: tutorial
exl-id: f5b224bf-60b9-46e0-abdb-9d96a7e8c59f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 2.4.7端到端方案

## 启动Azure事件中心触发器

要显示Adobe Experience Platform Real-time CDP在受众资格鉴定后发送到我们的Azure事件中心的有效负载，我们需要启动简单的Azure事件中心触发函数。 此函数将简单地将有效负载“转储”到Visual Studio Code中的控制台。 但请记住，此函数可以通过任何方式扩展到使用专用API和协议与各种环境进行接口。

### 启动Visual Studio代码并启动项目

确保已打开并运行您的Visual Studio代码项目

要在Visual Studio Code中启动/停止/重新启动Azure函数，请参阅上一个练习。

您的Visual Studio代码的&#x200B;**终端**&#x200B;应提及类似以下的内容：

```code
[2024-11-20T20:07:12.316Z] Debugger listening on ws://127.0.0.1:9229/86c8e251-8e2f-4c65-a063-cda77edbf2ca
[2024-11-20T20:07:12.318Z] For help, see: https://nodejs.org/en/docs/inspector
[2024-11-20T20:07:12.343Z] Worker process started and initialized.
[2024-11-20T20:07:12.359Z] Debugger attached.

Functions:

        vangeluw-aep-event-hub-trigger: eventHubTrigger

For detailed output, run func with --verbose flag.
[2024-11-20T20:07:18.150Z] Host lock lease acquired by instance ID '000000000000000000000000000C19D8'.
```

## 加载Citi Signal网站

转到[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登录后，您将看到此内容。 单击网站项目上的3个点&#x200B;**...**，然后单击&#x200B;**运行**&#x200B;以将其打开。

![DSN](./../../datacollection/module1.1/images/web8.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个练习，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

## 符合受众资格

导航到&#x200B;**计划**&#x200B;页面。 此操作将使您符合`--aepUserLdap-- - Interest in Plans`受众的条件。

![6-04-luma-telco-nav-sports.png](./images/cs1.png)

要进行验证，请打开“配置文件查看器”面板。 您现在应该是`--aepUserLdap-- - Interest in Plans`的成员。 如果配置文件查看器面板中尚未更新受众成员资格，请单击重新加载按钮。

![6-05-luma-telco-nav-broadband.png](./images/cs2.png)

切换回Visual Studio代码并查看&#x200B;**终端**&#x200B;选项卡，您应该会看到特定&#x200B;**ECID**&#x200B;的受众列表。 此激活有效负载会在您符合`--aepUserLdap-- - Interest in Plans`受众资格后立即交付到您的事件中心。

![6-06-vsc-activation-realized.png](./images/cs3.png)

当您更仔细地查看受众有效负载时，可以看到`--aepUserLdap-- - Interest in Plans`处于&#x200B;**已实现**&#x200B;状态。

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

受众状态&#x200B;**已实现**&#x200B;表示您的个人资料是受众的一部分，而&#x200B;**已退出**&#x200B;状态表示我们的个人资料已从受众中删除。

下一步：[摘要和优点](./summary.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
