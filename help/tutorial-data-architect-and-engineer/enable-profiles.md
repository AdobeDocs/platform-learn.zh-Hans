---
title: 启用实时客户档案
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 启用实时客户档案
description: 在本课程中，您将为Real-time Customer Profile启用架构和数据集。
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# 启用实时客户档案

<!-- 15min-->
在本课程中，您将为Real-time Customer Profile启用架构和数据集。

好的，当我说数据集课程是本教程中最短的课程时，我撒了谎 — 这个课程应该用更少的时间！ 实际上，你所要做的就是翻动一栈开关。 但是，当您翻转这些开关时，会出现什么情况&#x200B;_真的很_&#x200B;重要，因此我想为它专注一整页。

利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 用户档案允许您将不同的客户数据整合到一个统一的视图中，并提供每个客户交互的带时间戳的可操作帐户。

尽管听起来很神奇，但您无需为配置文件激活&#x200B;*所有数据*。 事实上，您应该只启用激活用例所需的数据。 启用要用于营销用例、呼叫中心集成等的数据，在这些用例中，您需要快速访问强大的客户档案。 如果您只上传数据进行分析，则可能不应为配置文件启用此功能。

在决定您自己的哪些数据应为配置文件启用时，您应该查看实时客户配置文件数据](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)的重要[护栏。

<!--is this accurate. Are there other considerations to point out? -->

**数据架构师**&#x200B;需要在本教程之外启用Real-Time Customer Profile。

在开始练习之前，请观看此简短视频，了解有关Real-Time Customer Profile的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on)

## 所需的权限

在[配置权限](configure-permissions.md)课程中，您已设置完成本课程所需的所有访问控制。


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 使用Platform用户界面为Real-time Customer Profile启用架构

让我们从启用架构的简单任务开始：

1. 在Platform用户界面中，打开&#x200B;**Luma忠诚度架构**
1. 在&#x200B;**[!UICONTROL 架构属性]**&#x200B;中，切换&#x200B;**配置文件**&#x200B;开关
1. 在确认模式中，按&#x200B;**[!UICONTROL 启用]**&#x200B;按钮进行确认
1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;按钮以保存更改

   >[!IMPORTANT]
   >
   >为配置文件启用架构后，无法禁用或删除该架构。 此外，此后无法从架构中删除字段。 在生产环境中使用您自己的数据时，请务必牢记这些含义。 在本教程中，您应该使用开发沙盒，您可以随时删除这个沙盒。
   >
   >在本教程的受控环境中，您将在引入任何数据&#x200B;_之前，为配置文件_&#x200B;启用架构和数据集。 在处理您自己的数据时，我们建议您按照以下顺序执行操作：
   >
   > 1. 首先，将一些数据摄取到数据集中。
   > 1. 解决在数据摄取过程中出现的任何问题（例如，数据验证或映射问题）。
   > 1. 为配置文件启用数据集和架构
   > 1. 重新摄取数据


   ![配置文件切换](assets/profile-loyalty-enableSchema.png)

轻松吧？ 对这些其他架构重复上述步骤：

1. Luma产品目录架构
1. Luma离线购买事件架构
1. Luma Web事件架构（在确认模式下，选中“此架构的数据将在identityMap字段中包含主标识”复选框。）

## 使用平台API为Real-time Customer Profile启用架构

现在该使用API启用`Luma CRM Schema`。 如果要跳过此练习并在用户界面中启用它，请直接进行下一步。

### 获取架构的meta：altId

首先，让我们获取`Luma CRM Schema`的`meta:altId`：

1. 打开[!DNL Postman]
1. 如果您没有访问令牌，请打开请求&#x200B;**[!DNL OAuth: Request Access Token]**，然后选择&#x200B;**发送**&#x200B;以请求新的访问令牌，就像在[!DNL Postman]课程中一样。
1. 打开请求&#x200B;**[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 选择&#x200B;**发送**&#x200B;按钮
1. 您应该收到200响应
1. 查看`Luma CRM Schema`项的响应并复制`meta:altId`值
   ![复制meta：altIid](assets/profile-crm-getMetaAltId.png)

