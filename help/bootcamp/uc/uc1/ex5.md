---
title: Bootcamp - Real-time CDP — 构建受众并采取行动 — 将受众发送至DV360
description: Bootcamp - Real-time CDP — 构建受众并采取行动 — 将受众发送至DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5操作：将受众发送到Facebook

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击文本来执行此操作 **[!UICONTROL 生产生产]** 在屏幕顶部的蓝线上。 选择适当的 [!UICONTROL 沙盒]，您将会看到屏幕更改，现在您已进入专用页面 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

在左侧菜单中，转到 **目标**，然后转到 **目录**. 您随后将看到 **目标目录**. 在 **目标**，单击 **激活受众** 在 **facebook自定义受众** 卡片。

![RTCDP](./images/rtcdpgoogleseg.png)

选择目标 **bootcamp-facebook** 并单击 **下一个**.

![RTCDP](./images/rtcdpcreatedest2.png)

在可用受众列表中，选择您在上一个练习中创建的受众。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest3.png)

在 **映射** 页面，确保 **应用转换** 复选框已启用。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4a.png)

在 **受众计划** 页面上，选择 **受众来源** 并将其设置为 **直接来自客户**. 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4.png)

最后，在 **审核** 页面，单击 **完成**.

![RTCDP](./images/rtcdpcreatedest5.png)

现在，您的受众已链接到Facebook自定义受众。 每次有客户符合此受众的资格条件时，都会向Facebook服务器端发送一个信号，将该客户包含在Facebook端的自定义受众中。

在Facebook中，您可以在自定义受众下找到来自Adobe Experience Platform的受众：

![RTCDP](./images/rtcdpcreatedest5b.png)

您现在可以看到您的自定义受众显示在Facebook中：

![RTCDP](./images/rtcdpcreatedest5a.png)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
