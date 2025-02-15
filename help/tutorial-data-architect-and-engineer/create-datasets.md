---
title: 创建数据集
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建数据集
description: 在本课程中，您将创建数据集以接收您的数据。
role: Data Architect, Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 6%

---

# 创建数据集

<!--15min-->

在本课程中，您将创建数据集以接收您的数据。 您会很高兴地知道这是本教程中最短的一课！

所有成功引入Adobe Experience Platform的数据将作为数据集保留在数据湖中。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集还包含描述其存储的数据的各个方面的元数据。

**数据架构师**&#x200B;需要在本教程之外创建数据集。

在开始练习之前，请观看此简短视频，了解有关数据集的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/27269?learn=on&enablevpops)

## 所需的权限

在[配置权限](configure-permissions.md)课程中，您已设置完成本课程所需的所有访问控制。

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 在UI中创建数据集

在本练习中，我们将在UI中创建数据集。 让我们从忠诚度数据开始：

1. 在Platform用户界面的左侧导航中转到&#x200B;**[!UICONTROL 数据集]**
1. 选择&#x200B;**[!UICONTROL 创建数据集]**按钮
   ![创建数据集](assets/datasets-createDataset.png)

1. 在下一个屏幕中，选择&#x200B;**从架构创建数据集**
1. 在下一个屏幕上，选择您的`Luma Loyalty Schema`，然后选择&#x200B;**[!UICONTROL 下一步]**按钮
   ![选择数据集](assets/datasets-selectSchema.png)

1. 命名数据集`Luma Loyalty Dataset`并选择&#x200B;**[!UICONTROL 完成]**按钮
   ![命名数据集](assets/datasets-nameDataset.png)
1. 保存数据集后，您将看到如下屏幕：
   已创建![数据集](assets/datasets-created.png)

操作完成！我告诉过你，这会很快的。 使用相同的步骤创建这些其他数据集：

1. 您的`Luma Offline Purchase Events Schema`的`Luma Offline Purchase Events Dataset`
1. 您的`Luma Web Events Schema`的`Luma Web Events Dataset`
1. 您的`Luma Product Catalog Schema`的`Luma Product Catalog Dataset`


## 使用API创建数据集

现在使用API创建`Luma CRM Dataset`。

>[!NOTE]
>
>如果您要跳过API练习并在用户界面中创建`Luma CRM Dataset`，则可以这样做。 将其命名为`Luma CRM Dataset`并使用`Luma CRM Schema`。

### 获取要在数据集中使用的架构的ID

首先，我们需要获取`Luma CRM Schema`的`$id`：

1. 打开[!DNL Postman]
1. 如果您没有访问令牌，请打开请求&#x200B;**[!DNL OAuth: Request Access Token]**，然后选择&#x200B;**发送**&#x200B;以请求新的访问令牌，就像在[!DNL Postman]课程中一样。
1. 打开请求&#x200B;**[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 选择&#x200B;**发送**&#x200B;按钮
1. 您应该收到200响应
1. 查看`Luma CRM Schema`项的响应并复制`$id`值
   ![复制$id](assets/dataset-crm-getSchemaId.png)

### 创建数据集

现在，您可以创建数据集：

1. 将[目录服务API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json)下载到`Luma Tutorial Assets`文件夹。
1. 将集合导入[!DNL Postman]
1. 选择请求&#x200B;**[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. 将以下内容粘贴为请求的&#x200B;**Body**，***将ID值替换为您自己的***：

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

1. 选择&#x200B;**发送**&#x200B;按钮
1. 您应该会收到一个包含新数据集ID的201已创建响应！
   ![使用API创建的数据集，您的自定义$id用在正文中](assets/datasets-crm-created.png)

>[!TIP]
>
> 发出此请求的常见问题以及可能的修复：
>
> * `400: There was a problem retrieving xdm schema`的问题。请确保已用您自己的`Luma CRM Schema`的ID替换上述示例中的ID
> * 无身份验证令牌：运行&#x200B;**OAuth：请求访问令牌**&#x200B;请求以生成新令牌
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`：将&#x200B;**CONTAINER_ID**&#x200B;环境变量从`global`更新为`tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`：在Admin Console中验证您的用户权限


您可以返回到Platform用户界面中的&#x200B;**[!UICONTROL 数据集]**屏幕，您可以验证是否已成功创建全部五个数据集！
![五个数据集完成](assets/datasets-allComplete.png)


## 其他资源

* [数据集文档](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=zh-Hans)
* [数据集API（目录服务的一部分）引用](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

现在，我们所有的架构、身份和数据集都已准备就绪，我们可以[为它们启用Real-time Customer Profile](enable-profiles.md)。
