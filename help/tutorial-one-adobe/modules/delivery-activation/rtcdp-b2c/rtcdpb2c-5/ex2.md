---
title: Adobe Experience Platform数据收集和实时服务器端转发 — 更新您的数据流，使数据可用于您的Adobe Experience Platform数据收集服务器资产
description: 更新您的数据流以使数据可用于您的Adobe Experience Platform数据收集服务器资产
kt: 5342
doc-type: tutorial
exl-id: f4bb0673-d553-4027-8bfd-53d2608efaf5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# 2.5.2更新您的数据流以使数据可用于您的Adobe Experience Platform数据收集服务器资产

## 更新您的数据流

在[快速入门](./../../../getting-started/gettingstarted/ex2.md)中，您创建了自己的&#x200B;**[!UICONTROL 数据流]**。 您随后使用了名称`--aepUserLdap-- - Demo System Datastream`。

在本练习中，您需要配置该&#x200B;**[!UICONTROL 数据流]**&#x200B;以使用您的&#x200B;**数据收集服务器属性**。

为此，请转到[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。 你会看到这个。 在左侧菜单中，单击&#x200B;**[!UICONTROL 数据流]**。

在屏幕右上角，选择沙盒名称，应为`--aepSandboxName--`。

![单击左侧导航栏中的“Edge配置”图标](./images/edgeconfig1b.png)

搜索名为`--aepUserLdap-- - Demo System Datastream`的&#x200B;**[!UICONTROL 数据流]**。 单击您的&#x200B;**[!UICONTROL 数据流]**&#x200B;以将其打开。

![WebSDK](./images/websdk0.png)

你会看到这个。 单击&#x200B;**[!UICONTROL +添加服务]**。

![WebSDK](./images/websdk3.png)

选择服务&#x200B;**事件转发**。 这将向您显示2个其他设置。 选择您在上一个练习中创建的、名为`--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`的事件转发属性。 然后选择&#x200B;**环境**&#x200B;下的&#x200B;**开发**。 单击&#x200B;**保存**。

![WebSDK](./images/websdk4.png)

您的数据流现已更新并可供使用。

![WebSDK](./images/websdk8a.png)

您的数据流现在已准备好与您的&#x200B;**[!DNL Event Forwarding property]**&#x200B;一起使用。

## 后续步骤

转到[2.5.3创建并配置自定义webhook](./ex3.md){target="_blank"}

返回[Real-Time CDP连接：事件转发](./aep-data-collection-ssf.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
