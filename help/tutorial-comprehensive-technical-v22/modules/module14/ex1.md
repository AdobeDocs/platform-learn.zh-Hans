---
title: Adobe Experience Platform数据收集和实时事件转发端转发 — 创建Adobe Experience Platform数据收集事件转发属性
description: 创建Adobe Experience Platform数据收集事件转发属性
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2ca908a3-28b9-48d4-b96e-00951de530ba
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 14.1创建Adobe Experience Platform数据收集事件转发属性

>[!NOTE]
>
>Adobe Experience Platform Edge移动扩展当前为测试版。 此扩展的使用仅受邀。 请联系您的Adobe客户成功经理，以了解更多信息并访问本教程的材料。

## 14.1.1什么是Adobe Experience Platform数据收集事件转发属性？

通常，使用Adobe Experience Platform数据收集来收集数据时，会在 **客户端**. 的 **客户端** 是网站或移动设备应用程序等环境。 在模块0和模块1中，对Adobe Experience Platform数据收集客户端属性的配置进行了深入讨论，并且您在您的网站和移动应用程序上实施了Adobe Experience Platform数据收集客户端属性，以便当客户与网站和移动应用程序交互时，可以在该处收集数据。

当Adobe Experience Platform数据收集客户端属性收集该交互数据时，网站或移动设备应用程序会向Adobe的Edge发送请求。 边缘是Adobe的数据收集环境，是点击流数据进入Adobe生态系统的入口点。 然后，从Edge将收集的数据发送到Adobe Experience Platform、Adobe Analytics、Adobe Audience Manager或Adobe Target等应用程序。

添加了Adobe Experience Platform数据收集事件转发属性后，现在可以配置Adobe Experience Platform数据收集属性，以在Edge中侦听传入数据。 当在Edge上运行的Adobe Experience Platform数据收集事件转发属性看到传入数据时，它能够使用该数据并将其转发到其他位置。 现在，其他位置也可以是非Adobe的外部网页挂接，这样就可以将数据发送到您选择的数据湖、决策应用程序或任何能够打开网页挂接的其他应用程序。

Adobe Experience Platform数据收集事件转发属性的配置对于客户端属性来说似乎很熟悉，能够像过去使用Adobe Experience Platform数据收集客户端属性一样配置数据元素和规则。 但是，访问和使用数据的方式将因用例而略有不同。

让我们首先创建Adobe Experience Platform数据收集事件转发属性。

## 14.1.2创建Adobe Experience Platform数据收集事件转发属性

转到 [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). 在左侧菜单中，单击 **事件转发**. 然后，您将看到所有可用Adobe Experience Platform数据收集事件转发属性的概述。 单击 **新建资产** 按钮。

![Adobe Experience Platform数据收集SSF](./images/launchhome.png)

现在，您需要输入Adobe Experience Platform数据收集事件转发属性的名称。 作为命名约定，请使用 `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. 例如，在本例中，名称为 **vangeluw — 演示系统(22/02/2022)(Edge)**. 单击&#x200B;**保存**。

![Adobe Experience Platform数据收集SSF](./images/ssf1.png)

然后，您将返回到Adobe Experience Platform数据收集事件转发属性的列表。 单击以打开您刚刚创建的资产。

![Adobe Experience Platform数据收集SSF](./images/ssf2.png)

## 14.1.2配置AdobeCloud Connector扩展

在左侧菜单中，转到 **扩展**. 你会看到 **核心** 扩展已配置。

![Adobe Experience Platform数据收集SSF](./images/ssf3.png)

转到 **目录**. 您将看到 **Adobe云连接器** 扩展。 单击&#x200B;**安装**&#x200B;可安装包。

![Adobe Experience Platform数据收集SSF](./images/ssf4.png)

随后将添加该扩展。 此步骤中没有要执行的配置。 您将被发送回已安装扩展的概述。

![Adobe Experience Platform数据收集SSF](./images/ssf5.png)

## 14.1.3部署Adobe Experience Platform数据收集事件转发属性

在左侧菜单中，转到 **发布流程**. 单击 **添加库**.

![Adobe Experience Platform数据收集SSF](./images/ssf6.png)

输入名称 **主要**，选择环境 **发展（发展）** 单击 **+添加所有已更改的资源**.

![Adobe Experience Platform数据收集SSF](./images/ssf7.png)

然后你会看到这个。 单击 **Save &amp; Build for Development**.

![Adobe Experience Platform数据收集SSF](./images/ssf8.png)

随后将构建库，这可能需要1-2分钟。

![Adobe Experience Platform数据收集SSF](./images/ssf9.png)

最终，您的库将会构建并准备就绪。

![Adobe Experience Platform数据收集SSF](./images/ssf10.png)

下一步： [14.2更新数据流，以使数据可用于数据收集事件转发属性](./ex2.md)

[返回到模块14](./aep-data-collection-ssf.md)

[返回到所有模块](./../../overview.md)
