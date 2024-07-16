---
title: Bootcamp — 将物理和数字相结合 — Journey Optimizer创建您的活动
description: Bootcamp — 将物理和数字相结合 — Journey Optimizer创建您的活动
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 3d47c686-c2d8-4961-a05b-0990025392fa
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.2创建事件

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`Bootcamp`。 若要从一个沙盒更改到另一个沙盒，请单击&#x200B;**Prod**&#x200B;并从列表中选择该沙盒。 在此示例中，沙盒名为&#x200B;**Bootcamp2**。 然后，您将进入沙盒`Bootcamp`的&#x200B;**主页**&#x200B;视图。

![ACOP](./images/acoptriglp.png)

在左侧菜单中，向下滚动并单击&#x200B;**配置**。 接下来，单击&#x200B;**事件**&#x200B;下的&#x200B;**管理**&#x200B;按钮。

![ACOP](./images/acopmenu.png)

然后，您将看到所有可用事件的概述。 单击&#x200B;**创建事件**&#x200B;开始创建您自己的事件。

![ACOP](./images/emptyevent.png)

随后将弹出一个新的空事件窗口。

首先，为您的事件提供如下名称： `yourLastNameBeaconEntryEvent`并添加如下描述`Beacon Entry Event`。

![ACOP](./images/eventdescription.png)

接下来，确保&#x200B;**类型**&#x200B;设置为&#x200B;**单一**，对于&#x200B;**事件ID类型**&#x200B;选择，请选择&#x200B;**系统生成的**。

![ACOP](./images/eventidtype.png)

接下来是架构选择。 为本练习准备了一个方案。 请使用架构`Demo System - Event Schema for Mobile App (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

选择架构后，您将在&#x200B;**字段**&#x200B;部分看到许多字段正在被选择。 现在，您应该将鼠标悬停在&#x200B;**字段**&#x200B;部分上，此时您会看到3个图标弹出窗口。 单击&#x200B;**编辑**&#x200B;图标。

![ACOP](./images/eventpayload.png)

您会看到&#x200B;**字段**&#x200B;窗口弹出窗口，您需要在其中选择个性化历程所需的某些字段。  我们稍后将使用Adobe Experience Platform中已有的数据，选择其他配置文件属性。

![ACOP](./images/eventfields.png)

向下滚动直到看到对象`Place context`为止，然后选中复选框。 这样，客户所在位置的所有上下文都将可供历程使用。 单击&#x200B;**确定**&#x200B;以保存更改。

![ACOP](./images/eventpayloadbr.png)

您应该会看到此内容。 再次单击&#x200B;**保存**&#x200B;以保存更改。

![ACOP](./images/eventsave.png)

您的事件现已配置并保存。

![ACOP](./images/eventdone.png)

再次单击您的事件以再次打开&#x200B;**编辑事件**&#x200B;屏幕。 再次将鼠标悬停在&#x200B;**字段**&#x200B;上可查看3个图标。 单击&#x200B;**查看**&#x200B;图标。

![ACOP](./images/viewevent.png)

您现在将看到预期有效负载的示例。
您的事件具有独特的编排eventID，您可以通过在该有效负荷中向下滚动直至看到`_experience.campaign.orchestration.eventID`来查找该事件。

![ACOP](./images/payloadeventID.png)

事件ID是需要发送到Adobe Experience Platform的，以触发您将在下一个练习中构建的历程。 记住此eventID，因为您以后可能需要它。
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

单击&#x200B;**确定**，然后单击&#x200B;**取消**。

您现在已经完成了此练习。

下一步： [3.3创建历程和推送通知](./ex3.md)

[返回用户流程3](./uc3.md)

[返回所有模块](../../overview.md)
