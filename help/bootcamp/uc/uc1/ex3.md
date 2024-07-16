---
title: Bootcamp — 实时客户个人资料 — 创建受众 — UI
description: Bootcamp — 实时客户个人资料 — 创建受众 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3创建受众 — UI

在本练习中，您将使用Adobe Experience Platform的Audience Builder创建一个受众。

## Story

转到[Adobe Experience Platform](https://experience.adobe.com/platform)。 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``Bootcamp``。 您可以通过单击屏幕顶部蓝线中的文本&#x200B;**[!UICONTROL Production Prod]**&#x200B;来执行此操作。 选择适当的[!UICONTROL 沙盒]后，您将看到屏幕更改，现在您已经进入专用的[!UICONTROL 沙盒]。

![数据获取](./images/sb1.png)

在左侧的菜单中，转到&#x200B;**受众**。 在此页面上，您将看到包含有关&#x200B;**受众**&#x200B;性能的基本信息的功能板。

![区段](./images/menuseg.png)

单击&#x200B;**浏览**&#x200B;查看所有现有受众的概述。 单击&#x200B;**+创建受众**&#x200B;按钮开始创建新受众。


![区段](./images/segmentationui.png)

将出现一个弹出窗口，询问您是要&#x200B;**&#39;组合受众&#39;**，还是&#x200B;**&#39;生成规则&#39;**。 选择&#x200B;**“生成规则”**&#x200B;以继续，然后单击&#x200B;**创建**。

![区段][def]

进入受众生成器后，您会立即注意到&#x200B;**Attributes**&#x200B;菜单选项和&#x200B;**XDM个人资料**&#x200B;引用。


由于XDM是支持体验业务的语言，因此XDM也是受众生成器的基础。 在Platform中引入的所有数据都应根据XDM进行映射，因此，无论数据来自何处，所有数据都会成为同一数据模型的一部分。 这为您在构建受众时提供了很大的优势，因为从这个受众生成器UI中，您可以在同一个工作流中组合来自任何来源的数据。 在Audience Builder中构建的受众可以发送到Adobe Target、Adobe Campaign或任何其他激活渠道等解决方案。

您现在需要创建查看了产品&#x200B;**Real-Time CDP**&#x200B;的所有客户的受众。

要构建此受众，您需要添加一个体验事件。 单击&#x200B;**字段**&#x200B;菜单栏中的&#x200B;**事件**&#x200B;图标可找到所有Experience Events。

![区段](./images/findee.png)

接下来，您将看到顶级&#x200B;**XDM ExperienceEvents**&#x200B;节点。 单击&#x200B;**XDM ExperienceEvent**。

![区段](./images/see.png)

转到&#x200B;**产品列表项**。

![区段](./images/plitems.png)

选择&#x200B;**Name**&#x200B;并从左侧菜单将&#x200B;**Name**&#x200B;对象拖放到受众生成器画布上的&#x200B;**事件**&#x200B;部分。 您随后将看到以下内容：

![区段](./images/eewebpdtlname.png)

比较参数应为&#x200B;**等于**，并在输入字段中输入&#x200B;**实时CDP**。

![区段](./images/pv.png)

每次将元素添加到受众生成器时，都可以单击&#x200B;**刷新估算**&#x200B;按钮以获取受众中群体的最新估算。

![区段](./images/refreshest.png)

作为&#x200B;**评估方法**，请选择&#x200B;**Edge**。

![区段](./images/evedge.png)

最后，让我们为您的受众提供一个名称并保存它。

作为命名约定，请使用：

- `yourLastName - Interest in Real-Time CDP`

然后，单击&#x200B;**保存并关闭**&#x200B;按钮以保存受众。

![区段](./images/segmentname.png)

您将立即返回受众概述页面，在那里您将看到符合受众条件的客户个人资料的示例预览。

![区段](./images/savedsegment.png)

您现在可以继续下一个练习，并将您的受众与Adobe Target结合使用。

下一步： [1.4操作：将受众发送到Adobe Target](./ex4.md)

[返回用户流程1](./uc1.md)

[返回所有模块](../../overview.md)


[def]: ./images/segmentationpopup.png
