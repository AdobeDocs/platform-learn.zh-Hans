---
title: Bootcamp — 混合物理和数字 — Journey Optimizer创建活动 — 巴西
description: Bootcamp — 混合物理和数字 — Journey Optimizer创建活动 — 巴西
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 3.2创建事件

通过转到Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Journey Optimizer**.

![ACOP](./images/acophome.png)

您将被重定向到 **主页**  查看Journey Optimizer。 首先，确保您使用的是正确的沙盒。 要使用的沙盒称为 `Bootcamp`. 要从一个沙盒更改为另一个沙盒，请单击 **生产** 并从列表中选择沙盒。 在此示例中，沙盒名为 **Bootcamp2**. 然后你会在 **主页** 沙盒视图 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

在左侧菜单中，向下滚动并单击 **配置**. 接下来，单击 **管理** 按钮 **事件**.

![ACOP](./images/acopmenu.png)

然后，您将看到所有可用事件的概述。 单击 **创建事件** 以开始创建您自己的事件。

![ACOP](./images/emptyevent.png)

随后将弹出一个新的空事件窗口。

首先，为您的事件指定如下名称： `yourLastNameBeaconEntryEvent` 并添加如下描述 `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

接下来，确保 **类型** 设置为 **单一**、和 **事件ID类型** 选择，选择 **系统生成**.

![ACOP](./images/eventidtype.png)

接下来是架构选择。 为本练习准备了一个模式。 请使用架构 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

选择架构后，您将在 **字段** 中。 现在，您应将鼠标悬停在 **字段** 部分，您将看到3个图标弹出窗口。 单击 **编辑** 图标。

![ACOP](./images/eventpayload.png)

你会看到 **字段** 窗口弹出窗口，您需要在其中选择一些需要个性化历程的字段。  我们稍后将使用Adobe Experience Platform中已有的数据选择其他配置文件属性。

![ACOP](./images/eventfields.png)

向下滚动直到看到对象为止 `Place context` 并选中复选框。 借助此，客户位置的所有上下文都将可用于历程。 单击 **确定** 以保存更改。

![ACOP](./images/eventpayloadbr.png)

然后你应该看到这个。 单击 **保存** 再次保存更改。

![ACOP](./images/eventsave.png)

您的事件现已配置并保存。

![ACOP](./images/eventdone.png)

再次单击您的事件以打开 **编辑事件** 屏幕。 将鼠标悬停在 **字段** 再次查看这3个图标。 单击 **查看** 图标。

![ACOP](./images/viewevent.png)

您现在将看到预期有效负载的示例。
您的事件具有唯一的编排事件ID，您可以通过在该有效负载中向下滚动直到您看到为止，来查找该事件 `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

事件ID是需要发送到Adobe Experience Platform的内容，以便触发将在接下来的练习之一中构建的历程。 请记住此eventID，因为您以后可能需要它。
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

单击 **确定**，然后单击 **取消**.

你现在已经完成了这个练习。

下一步： [3.3创建历程和推送通知](./ex3.md)

[返回到用户流量3](./uc3.md)

[返回到所有模块](../../overview.md)
