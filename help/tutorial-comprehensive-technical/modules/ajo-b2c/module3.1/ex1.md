---
title: Journey Optimizer创建您的活动
description: Journey Optimizer创建您的活动
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.1.1创建事件

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 若要从一个沙盒更改到另一个沙盒，请单击&#x200B;**PRODUCTION Prod (VA7)**，然后从列表中选择该沙盒。 在此示例中，沙盒名为&#x200B;**AEP Enablement FY22**。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./images/acoptriglp.png)

在左侧菜单中，向下滚动并单击&#x200B;**配置**。 接下来，单击&#x200B;**事件**&#x200B;下的&#x200B;**管理**&#x200B;按钮。

![ACOP](./images/acopmenu.png)

然后，您将看到所有可用事件的概述。 单击&#x200B;**创建事件**&#x200B;开始创建您自己的事件。

![ACOP](./images/emptyevent.png)

随后将弹出一个新的空事件窗口。

![ACOP](./images/emptyevent1.png)

首先，为您的事件提供一个名称，如下所示： `--aepUserLdap--AccountCreationEvent`。

![ACOP](./images/eventname.png)

接下来，添加类似于此`Account Creation Event`的说明。

![ACOP](./images/eventdescription.png)

接下来，确保&#x200B;**类型**&#x200B;设置为&#x200B;**单一**，对于&#x200B;**事件ID类型**&#x200B;选择，请选择&#x200B;**系统生成的**。

![ACOP](./images/eventidtype.png)

接下来是架构选择。 为本练习准备了一个方案。 请使用架构`Demo System - Event Schema for Website (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

选择架构后，您将在&#x200B;**有效负载**&#x200B;部分看到许多字段正在被选择。 现在，您应该将鼠标悬停在&#x200B;**有效负荷**&#x200B;部分上，此时您将看到3个图标弹出窗口。 单击&#x200B;**编辑**&#x200B;图标。

![ACOP](./images/eventpayload.png)

您会看到&#x200B;**字段**&#x200B;窗口弹出窗口，您需要在该窗口中选择个性化电子邮件所需的某些字段。  我们稍后将使用Adobe Experience Platform中已有的数据，选择其他配置文件属性。

![ACOP](./images/eventfields.png)

在对象`--aepTenantId--.demoEnvironment`中，请确保选择字段&#x200B;**brandLogo**&#x200B;和&#x200B;**brandName**。

![ACOP](./images/eventpayloadbr.png)

在对象`--aepTenantId--.identification.core`中，请确保选择字段&#x200B;**电子邮件**。

![ACOP](./images/eventpayloadbrid.png)

单击&#x200B;**确定**&#x200B;以保存更改。

![ACOP](./images/saveok.png)

您应该会看到以下内容：

![ACOP](./images/eventsave.png)

再次单击&#x200B;**保存**&#x200B;以保存更改。

![ACOP](./images/save1.png)

您的事件现已配置并保存。

![ACOP](./images/eventdone.png)

再次单击您的事件以再次打开&#x200B;**编辑事件**&#x200B;屏幕。 再次将鼠标悬停在&#x200B;**有效负载**&#x200B;字段上可再次查看这3个图标。 单击&#x200B;**查看有效负载**&#x200B;图标。

![ACOP](./images/viewevent.png)

您现在将看到预期有效负载的示例。

![ACOP](./images/fullpayload.png)

您的事件具有独特的编排eventID，您可以通过在该有效负荷中向下滚动直至看到`_experience.campaign.orchestration.eventID`来查找该事件。

![ACOP](./images/payloadeventID.png)

事件ID是需要发送到Adobe Experience Platform以触发您将在练习7.2中构建的历程的内容。请记住此eventID，因为在练习7.3中您将需要它。
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

单击&#x200B;**确定**，然后单击&#x200B;**取消**。

您现在已经完成了此练习。

下一步： [3.1.2 Journey Optimizer：创建您的历程和电子邮件](./ex2.md)

[返回模块3.1](./journey-orchestration-create-account.md)

[返回所有模块](../../../overview.md)