### 启用架构

现在我们有了架构的meta：altId，可以为配置文件启用它：

1. 打开请求&#x200B;**[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. 在&#x200B;**参数**&#x200B;中，将您的`meta:altId`值粘贴为`SCHEMA_ID`参数值
1. 在&#x200B;**正文**&#x200B;选项卡中，粘贴以下代码

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. 选择&#x200B;**发送**&#x200B;按钮
1. 您应该收到200响应

   ![使用作为SCHEMA_ID参数的自定义meta：altIid为配置文件启用CRM架构](assets/profile-crm-enableProfile.png)

您应该能够在用户界面中看到已为配置文件启用所有五个架构（您可能需要按SHIFT重新加载才能看到`Luma CRM Schema`已启用）：
![所有架构已启用](assets/profile-allSchemasEnabled.png)


## 使用Platform用户界面为Real-time Customer Profile启用数据集

还必须为配置文件启用数据集，此过程更加简单：

1. 在Platform用户界面中，打开`Luma Loyalty Dataset`
1. 切换&#x200B;**[!UICONTROL 配置文件]**&#x200B;开关
1. 在确认模式中，按&#x200B;**[!UICONTROL 启用]**&#x200B;按钮进行确认

   ![配置文件切换](assets/profile-loyalty-enableDataset.png)

对这些其他数据集重复上述步骤：

1. Luma产品目录数据集
1. Luma离线购买事件数据集
1. Luma Web事件数据集

>[!NOTE]
>
>与架构不同，您可以从配置文件中禁用数据集，但所有之前摄取的数据将保留在配置文件中。

## 使用平台API为Real-time Customer Profile启用数据集

现在，您将使用API为用户档案启用数据集。 同样，如果您希望使用上述方法通过用户界面启用它，这也没问题。

### 获取数据集的id

首先，我们需要获取`Luma CRM Dataset`的`id`：

1. 打开[!DNL Postman]
1. 如果您没有访问令牌，请打开请求&#x200B;**[!DNL OAuth: Request Access Token]**，然后选择&#x200B;**发送**&#x200B;以请求新的访问令牌，就像在[!DNL Postman]课程中一样。
1. 打开请求&#x200B;**[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. 选择&#x200B;**发送**&#x200B;按钮
1. 您应该收到200响应
1. 查看`Luma CRM Dataset`项目的响应并复制ID：
   ![复制ID](assets/profile-crm-copyDatasetId.png)

### 启用数据集

现在我们有了数据集的ID，可以为配置文件启用它：

1. 打开请求&#x200B;**[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. 在&#x200B;**参数**&#x200B;中，将`DATASET_ID`值更新为您自己的值
1. 在&#x200B;**正文**&#x200B;选项卡中，粘贴以下代码。 请注意，前两个值是预先存在的标记，在前一个响应中可见。 除了我们即将添加的两个新标记之外，还需要将它们包含在正文中：

   ```json
   {
       "tags":{
           "adobe/pqs/table":["luma_crm_dataset"],
           "adobe/siphon/table/format":["parquet"],
           "unifiedProfile":["enabled:true"],
           "unifiedIdentity":["enabled:true"]
           }
   }
   ```

1. 选择&#x200B;**发送**&#x200B;按钮
1. 您应该收到200响应

   ![为配置文件启用CRM数据集，确保将自定义数据集ID用作DATASET_ID参数](assets/profile-crm-enableDataset.png)

您还可以确认用户界面显示数据集已启用：
![确认](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> 如果在为用户档案启用架构和数据集之前摄取数据，则以后需要再次摄取该数据。

## 其他资源

* [实时客户资料文档](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hans)
* [实时客户个人资料API参考](https://www.adobe.io/experience-platform-apis/references/profile/)


**数据工程师**&#x200B;应继续参加[订阅数据摄取事件](subscribe-to-data-ingestion-events.md)课程。
**数据架构师** _可以跳过前面_&#x200B;并转到[批量摄取课程](ingest-batch-data.md)。
