---
title: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Analytics和Adobe Audience Manager
description: 基础 — 设置Adobe Experience Platform数据收集和Web SDK扩展 — 实施Adobe Analytics和Adobe Audience Manager
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: e3ef6534-9af9-4b8c-86d0-46f413f4ff6d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 11%

---

# 1.5 — 实施Adobe Analytics和Adobe Audience Manager

## 上下文

您现在知道XDM数据正在流入平台。 您将进一步了解XDM的功能 [模块2](./../module2/data-ingestion.md)，以及如何构建您自己的架构以跟踪自定义变量。 目前，您将查看在设置数据流以将数据转发到Analytics和Audience Manager时发生的情况。

## 1.5.1在Analytics中映射变量

Adobe Experience Platform [!DNL Web SDK] 自动映射某些值，从而尽可能快地通过Web SDK实现Analytics的新实施。 将列出自动映射的变量 [此处](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

对于未自动映射到的XDM数据 [!DNL Adobe Analytics]，您可以使用 [上下文数据](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=zh-Hans) 与 [模式](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans). 然后，它可以映射到 [!DNL Analytics] 使用 [处理规则](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hans) 填充 [!DNL Analytics] 变量。 上下文数据和处理规则是过去与Analytics一起使用的概念，但是现在，如果它们是新概念，则无需担心详细信息。

您还可以使用一组默认的操作和产品列表，通过AEP发送或检索数据 [!DNL Web SDK]. 为此，请参阅[产品](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection)。

### 上下文数据

供使用 [!DNL Analytics]，则会使用点标记对XDM数据进行扁平化处理，并作为 `contextData`. 以下值对列表显示了 `context data` 示例：

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### 处理规则

可以通过[处理规则](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)访问边缘网络收集的所有数据。在 [!DNL Analytics]，则可以使用处理规则将上下文数据合并到 [!DNL Analytics] 变量。

## 1.5.2Experience Platform边缘网络Audience Manager

服务器端转发不是Audience Manager的新概念，与应用之前的过程相同。 您还可以同步身份。

## 1.5.3查看数据流以将数据发送到Adobe Analytics

如果要将通过Web SDK收集的数据发送到Adobe Analytics和Adobe Audience Manager，请执行以下步骤。

转到 [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) 然后转到 **数据流**.

在屏幕的右上角，选择您的沙盒名称，该名称应为 `--aepSandboxId--`. 打开您的特定数据流(名为 `--demoProfileLdap-- - Demo System Datastream`.

![单击左侧导航中的“边缘配置”图标](./images/edgeconfig1b.png)

然后你会看到这个。 要启用Adobe Analytics，请单击 **+添加服务**.

![AEP Debugger](./images/aa2.png)

然后你会看到这个。 选择服务 **Adobe Analytics**，之后，您需要在Adobe Analytics中添加报表包以将数据发送到。 在本教程中，此操作范围不广。 单击 **取消**.

![AEP Debugger](./images/aa3.png)

## 1.5.4查看数据流以将数据发送到Adobe Audience Manager

然后你会看到这个。 要启用Adobe Audience Manager，请单击 **+添加服务**.

![AEP Debugger](./images/aa2.png)

然后你会看到这个。 选择服务 **Adobe Audience Manager** 之后，您可以决定启用或禁用Adobe Audience Manager cookie目标和/或URL目标。 在本教程中，此配置不在适用范围内。 单击 **取消**.

![AEP Debugger](./images/aam1.png)

下一步： [1.6实施Adobe Target](./ex6.md)

[返回到模块1](./data-ingestion-launch-web-sdk.md)

[返回到所有模块](./../../overview.md)
