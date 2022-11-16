---
title: Real-time CDP — 构建区段并采取操作 — 将区段发送到DV360
description: Real-time CDP — 构建区段并采取操作 — 将区段发送到DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7a78260f-cd25-4ed0-801b-87174babaffe
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# 6.3采取行动：将区段发送到DV360

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](../module2/images/sb1.png)

在左侧菜单中，转到 **目标**，然后转到 **目录**. 然后您将看到 **目标目录**.

![RTCDP](./images/rtcdpmenudest.png)

在 **目标**，请单击 **激活区段** 在 **Google显示与视频360** 卡。

![RTCDP](./images/rtcdpgoogleseg.png)

选择您的目标并单击 **下一个**.

![RTCDP](./images/rtcdpcreatedest2.png)

在可用区段列表中，选择在上一个练习中创建的区段。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest3.png)

在 **区段计划** 页面，单击 **下一个**.

![RTCDP](./images/rtcdpcreatedest4.png)

最后，在 **审阅** 页面，单击 **完成**.

![RTCDP](./images/rtcdpcreatedest5.png)

您的区段现在已链接到Google DV360。 每次客户符合此区段的条件时，都会向Google DV360发送一个信号，以将该客户包含在Google DV360端的受众中。

下一步： [6.4采取行动：将区段发送到S3目标](./ex4.md)

[返回到模块6](./real-time-cdp-build-a-segment-take-action.md)

[返回到所有模块](../../overview.md)
