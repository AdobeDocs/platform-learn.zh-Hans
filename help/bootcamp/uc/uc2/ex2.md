---
title: Bootcamp - Journey Optimizer创建事件
description: Bootcamp - Journey Optimizer创建事件
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 2.2创建事件

通过转到Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Journey Optimizer**.

![ACOP](./images/acophome.png)

您将被重定向到 **主页**  查看Journey Optimizer。 首先，确保您使用的是正确的沙盒。 要使用的沙盒称为 `Bootcamp`. 要从一个沙盒更改为另一个沙盒，请单击 **生产** 并从列表中选择沙盒。 在此示例中，沙盒名为 **Bootcamp**. 然后你会在 **主页** 沙盒视图 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

在左侧菜单中，向下滚动并单击 **配置**. 接下来，单击 **管理** 按钮 **事件**.

![ACOP](./images/acopmenu.png)

然后，您将看到所有可用事件的概述。 单击 **创建事件** 以开始创建您自己的事件。

![ACOP](./images/emptyevent.png)

随后将弹出一个新的空事件窗口。

![ACOP](./images/emptyevent1.png)

首先，为您的事件指定如下名称： `yourLastNameAccountCreationEvent` 并添加如下描述 `Account Creation Event`.

![ACOP](./images/eventdescription.png)

接下来，确保 **类型** 设置为 **单一**、和 **事件ID类型** 选择，选择 **系统生成**.

![ACOP](./images/eventidtype.png)

接下来是架构选择。 为本练习准备了一个模式。 请使用架构 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

选择架构后，您将在 **字段** 中。 现在，您应将鼠标悬停在 **字段** 部分，您将看到3个图标弹出窗口。 单击 **编辑** 图标。

![ACOP](./images/eventpayload.png)

你会看到 **字段** 窗口弹出窗口，您需要在其中选择一些个性化电子邮件所需的字段。  我们稍后将使用Adobe Experience Platform中已有的数据选择其他配置文件属性。

![ACOP](./images/eventfields.png)

在对象中 `_experienceplatform.demoEnvironment`，请确保选择字段 **brandLogo** 和 **brandName**.

![ACOP](./images/eventpayloadbr.png)

在对象中 `_experienceplatform.identification.core`，请确保选择字段 **电子邮件**.

![ACOP](./images/eventpayloadbrid.png)

单击 **确定** 以保存更改。

![ACOP](./images/saveok.png)

然后你应该看到这个。 单击 **保存** 再次保存更改。

![ACOP](./images/eventsave.png)

您的事件现已配置并保存。

![ACOP](./images/eventdone.png)

再次单击您的事件以打开 **编辑事件** 屏幕。 将鼠标悬停在 **字段** 再次查看3个图标。 单击 **查看有效负载** 图标。

![ACOP](./images/viewevent.png)

您现在将看到预期有效负载的示例。
您的事件具有唯一的编排事件ID，您可以通过在该有效负载中向下滚动直到您看到为止，来查找该事件 `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

事件ID是需要发送到Adobe Experience Platform的内容，以便触发将在接下来的练习之一中构建的历程。 请记住此eventID，因为您以后可能需要它。
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

单击 **确定**，然后单击 **取消**.

你现在已经完成了这个练习。

下一步： [2.3创建电子邮件](./ex3.md)

[返回到用户流量2](./uc2.md)

[返回到所有模块](../../overview.md)
