---
title: 启用实时客户用户档案
seo-title: Enable Real-time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 启用实时客户用户档案
description: 在本课程中，您将为实时客户用户档案启用架构和数据集。
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 1%

---

# 启用实时客户用户档案

<!-- 15min-->
在本课程中，您将为实时客户用户档案启用架构和数据集。

好，当我说数据集课程是本教程中最短的课程时，我撒了谎 — 这个课程应该花费更少的时间！ 实际上，你要做的就是翻转一堆开关。 但是当你翻开这些切换开关时 _真的_ 所以我想为它贡献一整页。

通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将不同的客户数据整合到统一视图中，为每次客户互动提供一个可操作且加盖时间戳的帐户。

尽管听起来很神奇，但您无需激活 *所有数据* 中。 事实上，您只应启用激活用例所需的数据。 启用要用于营销用例、呼叫中心集成等的数据，以便您能够快速访问强大的客户用户档案。 如果您上载数据仅供分析，则可能不应为用户档案启用该数据。

有很重要的 [实时客户资料数据的防护](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) 在决定应为用户档案启用哪些自己的数据时，您应该查看哪些数据。

<!--is this accurate. Are there other considerations to point out? -->

**数据架构师** 在本教程之外，将需要启用实时客户资料。

在开始练习之前，请观看此简短视频，进一步了解实时客户资料：
>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on)

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 使用平台用户界面为实时客户资料启用架构

让我们从启用架构的简单任务开始：

1. 在Platform用户界面中，打开 **Luma忠诚度架构**
1. 在 **[!UICONTROL 架构属性]**，切换 **用户档案** 开关
1. 在确认模式窗口中，按 **[!UICONTROL 启用]** 按钮确认
1. 选择 **[!UICONTROL 保存]** 按钮以保存更改

   >[!IMPORTANT]
   >
   >为配置文件启用架构后，便无法禁用或删除该架构。 此外，在此时间点之后，无法从架构中删除字段。 当您在生产环境中处理自己的数据时，请务必记住以后要考虑的这些影响。 在本教程中，您应该使用一个开发沙盒，该沙盒可随时删除。
   >
   >在本教程的受控环境中，您将为用户档案启用架构和数据集， _在摄取任何数据之前_. 使用您自己的数据时，我们建议您按以下顺序执行操作：
   >
   > 1. 首先，将一些数据摄取到数据集。
   > 1. 解决在数据获取过程中出现的任何问题（例如，数据验证或映射问题）。
   > 1. 为用户档案启用数据集和架构
   > 1. 重新摄取数据



   ![配置文件切换](assets/profile-loyalty-enableSchema.png)

轻松吧？ 对以下其他架构重复上述步骤：

1. Luma产品目录架构
1. Luma离线购买事件架构
1. Luma Web事件架构（在确认模式窗口中，选中“此架构的数据将在identityMap字段中包含主标识”框。）

## 使用Platform API为实时客户用户档案启用架构

现在，该启用 `Luma CRM Schema` 和API。 如果要跳过此练习，而只是在用户界面中启用它，请直接执行。

### 获取架构的meta:altId

先把 `meta:altId` 的 `Luma CRM Schema`:

1. Open [!DNL Postman]
1. 如果您在过去24小时内未发出请求，则授权令牌可能已过期。 打开请求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 选择 **发送** 请求新的JWT和访问令牌，就像您在 [!DNL Postman] 课程。
1. 打开请求 **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 选择 **发送** 按钮
1. 您应该收到200个响应
1. 查看 `Luma CRM Schema` 项目并复制 `meta:altId` 值
   ![复制meta:altId](assets/profile-crm-getMetaAltId.png)

### 启用架构

现在，我们拥有了架构的meta:altId，因此可以为用户档案启用它：

1. 打开请求 **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. 在 **参数** 粘贴 `meta:altId` 值作为 `SCHEMA_ID` 参数值
1. 在 **正文** ，请粘贴以下代码

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. 选择 **发送** 按钮
1. 您应该收到200个响应

   ![为自定义meta:altIid用作SCHEMA_ID参数的用户档案启用CRM架构](assets/profile-crm-enableProfile.png)

您应该能够在用户界面中看到已为用户档案启用了所有五个架构(可能需要SHIFT-Reload才能看到 `Luma CRM Schema` 启用):
![已启用所有架构](assets/profile-allSchemasEnabled.png)


## 使用Platform用户界面为实时客户资料启用数据集

此外，还必须为用户档案启用数据集，而且该过程更简单：

1. 在Platform用户界面中，打开 `Luma Loyalty Dataset`
1. 切换 **[!UICONTROL 用户档案]** 开关
1. 在确认模式窗口中，按 **[!UICONTROL 启用]** 按钮确认

   ![ 配置文件切换](assets/profile-loyalty-enableDataset.png)

对以下其他数据集重复上述步骤：

1. Luma产品目录数据集
1. Luma离线购买事件数据集
1. Luma Web事件数据集

>[!NOTE]
>
>与架构不同，您可以禁用配置文件中的数据集，但所有之前摄取的数据都将保留在配置文件中。

## 使用Platform API为实时客户资料启用数据集

现在，您将使用API为用户档案启用数据集。 同样，如果您希望使用上述方法通过用户界面启用它，那也没关系。

### 获取数据集的ID

首先，我们得 `id` 的 `Luma CRM Dataset`:

1. 打开 [!DNL Postman]
1. 如果您在过去24小时内未发出请求，则授权令牌可能已过期。 打开请求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 选择 **发送** 请求新的JWT和访问令牌，就像您在 [!DNL Postman] 课程。
1. 打开请求 **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. 选择 **发送** 按钮
1. 您应该收到200个响应
1. 查看 `Luma CRM Dataset` 项目并复制id:
   ![复制ID](assets/profile-crm-copyDatasetId.png)

### 启用数据集

现在，我们已拥有数据集的id，可以为用户档案启用它：

1. 打开请求 **[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. 在 **参数** 更新 `DATASET_ID` 价值
1. 在 **正文** ，请粘贴以下代码。 请注意，前两个值是预先存在的标记，这些标记在上一个响应中可见。 除了我们添加的两个新标记之外，还需要将它们包含在主体中：

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

1. 选择 **发送** 按钮
1. 您应该收到200个响应

   ![为配置文件启用CRM数据集，并确保将您的自定义数据集ID用作DATASET_ID参数](assets/profile-crm-enableDataset.png)

您还可以确认用户界面显示已启用的数据集：
![确认](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> 如果在为配置文件启用架构和数据集之前摄取了数据，则以后将需要再次重新摄取该数据。

## 其他资源

* [实时客户资料文档](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hans)
* [实时客户资料API参考](https://www.adobe.io/experience-platform-apis/references/profile/)


**数据工程师** 应继续 [订阅数据摄取事件](subscribe-to-data-ingestion-events.md) 课程。
**数据架构师** _可以跳前_ 然后转到 [批量摄取课程](ingest-batch-data.md).
