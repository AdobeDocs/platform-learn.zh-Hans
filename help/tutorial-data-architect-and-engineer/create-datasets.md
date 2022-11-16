---
title: 创建数据集
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建数据集
description: 在本课程中，您将创建用于接收数据的数据集。
role: Data Architect, Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 8%

---

# 创建数据集

<!--15min-->

在本课程中，您将创建用于接收数据的数据集。 您很高兴地知道，这是教程中最短的课程！

成功摄取到Adobe Experience Platform的所有数据都将作为数据集保留在数据湖中。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集还包含描述其存储的数据的各方面特性的元数据。

**数据架构师** 将需要在本教程之外创建数据集。

在开始练习之前，请观看此简短视频，了解有关数据集的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 在UI中创建数据集

在本练习中，我们将在UI中创建数据集。 让我们从忠诚度数据开始：

1. 转到 **[!UICONTROL 数据集]** 在平台用户界面的左侧导航中
1. 选择 **[!UICONTROL 创建数据集]** 按钮
   ![创建数据集](assets/datasets-createDataset.png)

1. 在下一个屏幕上，选择 **从架构创建数据集**
1. 在下一个屏幕上，选择 `Luma Loyalty Schema` ，然后选择 **[!UICONTROL 下一个]** 按钮
   ![选择数据集](assets/datasets-selectSchema.png)

1. 命名数据集 `Luma Loyalty Dataset` ，然后选择 **[!UICONTROL 完成]** 按钮
   ![命名数据集](assets/datasets-nameDataset.png)
1. 保存数据集后，您将被带到如下屏幕：
   ![创建的数据集](assets/datasets-created.png)

操作完成！我告诉过你，这会很快的。 使用相同的步骤创建这些其他数据集：

1. `Luma Offline Purchase Events Dataset` , `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` , `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` , `Luma Product Catalog Schema`


## 使用API创建数据集

现在，创建 `Luma CRM Dataset` 使用API。

>[!NOTE]
>
>如果要跳过API练习，并创建 `Luma CRM Dataset` 在用户界面中，这没问题。 将其命名为 `Luma CRM Dataset` 并使用 `Luma CRM Schema`.

### 获取要在数据集中使用的架构的ID

首先，我们得 `$id` 的 `Luma CRM Schema`:

1. Open [!DNL Postman]
1. 如果您在过去24小时内未发出请求，则授权令牌可能已过期。 打开请求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 选择 **发送** 请求新的JWT和访问令牌，就像您在 [!DNL Postman] 课程。
1. 打开请求 **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 选择 **发送** 按钮
1. 您应该收到200个响应
1. 查看 `Luma CRM Schema` 项目并复制 `$id` 值
   ![复制$id](assets/dataset-crm-getSchemaId.png)

### 创建数据集

现在，您可以创建数据集：

1. 下载 [目录服务API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) 至 `Luma Tutorial Assets` 文件夹。
1. 将集合导入 [!DNL Postman]
1. 选择请求 **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. 将以下内容粘贴为 **正文** 请求， ***将id值替换为您自己的***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. 选择 **发送** 按钮
1. 您应会收到一个201 Created响应，其中包含新数据集的ID!
   ![使用API创建的数据集，您在主体中使用的自定义$id](assets/datasets-crm-created.png)

>[!TIP]
>
> 提出此请求的常见问题和可能的修复：
>
> * `400: There was a problem retrieving xdm schema`的问题。请确保已将上述示例中的id替换为您自己的id `Luma CRM Schema`
> * 无身份验证令牌：运行 **IMS:JWT通过用户令牌生成+身份验证** 调用以生成新令牌
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`:更新 **CONTAINER_ID** 环境变量 `global` to `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`:在Admin Console中验证用户权限



您可以返回到 **[!UICONTROL 数据集]** 屏幕中，您可以验证是否成功创建了所有五个数据集！
![完成五个数据集](assets/datasets-allComplete.png)


## 其他资源

* [数据集文档](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=zh_Hans)
* [数据集API（目录服务的一部分）引用](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

现在，我们的所有架构、身份和数据集都到位了，我们可以 [为实时客户用户档案启用它们](enable-profiles.md).
