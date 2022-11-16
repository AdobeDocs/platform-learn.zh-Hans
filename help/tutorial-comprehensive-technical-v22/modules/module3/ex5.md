---
title: 基础 — 实时客户资料 — 创建区段 — API
description: 基础 — 实时客户资料 — 创建区段 — API
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 3f537efd-7281-4c0c-b809-97f266a2a337
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 3%

---

# 3.5创建区段 — API

在本练习中，您将使用Postman和Adobe I/O通过使用Adobe Experience Platform的API，创建一个区段，并将该区段的结果存储为数据集。

## Story

在“实时客户资料”中，所有资料数据都与事件数据和现有区段成员资格一起显示。 显示的数据可以从任何位置(从Adobe应用程序和外部解决方案)获取。 这是Adobe Experience Platform最有力的观点，是记录体验系统。

## 练习3.5.1 — 通过Platform API创建区段

去Postman。

找到收藏集： **_Adobe Experience Platform启用**. 在此收藏集中，您将看到一个文件夹 **2. 区段**. 我们将在本练习中使用这些请求。

![区段](./images/pmdtl.png)

我们接下来将执行所有必需的步骤以通过API创建区段。 我们将构建一个简单的区段：&quot;**ldap**  — 所有女性客户”。

### 步骤1 — 创建区段定义

单击名为 **步骤1 — 配置文件：创建区段定义**.

![区段](./images/s1_call.png)

转到 **正文** 部分。

![区段](./images/s1_body.png)

在 **正文** 在此请求中，您将看到以下内容：

![区段](./images/s1_bodydtl.png)

此请求所使用的语言称为用户档案查询语言，或 **PQL**.

您可以找到有关PQL的更多信息和文档 [此处](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en).


注意：请更新变量 **name** 在以下请求中，通过将 **ldap** 在您的 **ldap**.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

添加特定 **ldap**，则正文应类似于以下内容：

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

您还应验证 **标题**  — 请求的字段。 转到 **标题**. 然后您将看到：

![Postman](./images/s1_h.png)

| 键 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您需要指定所使用的Adobe Experience Platform沙盒的名称。 您的x-sandbox-name应为 `--aepSandboxId--`.

现在，单击蓝色 **发送** 按钮以创建区段并查看该区段的结果。

![区段](./images/s1_bodydtl_results.png)

完成此步骤后，您可以在平台UI中查看区段定义。 要选中此复选框，请登录到Adobe Experience Platform，然后转到 **区段**.

![区段](./images/s1_segmentdef.png)

### 第2步 — 创建区段POST作业

在上一个练习中，您创建了 _流_ 区段。 流区段会持续实时评估资格。 你在这里做的，是在 _批次_ 区段。 批处理客户细分可让您预览该客户细分在资格方面的外观，但 _这并不意味着该区段已实际运行_. 目前， _没有人符合此区段的资格_. 要使人员符合条件，需要运行批处理客户细分，这正是我们在此将要执行的操作。

现在，让我们POST区段作业。

去Postman。

![区段](./images/pmdtl.png)

在Postman集合中，单击名为 **第2步 — POST区段作业** 打开它。

![区段](./images/s2_call.png)

您还应验证 **标题**  — 请求的字段。 转到 **标题**. 然后您将看到：

![Postman](./images/s2headers.png)

| 键 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您需要指定所使用的Adobe Experience Platform沙盒的名称。 您的x-sandbox-name应为 `--aepSandboxId--`.

单击蓝色 **发送** 按钮。

您应会看到类似的结果：

![区段](./images/s2_call_response.png)

此区段作业当前正在运行，这可能需要一些时间。 在步骤3中，您将能够检查此作业的状态。


### 步骤3 -GET区段作业状态

去Postman。

![区段](./images/pmdtl.png)

在Postman集合中，单击名为 **步骤3 -GET区段作业状态**.

![区段](./images/s3_call.png)

您还应验证 **标题**  — 请求的字段。 转到 **标题**. 然后您将看到：

![Postman](./images/s3headers.png)

| 键 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您需要指定所使用的Adobe Experience Platform沙盒的名称。 您的x-sandbox-name应为 `--aepSandboxId--`.

单击蓝色 **发送** 按钮。

您应会看到类似的结果：

![区段](./images/s3_status.png)

在本例中， **状态** 的 **已排队**.

单击蓝色的 **发送** 按钮，直到 **状态** 设置为 **成功**.

![区段](./images/s3_status_succeeded.png)

状态为 **成功**，则区段作业已运行，且客户现在符合区段资格条件。

恭喜，您已成功完成分段练习。 现在，让我们看一看如何在整个企业中激活实时客户资料。

下一步： [3.6请在呼叫中心查看您的实时客户资料](./ex6.md)

[返回到模块3](./real-time-customer-profile.md)

[返回到所有模块](../../overview.md)
