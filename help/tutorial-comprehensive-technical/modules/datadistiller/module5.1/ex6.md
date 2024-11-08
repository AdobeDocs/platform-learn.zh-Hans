---
title: 查询服务 — 使用Tableau浏览数据集
description: 查询服务 — 使用Tableau浏览数据集
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.6查询服务和Tableau

打开Tableau。

![start-tableau.png](./images/start-tableau.png)

在&#x200B;**连接到服务器**&#x200B;中，选择&#x200B;**PostgreSQL**：

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

转到Adobe Experience Platform、**查询**&#x200B;和&#x200B;**凭据**。

![query-service-credentials.png](./images/query-service-credentials.png)

从Adobe Experience Platform的&#x200B;**凭据**&#x200B;页中，复制&#x200B;**主机**&#x200B;并将其粘贴到&#x200B;**服务器**&#x200B;字段中，复制&#x200B;**数据库**&#x200B;并将其粘贴到Tableau中的&#x200B;**数据库**&#x200B;字段中，复制&#x200B;**端口**&#x200B;并将其粘贴到Tableau中的&#x200B;**端口**&#x200B;字段中，对&#x200B;**用户名**&#x200B;和&#x200B;**密码**&#x200B;执行相同的操作。 接下来，单击&#x200B;**登录**。

登录：

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

单击搜索(1)并在搜索字段中输入您的&#x200B;**ldap**，从结果集中识别您的表并将其拖到名为&#x200B;**将表拖到此处**&#x200B;的位置。 完成后，单击&#x200B;**表1** (3)。

![tableau-drag-table.png](./images/tableau-drag-table.png)

要在地图上可视化我们的数据，我们需要将经度和纬度转换为维度。 在&#x200B;**度量**&#x200B;中，选择&#x200B;**纬度** (1)，然后打开该字段的下拉列表，并选择&#x200B;**转换为Dimension** (2)。 对&#x200B;**经度**&#x200B;度量值执行相同操作。

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

将&#x200B;**Longitude**&#x200B;度量值拖动到&#x200B;**列**，将&#x200B;**纬度**&#x200B;度量值拖动到&#x200B;**行**。 **Belgium**&#x200B;的地图将自动显示，其中带有代表数据集中的城市的小点。

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

选择&#x200B;**度量值名称** (1)，打开下拉菜单并选择&#x200B;**添加到工作表** (2)：

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

您现在将拥有包含各种大小点的地图。 该大小表示特定城市的呼叫中心互动次数。 若要改变点的大小，请导航到右侧面板并打开&#x200B;**度量值**（使用下拉图标）。 从下拉列表中选择&#x200B;**编辑大小**。 玩不同大小的游戏。

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

若要进一步显示每个&#x200B;**调用主题**&#x200B;的数据，请将(1) **调用主题**&#x200B;维度拖到&#x200B;**页**&#x200B;上。 使用屏幕右侧的&#x200B;**呼叫主题** (2)浏览不同的&#x200B;**呼叫主题**：

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

您现在已经完成了此练习。

下一步： [5.1.7查询服务API](./ex7.md)

[返回模块5.1](./query-service.md)

[返回所有模块](../../../overview.md)
