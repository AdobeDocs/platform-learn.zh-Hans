---
title: Bootcamp — 实时CDP — 构建区段并采取操作 — 将区段发送到DV360
description: Bootcamp — 实时CDP — 构建区段并采取操作 — 将区段发送到DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5采取行动：将区段发送到Facebook

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧菜单中，转到 **目标**，然后转到 **目录**. 然后您将看到 **目标目录**. 在 **目标**，单击 **激活区段** 在 **Facebook自定义受众** 卡。

![RTCDP](./images/rtcdpgoogleseg.png)

选择目标 **bootcamp-facebook** 单击 **下一个**.

![RTCDP](./images/rtcdpcreatedest2.png)

在可用区段列表中，选择在上一个练习中创建的区段。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest3.png)

在 **映射** 页面，确保 **应用转换** 复选框。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4a.png)

在 **区段计划** 页面，选择 **受众的来源** 将其设置为 **直接从客户处**. 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4.png)

最后，在 **审阅** 页面，单击 **完成**.

![RTCDP](./images/rtcdpcreatedest5.png)

您的区段现在已链接到Facebook自定义受众。 每次客户符合此区段的条件时，都会向Facebook服务器端发送一个信号，以将该客户包含在Facebook端的自定义受众中。

在Facebook中，您将在自定义受众下找到来自Adobe Experience Platform的区段：

![RTCDP](./images/rtcdpcreatedest5b.png)

您现在可以在Facebook中看到自定义受众：

![RTCDP](./images/rtcdpcreatedest5a.png)

[返回到用户流量1](./uc1.md)

[返回到所有模块](../../overview.md)
