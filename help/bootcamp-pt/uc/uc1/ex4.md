---
title: Bootcamp — 实时CDP — 构建区段并采取操作 — 将您的区段发送到Adobe Target — 巴西
description: Bootcamp — 实时CDP — 构建区段并采取操作 — 将您的区段发送到Adobe Target — 巴西
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 1%

---

# 1.4采取行动：将区段发送到Adobe Target

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

## 1.4.1激活您的区段到Adobe Target目标

Adobe Target可作为Real-Time CDP的目的地。 要设置Adobe Target集成，请转到 **目标**，更改为 **目录**.

单击 **个性化** 在 **类别** 菜单。 然后您将看到 **Adobe Target** 目标卡。 单击 **激活区段**.

![AT](./images/atdest1.png)

选择目标 ``Bootcamp Target`` 单击 **下一个**.

![AT](./images/atdest3.png)

在可用区段列表中，选择您在中创建的区段 [1.3创建区段](./ex3.md)，该名称为 `yourLastName - Interest in Real-Time CDP`. 然后，单击 **下一个**.

![AT](./images/atdest8.png)

在下一页，单击 **下一个**.

![AT](./images/atdest9.png)

单击&#x200B;**完成**。

![AT](./images/atdest10.png)

您的区段现在已激活到Adobe Target。

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>当您刚在Real-Time CDP中创建了Adobe Target目标后，该目标可能需要长达一小时才能正式启用。 由于设置了后端配置，这是一次性等待时间。 完成初始1小时等待时间和后端配置后，发送到Adobe Target目标的新添加的边缘区段将可用于实时定位。

## 1.4.2配置Adobe Target基于表单的活动

现在，您的Real-Time CDP区段已配置为发送到Adobe Target，接下来可以在Adobe Target中配置体验定位活动。 在本练习中，您将配置一个基于可视化体验编辑器的活动。

转到Adobe Experience Cloud主页 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 单击 **Target** 打开它。

![RTCDP](./images/excl.png)

在 **Adobe Target** 主页，您将看到所有现有活动。
单击 **+创建活动** 创建新活动。

![RTCDP](./images/exclatov.png)

选择 **体验定位**.

![RTCDP](./images/exclatcrxt.png)

选择 **可视** 并设置 **活动URL** to `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`，但在执行此操作之前，请将XX替换为01到30之间的数字。

>[!IMPORTANT]
>
>启用的每位参与者都应使用单独的网页，以避免各种Adobe Target体验发生冲突。 您可以选择网页并通过转到此处查找URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>所有页面都共享相同的基本URL，并以参与者人数结尾。
>
>例如，参与者1应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，参与者30应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

选择工作区 **AT Bootcamp**.

单击&#x200B;**下一步**。

![RTCDP](./images/exclatcrxtdtlform.png)

您现在可以使用可视化体验编辑器。 网站完全加载之前，可能需要20-30秒。

![RTCDP](./images/atform1.png)

默认受众当前为 **所有访客**. 单击 **3点** 下一页 **所有访客** 单击 **更改受众**.

![RTCDP](./images/atform3.png)

现在，您会看到可用受众的列表，之前创建并发送到Adobe Target的Adobe Experience Platform区段现在已包含在此列表中。 选择您之前在Adobe Experience Platform中创建的区段。 单击 **分配受众**.

![RTCDP](./images/exclatvecchaud.png)

您的Adobe Experience Platform区段现在是此体验定位活动的一部分。

![RTCDP](./images/atform4.png)

在更改主页图像之前，您需要单击 **允许全部** 在cookie横幅上。

要执行此操作，请转到 **浏览**

![RTCDP](./images/cook1.png)

接下来，单击 **允许全部**.

![RTCDP](./images/cook2.png)

接下来，返回 **撰写**.

![RTCDP](./images/cook3.png)

现在，让我们更改网站主页上的主页图像。 单击网站上的默认主页图像，然后单击 **替换内容** 然后选择 **图像**.

![RTCDP](./images/atform5.png)

搜索图像文件 **rtcdp.png**. 选择它，然后单击 **保存**.

![RTCDP](./images/atform6.png)

然后，您将看到所选受众的新体验以及新图像。

![RTCDP](./images/atform7.png)

单击左上角活动的标题以对其重命名。

![RTCDP](./images/exclatvecname.png)

对于名称，请使用：

- `yourLastName - RTCDP - XT (VEC)`

单击&#x200B;**下一步**。

![RTCDP](./images/atform8.png)

单击&#x200B;**下一步**。

![RTCDP](./images/atform8a.png)

在 **目标和设置**  — 页面，转到 **目标量度**.

![RTCDP](./images/atform9.png)

将主要目标设置为 **参与度** - **网站逗留时间**. 单击“**保存并关闭**”。

![RTCDP](./images/vec3.png)

你现在在 **活动概述** 页面。 您仍需要激活活动。

![RTCDP](./images/atform10.png)

单击字段 **不活动** 选择 **激活**.

![RTCDP](./images/atform11.png)

然后，您会收到一则可视确认消息，确认您的活动现已启动。

![RTCDP](./images/atform12.png)

您的活动现已上线，可在bootcamp网站上进行测试。

如果您现在返回演示网站并访问 **Real-Time CDP**，您随后将立即有资格访问您创建的区段，并且您将看到Adobe Target活动实时显示在主页上。

>[!IMPORTANT]
>
>启用的每位参与者都应使用单独的网页，以避免各种Adobe Target体验发生冲突。 您可以选择网页并通过转到此处查找URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>所有页面都共享相同的基本URL，并以参与者人数结尾。
>
>例如，参与者1应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，参与者30应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

下一步： [1.5采取行动：将区段发送到Facebook](./ex5.md)

[返回到用户流量1](./uc1.md)

[返回到所有模块](../../overview.md)
