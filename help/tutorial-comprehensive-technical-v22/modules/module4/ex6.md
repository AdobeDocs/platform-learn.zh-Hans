---
title: 查询服务 — 使用Tableau浏览数据集
description: 查询服务 — 使用Tableau浏览数据集
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 04209eb4-b054-4a2e-885e-61f601c3fc2c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 4.6查询服务和表格

打开表格。

![start-tableau.png](./images/start-tableau.png)

在 **连接到服务器** 选择 **PostgreSQL**:

![tableau-connect-postogress.png](./images/tableau-connect-postgress.png)

转到Adobe Experience Platform, **查询** 和 **凭据**.

![query-service-credentials.png](./images/query-service-credentials.png)

从 **凭据** 页面，复制 **主机** 然后粘贴到 **服务器** 字段，复制 **数据库** 然后粘贴到 **数据库** 字段，请复制 **端口** 并粘贴到字段中 **端口**&#x200B;在表格中，为 **用户名** 和 **密码**. 接下来，单击 **登录**.

登录：

![tableau-connection-dialog-png](./images/tableau-connection-dialog.png)

单击搜索(1)，然后输入 **ldap** 在搜索字段中，从结果集中标识您的表，然后将其拖动(3)到名为的位置 **将表格拖动到此处**. 完成后，单击 **表1** (3)。

![tableau-drag-table.png](./images/tableau-drag-table.png)

要在地图上可视化我们的数据，我们需要将经度和纬度转换为维度。 在 **措施** 选择 **纬度** (1)并打开字段的下拉菜单，然后选择 **转换为Dimension** (2)。 为 **经度** 度量。

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

拖动 **经度** 度量 **列** 和 **纬度** 衡量 **行**. 自动映射 **比利时** 将显示一些小圆点，这些小圆点表示数据集中的城市。

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

选择 **度量名称** (1)，打开下拉菜单并选择 **添加到工作表** （二）：

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

您现在将拥有一张地图，其中包含各种大小的点。 大小表示该特定城市呼叫中心交互的数量。 要更改点的大小，请导航到右侧面板并打开 **测量值** （使用下拉图标）。 从下拉列表中，选择 **编辑大小**. 用不同大小玩。

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

进一步显示 **调用主题**，拖动(1) **调用主题** 维度 **页面**. 在不同的 **调用主题** 使用 **调用主题** (2)屏幕右侧：

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

你现在已经完成了这个练习。

下一步： [4.7查询服务API](./ex7.md)

[返回到模块4](./query-service.md)

[返回到所有模块](../../overview.md)
