---
title: Real-time CDP — 构建受众并采取行动 — 将受众发送至DV360
description: Real-time CDP — 构建受众并采取行动 — 将受众发送至DV360
kt: 5342
doc-type: tutorial
exl-id: bb76524e-52c1-4c2c-8bcd-33cd39d12741
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 1%

---

# 2.3.3采取行动：将您的受众发送至DV360

转到[Adobe Experience Platform](https://experience.adobe.com/platform)。 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../modules/datacollection/module1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择适当的[!UICONTROL 沙盒]后，您将看到屏幕更改，现在您已经进入专用的[!UICONTROL 沙盒]。

![数据获取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左侧菜单中，转到&#x200B;**目标**，然后转到&#x200B;**浏览**。 您随后将看到&#x200B;**DV360**&#x200B;目标。 单击3个圆点&#x200B;**...**，然后单击&#x200B;**激活受众**。

![RTCDP](./images/rtcdpmenudest.png)

在可用受众列表中，选择您在上一个练习中创建的受众。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest3.png)

在&#x200B;**受众计划**&#x200B;页面上，单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4.png)

最后，在&#x200B;**审核**&#x200B;页面上单击&#x200B;**完成**。

![RTCDP](./images/rtcdpcreatedest5.png)

现在，您的受众已链接到Google DV360。 每次有客户符合此受众的资格条件时，系统都会向Google DV360发送一个信号，以便将该客户包含在Google DV360端的受众中。

下一步： [2.3.4执行操作：将受众发送到S3-destination](./ex4.md)

[返回模块2.3](./real-time-cdp-build-a-segment-take-action.md)

[返回所有模块](../../../overview.md)
