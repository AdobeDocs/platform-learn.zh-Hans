---
title: Bootcamp - Journey Optimizer创建您的活动
description: Bootcamp - Journey Optimizer创建您的活动
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 2.2创建事件

登录到Adobe Journey Optimizer，方法是： [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Journey Optimizer**.

![ACOP](./images/acophome.png)

您将被重定向到 **主页**  在Journey Optimizer中查看。 首先，确保使用正确的沙盒。 调用要使用的沙盒 `Bootcamp`. 要从一个沙盒更改到另一个沙盒，请单击 **Prod** 并从列表中选择沙盒。 在此示例中，将沙盒命名为 **Bootcamp**. 然后，您将位于 **主页** 沙盒视图 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

在左侧菜单中，向下滚动并单击 **配置**. 接下来，单击 **管理** 按钮位于 **事件**.

![ACOP](./images/acopmenu.png)

然后，您将看到所有可用事件的概述。 单击 **创建事件** 以开始创建您自己的事件。

![ACOP](./images/emptyevent.png)

随后将弹出一个新的空事件窗口。

![ACOP](./images/emptyevent1.png)

首先，为您的事件提供一个名称，如下所示： `yourLastNameAccountCreationEvent` 并添加如下描述 `Account Creation Event`.

![ACOP](./images/eventdescription.png)

接下来，确保 **类型** 设置为 **单一**&#x200B;的，和 **事件ID类型** 选择，选择 **系统生成**.

![ACOP](./images/eventidtype.png)

接下来是架构选择。 为此练习准备了一个模式。 请使用架构 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

选择架构后，您将看到在 **字段** 部分。 现在，您应该将鼠标悬停在 **字段** 部分中，您将看到3个图标弹出窗口。 单击 **编辑** 图标。

![ACOP](./images/eventpayload.png)

您将看到 **字段** 窗口弹出窗口，从中需要选择我们对电子邮件进行个性化所需的某些字段。  我们稍后将使用Adobe Experience Platform中已有的数据，选择其他配置文件属性。

![ACOP](./images/eventfields.png)

在对象中 `_experienceplatform.demoEnvironment`，请确保选择字段 **brandLogo** 和 **brandName**.

![ACOP](./images/eventpayloadbr.png)

在对象中 `_experienceplatform.identification.core`，请确保选择字段 **电子邮件**.

![ACOP](./images/eventpayloadbrid.png)

单击 **确定** 以保存更改。

![ACOP](./images/saveok.png)

然后您应该会看到此内容。 单击 **保存** 再保存一次更改。

![ACOP](./images/eventsave.png)

您的事件现已配置并保存。

![ACOP](./images/eventdone.png)

再次单击您的事件以打开 **编辑事件** 再次屏幕。 将鼠标悬停在 **字段** 再次查看这3个图标。 单击 **查看有效负荷** 图标。

![ACOP](./images/viewevent.png)

您现在将看到预期有效负载的示例。
您的事件具有唯一的编排eventID，您可以通过向下滚动该有效负载中的直到看到 `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

事件ID是需要发送到Adobe Experience Platform的，以触发您将在下一个练习中构建的历程。 记住此eventID，因为您以后可能需要它。
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

单击 **确定**，然后单击 **取消**.

您现在已经完成了此练习。

下一步： [2.3创建电子邮件](./ex3.md)

[返回用户流程2](./uc2.md)

[返回所有模块](../../overview.md)
