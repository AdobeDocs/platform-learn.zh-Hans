---
title: Foundation - Real-time Customer Profile — 创建区段 — API
description: Foundation - Real-time Customer Profile — 创建区段 — API
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# 2.1.5创建区段 — API

在本练习中，您将使用Postman和Adobe I/O创建区段，并将该区段的结果存储为数据集，具体方法是使用Adobe Experience Platform的API。

## Story

在实时客户个人资料中，所有个人资料数据都与事件数据和现有区段成员资格一起显示。 所显示的数据可以来自任何地方，包括Adobe应用程序和外部解决方案。 这是Adobe Experience Platform中最强大的视图，体验记录体系。

## 2.1.5.1 — 通过平台API创建区段

转到Postman。

找到集合： **_Adobe Experience Platform Enablement**。 在此集合中，您将看到一个文件夹&#x200B;**2。 分段**。 在本练习中，我们将使用这些请求。

![区段](./images/pmdtl.png)

接下来，我们将执行通过API创建区段所需的所有步骤。 我们将构建一个简单的区段：“**ldap** — 所有女性客户”。

### 步骤1 — 创建区段定义

单击名为&#x200B;**第1步 — 配置文件：创建区段定义**&#x200B;的请求。

![区段](./images/s1_call.png)

转到此请求的&#x200B;**Body**&#x200B;部分。

![区段](./images/s1_body.png)

在此请求的&#x200B;**正文**&#x200B;中，您将看到以下内容：

![区段](./images/s1_bodydtl.png)

用于此请求的语言名为Profile Query Language或&#x200B;**PQL**。

您可以在[此处](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en)找到有关PQL的更多信息和文档。


注意：请更新以下请求中的变量&#x200B;**name**，方法是将&#x200B;**ldap**&#x200B;替换为您的特定&#x200B;**ldap**。

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

添加特定的&#x200B;**ldap**&#x200B;后，正文应类似于以下内容：

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

您还应验证请求的&#x200B;**标头** — 字段。 转到&#x200B;**标头**。 您随后将看到以下内容：

![Postman](./images/s1_h.png)

| 键 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您需要指定正在使用的Adobe Experience Platform沙盒的名称。 您的x-sandbox-name应为`--aepSandboxName--`。

现在，单击蓝色的&#x200B;**发送**&#x200B;按钮以创建区段并查看其结果。

![区段](./images/s1_bodydtl_results.png)

执行此步骤后，您可以在Platform UI中查看区段定义。 若要查看此信息，请登录到Adobe Experience Platform并转到&#x200B;**区段**。

![区段](./images/s1_segmentdef.png)

### 步骤2 — 创建区段POST作业

在上一个练习中，您创建了一个&#x200B;_流式传输_&#x200B;区段。 流区段会持续实时评估资格。 您正在这里创建&#x200B;_批次_&#x200B;区段。 批处理区段可以预览该区段在资格方面的外观，但&#x200B;_并不意味着该区段实际运行了_。 当前，_没有任何人符合此区段的条件_。 要使人员符合条件，需要运行批处理客户细分，这正是我们将在此处执行的操作。

现在，我们POST区段作业。

转到Postman。

![区段](./images/pmdtl.png)

在Postman收藏集中，单击名为&#x200B;**第2步 — POST区段作业**&#x200B;的请求以将其打开。

![区段](./images/s2_call.png)

您还应验证请求的&#x200B;**标头** — 字段。 转到&#x200B;**标头**。 您随后将看到以下内容：

![Postman](./images/s2headers.png)

| 键 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您需要指定正在使用的Adobe Experience Platform沙盒的名称。 您的x-sandbox-name应为`--aepSandboxName--`。

单击蓝色的&#x200B;**发送**&#x200B;按钮。

您应会看到类似的结果：

![区段](./images/s2_call_response.png)

此区段作业正在运行，这可能需要一些时间。 在步骤3中，您可以检查此作业的状态。


### 步骤3 -GET区段作业状态

转到Postman。

![区段](./images/pmdtl.png)

在Postman收藏集中，单击名为&#x200B;**第3步 — GET区段作业状态**&#x200B;的请求。

![区段](./images/s3_call.png)

您还应验证请求的&#x200B;**标头** — 字段。 转到&#x200B;**标头**。 您随后将看到以下内容：

![Postman](./images/s3headers.png)

| 键 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您需要指定正在使用的Adobe Experience Platform沙盒的名称。 您的x-sandbox-name应为`--aepSandboxName--`。

单击蓝色的&#x200B;**发送**&#x200B;按钮。

您应会看到类似的结果：

![区段](./images/s3_status.png)

在此示例中，作业的&#x200B;**状态**&#x200B;设置为&#x200B;**已排队**。

每隔几分钟单击蓝色的&#x200B;**发送**&#x200B;按钮重复此请求，直到&#x200B;**状态**&#x200B;设置为&#x200B;**SUCCEEDED**。

![区段](./images/s3_status_succeeded.png)

一旦状态为&#x200B;**SUCCEEDED**，您的区段作业即已运行，客户现在符合该区段的资格。

恭喜，您已成功完成分段练习。 现在，让我们看一下如何在整个企业内激活Real-time Customer Profile。

下一步：[2.1.6在呼叫中心查看您正在运行的实时客户档案](./ex6.md)

[返回模块2.1](./real-time-customer-profile.md)

[返回所有模块](../../../overview.md)
