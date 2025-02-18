---
title: Real-time CDP — 构建受众并采取行动 — 构建受众
description: Real-time CDP — 构建受众并采取行动 — 构建受众
kt: 5342
doc-type: tutorial
exl-id: fddcf394-b775-40f6-98d8-509ff9bd1c83
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 2%

---

# 2.3.1创建受众

在本练习中，您将使用Adobe Experience Platform的受众生成器来创建受众。

## 上下文

对客户兴趣的响应需要实时进行。 实时响应客户行为的一种方法是，在受众具有实时资格的情况下，使用受众。 在本练习中，您需要构建受众，同时考虑到我们一直在使用的网站上的实际活动。

## 确定您要回应的行为

转到[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登录后，您将看到此内容。 单击网站项目上的3个点&#x200B;**...**，然后单击&#x200B;**运行**&#x200B;以将其打开。

![DSN](./../../datacollection/dc1.1/images/web8.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../../../getting-started/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](../../../getting-started/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../../../getting-started/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../../../getting-started/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个练习，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](../../../getting-started/gettingstarted/images/web7.png)

在本例中，您希望对查看特定产品的特定客户做出响应。
从**Citi Signal**&#x200B;主页，转到&#x200B;**手机和设备**，然后单击产品&#x200B;**Galaxy S24**。

![数据获取](./images/homegalaxy.png)

因此，当有人访问&#x200B;**Galaxy S24**&#x200B;的产品页面时，您希望能够采取行动。 要采取行动，首先要定义受众。

![数据获取](./images/homegalaxy1.png)

## 创建受众

转到[Adobe Experience Platform](https://experience.adobe.com/platform)。 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择适当的[!UICONTROL 沙盒]后，您将看到屏幕更改，现在您已经进入专用的[!UICONTROL 沙盒]。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

在左侧的菜单中，转到&#x200B;**受众**，然后转到&#x200B;**浏览**，您可以在其中查看所有现有受众的概述。 单击&#x200B;**创建受众**&#x200B;按钮开始创建新受众。

![区段](./images/menuseg.png)

选择&#x200B;**生成规则**&#x200B;并单击&#x200B;**创建**。

![区段](./images/menuseg1.png)

如上所述，您需要从已查看产品&#x200B;**Galaxy S24**&#x200B;的所有客户中构建受众。

要构建此受众，您需要添加一个事件。 通过单击&#x200B;**受众**&#x200B;菜单栏中的&#x200B;**事件**&#x200B;图标，您可以找到所有事件。

接下来，您将看到顶级&#x200B;**XDM ExperienceEvent**&#x200B;节点。

要查找访问过&#x200B;**Galaxy S24**&#x200B;产品的客户，请单击&#x200B;**XDM ExperienceEvent**。

![区段](./images/findee.png)

向下滚动到&#x200B;**产品列表项**&#x200B;并单击它。

![区段](./images/see.png)

选择&#x200B;**Name**&#x200B;并将左侧&#x200B;**产品列表项**&#x200B;菜单中的&#x200B;**Name**&#x200B;对象拖放到受众生成器画布中的&#x200B;**事件**&#x200B;部分。

![区段](./images/eewebpdtlname1.png)

比较参数应为&#x200B;**等于**，并在输入字段中输入`Galaxy S24`。

![区段](./images/pv.png)

您的&#x200B;**事件规则**&#x200B;现在应如下所示。 每次将元素添加到受众生成器时，都可以单击&#x200B;**刷新估算**&#x200B;按钮以获取受众中群体的最新估算。

![区段](./images/ldap4.png)

为受众提供一个名称并将&#x200B;**评估方法**&#x200B;设置为&#x200B;**Edge**。

作为命名约定，请使用：

- `--aepUserLdap-- - Interest in Galaxy S24`

接下来，单击&#x200B;**发布**&#x200B;按钮以保存受众。

![区段](./images/segmentname.png)

此时您将返回到受众概述页面。

![区段](./images/savedsegment.png)

## 后续步骤

转到[2.3.2查看如何使用目标](./ex2.md){target="_blank"}配置DV360目标

返回[Real-time CDP — 构建受众并执行操作](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
