---
title: 区段激活到Microsoft Azure事件中心 — 激活区段
description: 区段激活到Microsoft Azure事件中心 — 激活区段
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---

# 2.4.4激活区段

## 2.4.4.1将区段添加到Azure事件中心目标

在本练习中，您要将区段`--aepUserLdap-- - Interest in Equipment`添加到`--aepUserLdap---aep-enablement` Azure事件中心目标。

通过转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../modules/datacollection/module1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 您可以通过单击屏幕顶部蓝线中的文本&#x200B;**[!UICONTROL Production Prod]**&#x200B;来执行此操作。 选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](./../../../modules/datacollection/module1.2/images/sb1.png)

转到&#x200B;**目标**，然后单击&#x200B;**浏览**。 然后，您将看到所有可用的目标。 找到您的目标，然后单击&#x200B;**+**&#x200B;图标，如下所示。

![5-01-select-destination.png](./images/5-01-select-destination.png)

你会看到这个。 使用您的ldap搜索您的区段，并从区段列表中选择`--aepUserLdap-- - Interest in Equipment`。

单击&#x200B;**下一步**。

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP可以将有效负载交付给两种类型的目标：区段目标和配置文件目标。

区段目标将收到预定义的区段资格有效负载，该有效负载将在后面讨论。 此类有效负载包含&#x200B;**所有**&#x200B;特定配置文件的区段资格。 即使区段不在目标的激活列表中。 此类区段目标的一个示例是&#x200B;**Azure事件中心**&#x200B;和&#x200B;**AWS Kinesis**。

基于配置文件的目标允许您从XDM配置文件合并架构中选择任何属性(firstName、lastName、...)，并将其包含在激活有效负载中。 **电子邮件营销**&#x200B;就是此类目标的示例。

由于您的Azure事件中心目标是&#x200B;**区段**&#x200B;目标，因此请选择字段`--aepTenantId--.identification.core.ecid`作为示例。

单击&#x200B;**添加新字段**，单击浏览架构并选择字段`--aepTenantId--identification.core.ecid`（删除将自动显示的任何其他字段）。

单击&#x200B;**下一步**。

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

单击&#x200B;**完成**。

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

现在，您的区段将会朝着您的Microsoft事件中心目标激活。

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

下一步：[2.4.5创建您的Microsoft Azure项目](./ex5.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
