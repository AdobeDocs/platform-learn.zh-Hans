---
title: Bootcamp - Real-time CDP — 构建区段并采取行动 — 将区段发送到Adobe Target
description: Bootcamp - Real-time CDP — 构建区段并采取行动 — 将区段发送到Adobe Target
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---

# 1.4采取行动：将您的区段发送到Adobe Target

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``Bootcamp``. 您可以通过单击文本来执行此操作 **[!UICONTROL 生产产品]** 在屏幕顶部的蓝线上。 选择适当的 [!UICONTROL 沙盒]，您会看到屏幕更改，现在您已专心致志地工作 [!UICONTROL 沙盒].

![数据获取](./images/sb1.png)

## 1.4.1将区段激活到Adobe Target目标

Adobe Target可作为Real-Time CDP中的目标。 要设置Adobe Target集成，请转到 **目标**，至 **目录**.

单击 **个性化** 在 **类别** 菜单。 然后您将会看到 **Adobe Target** 目标卡。 单击 **激活区段**.

![在](./images/atdest1.png)

选择目标 ``Bootcamp Target`` 并单击 **下一个**.

![在](./images/atdest3.png)

在可用区段列表中，选择您在中创建的区段 [1.3创建区段](./ex3.md)，已命名 `yourLastName - Interest in Real-Time CDP`. 然后，单击 **下一个**.

![在](./images/atdest8.png)

在下一页，单击 **下一个**.

![在](./images/atdest9.png)

单击&#x200B;**完成**。

![在](./images/atdest10.png)

您的区段现在已激活到Adobe Target。

![在](./images/atdest11.png)

>[!IMPORTANT]
>
>当您刚刚在Real-Time CDP中创建Adobe Target目标时，该目标可能最多需要一小时的时间来启用。 由于后端配置的设置，这是一个一次性等待时间。 完成初始1小时的等待时间和后端配置后，发送到Adobe Target目标的新添加的边缘区段将可用于实时定位。

## 1.4.2配置基于Adobe Target表单的活动

现在，您的Real-Time CDP区段已配置为发送到Adobe Target，您可以在Adobe Target中配置体验定位活动。 在本练习中，您将配置一个基于可视化体验编辑器的活动。

转到Adobe Experience Cloud主页，然后转到 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 单击 **Target** 打开它。

![RTCDP](./images/excl.png)

在 **Adobe Target** 在主页上，您将看到所有现有活动。
单击 **+创建活动** 以创建新活动。

![RTCDP](./images/exclatov.png)

选择 **体验定位**.

![RTCDP](./images/exclatcrxt.png)

选择 **可视化** 并设置 **活动URL** 到 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`，但在执行此操作之前，请将XX替换为介于01和30之间的数字。

>[!IMPORTANT]
>
>每个参与启用的人都应该使用单独的网页，以避免各种Adobe Target体验发生冲突。 您可以通过转到以下位置来选择网页并查找URL： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>所有页面共享相同的基本URL，并以参与者的数量结尾。
>
>例如，参与者1应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，参与者30应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

选择工作区 **AT Bootcamp**.

单击&#x200B;**下一步**。

![RTCDP](./images/exclatcrxtdtlform.png)

您现在位于可视化体验编辑器中。 网站完全加载可能需要20-30秒。

![RTCDP](./images/atform1.png)

默认受众当前为 **所有访客**. 单击 **3个点** 旁边 **所有访客** 并单击 **更改受众**.

![RTCDP](./images/atform3.png)

您现在可以看到可用受众的列表，而您之前创建并发送到Adobe Target的Adobe Experience Platform区段现在包含在此列表中。 选择您之前在Adobe Experience Platform中创建的区段。 单击 **分配受众**.

![RTCDP](./images/exclatvecchaud.png)

您的Adobe Experience Platform区段现已加入此体验定位活动。

![RTCDP](./images/atform4.png)

在更改主页图像之前，您需要单击 **全部允许** 在Cookie横幅上。

要执行此操作，请转到 **浏览**

![RTCDP](./images/cook1.png)

接下来，单击 **全部允许**.

![RTCDP](./images/cook2.png)

接下来，返回到 **撰写**.

![RTCDP](./images/cook3.png)

现在，让我们更改网站主页上的主页图像。 单击网站上的默认主页图像，然后单击 **替换内容** 然后选择 **图像**.

![RTCDP](./images/atform5.png)

搜索图像文件 **rtcdp.png**. 选择它，然后单击 **保存**.

![RTCDP](./images/atform6.png)

然后，您将看到所选受众的新图像体验。

![RTCDP](./images/atform7.png)

单击左上角的活动标题可为其重命名。

![RTCDP](./images/exclatvecname.png)

对于名称，请使用：

- `yourLastName - RTCDP - XT (VEC)`

单击&#x200B;**下一步**。

![RTCDP](./images/atform8.png)

单击&#x200B;**下一步**。

![RTCDP](./images/atform8a.png)

在 **目标和设置**  — 页面，转到 **目标量度**.

![RTCDP](./images/atform9.png)

将主要目标设置为 **参与** - **Time On Site**. 单击“**保存并关闭**”。

![RTCDP](./images/vec3.png)

您现在位于 **活动概述** 页面。 您仍需要激活活动。

![RTCDP](./images/atform10.png)

单击字段 **不活动** 并选择 **激活**.

![RTCDP](./images/atform11.png)

然后，您将获得一条可视化确认消息，确认您的活动现已上线。

![RTCDP](./images/atform12.png)

您的活动现已上线，可以在bootcamp网站上进行测试。

如果您现在返回演示网站，并访问的产品页面 **Real-Time CDP**，您将立即获得所创建区段的资格，并且您将看到Adobe Target活动实时显示在主页上。

>[!IMPORTANT]
>
>每个参与启用的人都应该使用单独的网页，以避免各种Adobe Target体验发生冲突。 您可以通过转到以下位置来选择网页并查找URL： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>所有页面共享相同的基本URL，并以参与者的数量结尾。
>
>例如，参与者1应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，参与者30应使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

下一步： [1.5采取行动：将您的区段发送到Facebook](./ex5.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)
