---
title: offer decisioning — 使用API测试您的决策
description: 使用API测试您的决策
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# 3.3.6使用API测试您的决策

## 3.3.6.1使用Postman的Offer decisioningAPI

将[此Offer decisioning的Postman收藏集](./../../../assets/postman/postman_offer-decisioning.zip)下载到您的桌面并解压缩。 然后，您将拥有以下权限：

![OD API](./images/unzip.png)

您的桌面上现在有此文件：

- [!UICONTROL _模块14- Decisioning Service.postman_collection.json]

在[练习2.1.3 — 对Adobe I/O](./../../../modules/rtcdp-b2c/module2.1/ex3.md)进行Postman身份验证中，您已安装Postman。 在本练习中，您将需要再次使用Postman 。

打开Postman。 单击&#x200B;**[!UICONTROL 导入]**。

![Adobe I/O新集成](./images/postmanui.png)

单击&#x200B;**[!UICONTROL 上载文件]**。

![Adobe I/O新集成](./images/pm1.png)

选择文件&#x200B;**[!UICONTROL _Module 14- Decisioning Service.postman_collection.json]**，然后单击&#x200B;**[!UICONTROL 打开]**。

![Adobe I/O新集成](./images/pm2.png)

然后，您将在Postman中拥有此收藏集。

![Adobe I/O新集成](./images/pm3.png)

您现在拥有Postman中开始通过API与Adobe Experience Platform交互所需的一切。

### 3.3.6.1.1列表容器

单击以打开请求&#x200B;**[!UICONTROL GET — 列出容器]**。

在&#x200B;**[!UICONTROL 参数]**&#x200B;下，您将看到以下内容：

- 属性： `_instance.parentName==aepenablementfy22`

在该参数中，**[!UICONTROL aepenablementfy22]**&#x200B;是Adobe Experience Platform中使用的沙盒的名称。 您应使用的沙盒是`--aepSandboxName--`。 将文本&#x200B;**[!UICONTROL aepenablementfy22]**&#x200B;替换为`--aepSandboxName--`。

替换沙盒名称后，单击&#x200B;**[!UICONTROL 发送]**。

![OD API](./images/api2.png)

这是响应，其中显示您指定的沙盒的选件容器。 请复制如下所示的&#x200B;**[!UICONTROL container instanceId]**，并将其写在计算机上的文本文件中。 下一个练习需要使用此&#x200B;**[!UICONTROL container instanceId]**！

![OD API](./images/api3.png)

### 3.3.6.1.2列表投放位置

单击以打开请求&#x200B;**[!UICONTROL GET — 列表投放位置]**。 单击&#x200B;**[!UICONTROL 发送]**。

![OD API](./images/api4.png)

现在，您的选件容器中会显示所有可用的版面。 正如您在[练习3.3.1.3](./ex1.md)中所看到的，您所看到的版面是在Adobe Experience Platform UI中定义的。

![OD API](./images/api5.png)

### 3.3.6.1.3列出决定规则

单击以打开请求&#x200B;**[!UICONTROL GET — 列出决策规则]**。 单击&#x200B;**[!UICONTROL 发送]**。

![OD API](./images/api6.png)

在响应中，您将看到在Adobe Experience Platform UI中定义的决策规则，如您在[练习3.3.1.4](./ex1.md)中所见。

![OD API](./images/api7.png)

### 3.3.6.1.4列出个性化优惠

单击以打开请求&#x200B;**[!UICONTROL GET — 列出个性化优惠]**。 单击&#x200B;**[!UICONTROL 发送]**。

![OD API](./images/api8.png)

在响应过程中，您将在[练习3.3.2.1](./ex2.md)中看到您在Adobe Experience Platform UI中定义的个性化优惠。

![OD API](./images/api9.png)

### 3.3.6.1.5列出后备优惠

单击以打开请求&#x200B;**[!UICONTROL GET — 列出后备优惠]**。 单击&#x200B;**[!UICONTROL 发送]**。

![OD API](./images/api10.png)

在响应过程中，您将在[练习3.3.2.2](./ex2.md)中看到在Adobe Experience Platform UI中定义的后备优惠。

![OD API](./images/api11.png)

### 3.3.6.1.6列表收藏集

单击以打开请求&#x200B;**[!UICONTROL GET — 列出收藏集]**。

![OD API](./images/api12.png)

在响应中，您将在[练习3.3.2.3](./ex2.md)中看到您在Adobe Experience Platform UI中定义的集合。

![OD API](./images/api13.png)

### 3.3.6.1.7获取客户个人资料的详细选件

单击以打开请求&#x200B;**[!UICONTROL POST — 获取客户配置文件的详细选件]**。 此请求与上一个请求类似，但实际上将返回图像URL、文本等详细信息。

![OD API](./images/api23.png)

对于此请求（与具有类似要求的上一个练习类似），您需要提供&#x200B;**[!UICONTROL xdm：placementId]**&#x200B;和&#x200B;**[!UICONTROL xdm：activityId]**&#x200B;的值，以检索客户的特定选件详细信息。

需要填写字段&#x200B;**[!UICONTROL xdm：activityId]**。 您可以在Adobe Experience Platform UI中检索它，如下所示。

![OD API](./images/activityid.png)

需要填写字段&#x200B;**[!UICONTROL xdm：placementId]**。 您可以在Adobe Experience Platform UI中检索它，如下所示。 在以下示例中，您可以看到版面&#x200B;**[!UICONTROL Web — 图像]**&#x200B;的placementId。

![OD API](./images/placementid.png)

转到&#x200B;**[!UICONTROL 正文]**，然后输入要向其请求优惠的客户的电子邮件地址。 单击&#x200B;**[!UICONTROL 发送]**。

![OD API](./images/api24.png)

最后，您将看到什么类型的个性化优惠以及需要向该客户显示哪些资产的结果。

![OD API](./images/api25.png)

您现在已经完成了此练习。

下一步：[摘要和优点](./summary.md)

[返回模块3.3](./offer-decisioning.md)

[返回所有模块](./../../../overview.md)
