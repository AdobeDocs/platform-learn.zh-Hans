---
title: 摄取批量数据
seo-title: Ingest batch data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 摄取批量数据
description: 在本课程中，您将使用各种方法将批量数据摄取到Experience Platform中。
role: Data Engineer
feature: Data Ingestion
kt: 4348
thumbnail: 4348-ingest-batch-data.jpg
exl-id: fc7db637-e191-4cc7-9eec-29f4922ae127
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 0%

---

# 摄取批量数据

<!-- 1hr-->
在本课程中，您将使用各种方法将批量数据摄取到Experience Platform中。

批量数据摄取允许您一次将大量数据摄取到Adobe Experience Platform。 您可以在Platform界面中或使用API，一次性摄取批量数据。 您还可以使用源连接器配置从第三方服务（如云存储服务）定期安排的批量上传。

**数据工程师** 将需要在本教程之外摄取批量数据。

在开始练习之前，请观看此简短视频，以了解有关数据摄取的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)


## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--
* Permission item **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]**, **[!UICONTROL Manage Datasets]** and **[!UICONTROL Data Monitoring]**
* Permission items **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

在“源”练习中，您需要访问(S)FTP服务器或云存储解决方案。 如果您没有解决方法，则可以使用此方法。

## 使用Platform用户界面批量摄取数据

数据可以以JSON和Parquet格式直接上传到数据集屏幕上的数据集中。 这是在创建

### 下载并准备数据

首先，获取示例数据并为租户自定义该数据：

>[!NOTE]
>
>包含在 [luma-data.zip](assets/luma-data.zip) 文件是虚构的，仅用于演示目的。

1. 下载 [luma-data.zip](assets/luma-data.zip) 至 **Luma教程资产** 文件夹。
1. 解压缩文件，并创建一个名为 `luma-data` 其中包含我们在本课程中使用的四个数据文件
1. 打开 `luma-loyalty.json` ，并替换 `_techmarketingdemos` 使用您自己的underscore-tenant id，如您自己的架构中所示：
   ![下划线租户ID](assets/ingestion-underscoreTenant.png)

1. 保存更新的文件

### 摄取数据

1. 在Platform用户界面中，选择 **[!UICONTROL 数据集]** 在左侧导航中
1. 打开 `Luma Loyalty Dataset`
1. 向下滚动直到您看到 **[!UICONTROL 添加数据]** 右列的
1. 上传 `luma-loyalty.json` 文件。
1. 文件上传后，将显示批处理的行
1. 如果您在几分钟后重新加载页面，则应会看到该批处理已成功上传，其中包含1000条记录和1000个配置文件片段。

   ![摄取](assets/ingestion-loyalty-uploadJson.png)
<!--do i need to explain error diagnostics and partial ingestion-->

>[!NOTE]
>
>有几个选择， **[!UICONTROL 错误诊断]** 和 **[!UICONTROL 部分摄取]**，您将在本课程的各个屏幕上看到该内容。 教程中未介绍这些选项。 一些快速信息：
>
>* 启用错误诊断会生成有关摄取数据的数据，然后您可以使用数据访问API查看这些数据。 在 [文档](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html).
>* 部分摄取允许您摄取包含错误的数据，最多可以指定某个阈值。 在 [文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/partial.html)


### 验证数据

有几种方法可确认已成功摄取数据。

#### 在Platform用户界面中验证

要确认已将数据摄取到数据集，请执行以下操作：

1. 在摄取数据的同一页面上，选择 **[!UICONTROL 预览数据集]** 按钮
1. 选择 **预览** 按钮，您应该能够看到一些摄取的数据。

   ![预览成功的数据集](assets/ingestion-loyalty-preview.png)


要确认登录到用户档案的数据（数据登陆可能需要几分钟），请执行以下操作：

1. 转到 **[!UICONTROL 用户档案]** 在左侧导航中
1. 选择 **[!UICONTROL 选择身份命名空间]** 字段以打开模式窗口
1. 选择 `Luma Loyalty Id` 命名空间
1. 然后，输入 `loyaltyId` 值，  `5625458`
1. 选择 **[!UICONTROL 查看]**

   ![从数据集确认用户档案](assets/ingestion-loyalty-profile.png)

#### 使用数据摄取事件进行验证

如果您订阅了上一课程中的数据摄取事件，请检查您唯一的webhook.site URL。 您应会看到三个请求按以下顺序显示，它们之间会有一段时间，并且如下所示 `eventCode` 值：

1. `ing_load_success` — 摄取的批次
1. `ig_load_success` — 将批次摄取到身份图中
1. `ps_load_success` — 将批次摄取到配置文件服务中

![数据摄取WebHook](assets/ingestion-loyalty-webhook.png)

请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events) 以了解有关通知的更多详细信息。

## 使用Platform API批量摄取数据

现在，让我们使用API上传数据。

>[!NOTE]
>
>数据架构师，可随时通过用户界面方法上传CRM数据。

### 下载并准备数据

1. 您应该已经下载并解压 [luma-data.zip](assets/luma-data.zip) 到 `Luma Tutorial Assets` 文件夹。
2. 打开 `luma-crm.json` ，并替换 `_techmarketingdemos` ，如您的架构中所示
3. 保存更新的文件

### 获取数据集ID

首先，让我们获取要将数据摄取到的数据集的数据集ID:

1. Open [!DNL Postman]
1. 如果您在过去24小时内未发出请求，则授权令牌可能已过期。 打开请求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 选择 **发送** 请求新的JWT和访问令牌，就像您在 [!DNL Postman] 课程。
1. 打开环境变量，并确保 **CONTAINER_ID** 仍为 `tenant`
1. 打开请求 **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]** 选择 **发送**
1. 你应该得到 `200 OK` 响应
1. 复制 `Luma CRM Dataset` 从响应主体
   ![获取数据集ID](assets/ingestion-crm-getDatasetId.png)

### 创建批

现在，我们可以在数据集中创建一个批次：

1. 下载 [数据摄取API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json) 至 `Luma Tutorial Assets` 文件夹
1. 将集合导入 [!DNL Postman]
1. 选择请求 **[!DNL Data Ingestion API > Batch Ingestion > Create a new batch in Catalog Service.]**
1. 将以下内容粘贴为 **正文** 请求， ***将datasetId值替换为您自己的***:

   ```json
   {
       "datasetId":"REPLACE_WITH_YOUR_OWN_DATASETID",
       "inputFormat": {
           "format": "json"
       }
   }
   ```

1. 选择 **发送** 按钮
1. 您应会收到一个201 Created响应，其中包含新批次的ID!
1. 复制 `id` 新批的
   ![批次创建](assets/ingestion-crm-createBatch.png)

### 摄取数据

现在，我们可以将数据上传到批处理：

1. 选择请求 **[!DNL Data Ingestion API > Batch Ingestion > Upload a file to a dataset in a batch.]**
1. 在 **参数** 选项卡，在相应的字段中输入数据集id和批处理id
1. 在 **参数** ，输入 `luma-crm.json` 作为 **filePath**
1. 在 **正文** 选项卡，选择 **二进制** 选项
1. 选择下载的 `luma-crm.json` 从本地 `Luma Tutorial Assets` 文件夹
1. 选择 **发送** 而且您应会在响应主体中得到一个包含“1”的200 OK响应

   ![上载数据](assets/ingestion-crm-uploadFile.png)

此时，如果您在Platform用户界面中查看批处理，您会看到它位于“[!UICONTROL 正在加载]&quot;状态：
![批量加载](assets/ingestion-crm-loading.png)

由于批处理API通常用于上传多个文件，因此您需要告知平台批次何时完成，我们将在下一步中执行该操作。

### 完成批处理

要完成批，请执行以下操作：

1. 选择请求 **[!DNL Data Ingestion API > Batch Ingestion > Finish uploading a file to a dataset in a batch.]**
1. 在 **参数** ，输入 `COMPLETE` 作为 **操作**
1. 在 **参数** 选项卡，输入批ID。 如果存在数据集id或filePath，则不要担心它们。
1. 确保POST的URL为 `https://platform.adobe.io/data/foundation/import/batches/:batchId?action=COMPLETE` 而且没有任何不必要的 `datasetId` 或 `filePath`
1. 选择 **发送** 而且您应会在响应主体中得到一个包含“1”的200 OK响应

   ![批量完成](assets/ingestion-crm-complete.png)

### 验证数据

#### 在Platform用户界面中验证

验证数据是否已登录到Platform用户界面，就像您对Loyaty数据集所做的一样。

首先，确认批次显示已摄取1000条记录：

![批量成功](assets/ingestion-crm-success.png)

接下来，使用“预览”数据集确认批次：

![批量预览](assets/ingestion-crm-preview.png)

最后，通过查找 `Luma CRM Id` 命名空间，例如 `112ca06ed53d3db37e4cea49cc45b71e`

![摄取的用户档案](assets/ingestion-crm-profile.png)

有件有趣的事情，我想指出。 打开 `Danny Wright` 配置文件。 用户档案的 `Lumacrmid` 和 `Lumaloyaltyid`. 记住 `Luma Loyalty Schema` 包含两个标识字段，即Luma忠诚度ID和CRM ID。 现在，我们已上传这两个数据集，它们已合并到单个用户档案中。 忠诚度数据 `Daniel` 名称和“纽约市”作为主地址，而CRM数据已 `Danny` 作为名字和 `Portland` 作为具有相同忠诚度ID的客户的主页地址。 我们回到名字显示的原因 `Danny` 中有关合并策略的课程。

恭喜，您刚刚合并了用户档案！

![合并的配置文件 ](assets/ingestion-crm-profileLinkedIdentities.png)

#### 使用数据摄取事件进行验证

如果您订阅了上一课程中的数据摄取事件，请检查您唯一的webhook.site URL。 此时，您应会看到有三个请求出现，就像会员数据一样：

![数据摄取WebHook](assets/ingestion-crm-webhook.png)

请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events) 以了解有关通知的更多详细信息。

## 使用工作流摄取数据

让我们看看另一种上传数据的方式。 工作流功能允许您摄取尚未在XDM中建模的CSV数据。

### 下载并准备数据

1. 您应该已经下载并解压 [luma-data.zip](assets/luma-data.zip) 到 `Luma Tutorial Assets` 文件夹。
1. 确认您已`luma-products.csv`

### 创建工作流

现在，让我们设置工作流：

1. 转到 **[!UICONTROL 工作流]** 在左侧导航中
1. 选择 **[!UICONTROL 将CSV映射到XDM架构]** ，然后选择 **[!UICONTROL Launch]** 按钮
   ![启动工作流](assets/ingestion-products-launchWorkflow.png)
1. 选择 `Luma Product Catalog Dataset` ，然后选择 **[!UICONTROL 下一个]** 按钮
   ![选择您的数据集](assets/ingestion-products-selectDataset.png)
1. 添加 `luma-products.csv` 下载的文件，然后选择 **[!UICONTROL 下一个]** 按钮
   ![选择您的数据集](assets/ingestion-products-selectData.png)
1. 现在，您位于映射器界面中，在该界面中，可以从源数据( `luma-products.csv` 文件)到目标架构中的XDM字段。 在我们的示例中，列名称与架构字段名称足够接近，映射器能够自动检测右侧映射！ 如果映射器无法自动检测右侧字段，则可以选择目标字段右侧的图标以选择正确的XDM字段。 此外，如果您不想从CSV中摄取其中一个列，则可以从映射器中删除该行。 您可以随时在 `luma-products.csv` 以了解映射器的工作方式。
1. 选择 **[!UICONTROL 完成]** 按钮
   ![选择您的数据集](assets/ingestion-products-mapper.png)

### 验证数据

上传批量后，通过预览数据集来验证上传情况。

自 `Luma Product SKU` 是非人员命名空间，我们看不到产品SKU的任何用户档案。

您应会看到网页钩的三次点击。

## 使用源摄取数据

好吧，你做的很艰难。 现在，让我们进入到 _自动化_ 批量摄取！ 当我说，“设置！” 你说，&quot;别管它！&quot; “设置！” “算了吧！” “设置！” “算了吧！” 开玩笑的，你绝不会做这种事！ 好，回去工作。 你快完蛋了。

转到 **[!UICONTROL 源]** 在左侧导航中打开源目录。 在此，您将看到与业界领先的数据和存储提供商的各种现成集成。

![源目录](assets/ingestion-offline-sourceCatalog.png)

好，让我们使用源连接器摄取数据。

这项练习将是您自己选择的冒险风格。 我将使用FTP源连接器显示工作流。 您可以使用您在公司中使用的其他云存储源连接器，也可以使用与忠诚度数据一样的数据集用户界面上传json文件。

许多源都具有类似的配置工作流，在该工作流中，您可以：

1. 输入您的身份验证详细信息
1. 选择要摄取的数据
1. 选择要将其摄取到的Platform数据集
1. 将字段映射到XDM架构
1. 选择要从该位置提取数据的频率

>[!NOTE]
>
>我们将在本练习中使用的离线购买数据包含日期时间数据。 日期时间数据应位于 [ISO 8061格式化字符串](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15&quot;:05:59.000-08:00&quot;)或Unix时间（以毫秒为格式）(1531263959000)，在摄取时将转换为目标XDM类型。 有关数据转换和其他限制的更多信息，请参阅 [批量摄取API文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/api-overview.html#types).

### 下载、准备数据并将数据上传到首选的云存储供应商

1. 您应该已经下载并解压 [luma-data.zip](assets/luma-data.zip) 到 `Luma Tutorial Assets` 文件夹。
1. 打开 `luma-offline-purchases.json` ，并替换 `_techmarketingdemos` ，如您的架构中所示
1. 选择首选的云存储提供商，确保该提供商位于 [!UICONTROL 源] 目录
1. 上传 `luma-offline-purchases.json` 到首选云存储提供商中的位置

### 将数据摄取到首选的云存储位置

1. 在Platform用户界面中，过滤 [!UICONTROL 源] 目录 **[!UICONTROL 云存储]**
1. 请注意， `...`
1. 在首选云存储供应商的框中，选择 **[!UICONTROL 配置]** 按钮
   ![选择配置](assets/ingestion-offline-selectFTP.png)
1. **[!UICONTROL 身份验证]** 是第一步。 例如，输入帐户的名称 `Luma's FTP Account` 和您的身份验证详细信息。 对于所有云存储源，此步骤应该相当相似，不过字段可能略有不同。 在输入了帐户的身份验证详细信息后，您便可以将其重复用于其他源连接，这些源连接可能会与同一帐户中的其他文件在不同的计划上发送不同的数据
1. 选择 **[!UICONTROL “连接到源”按钮]**
1. 当平台成功连接到源时，选择 **[!UICONTROL 下一个]** 按钮
   ![对源进行身份验证](assets/ingestion-offline-authentication.png)

1. 在 **[!UICONTROL 选择数据]** 步骤中，用户界面将使用您的凭据打开云存储解决方案上的文件夹
1. 例如，选择要摄取的文件 `luma-offline-purchases.json`
1. 作为 **[!UICONTROL 数据格式]**，选择 `XDM JSON`
1. 然后，您可以预览文件中的json结构和示例数据
1. 选择 **[!UICONTROL 下一个]** 按钮
   ![选择您的数据文件](assets/ingestion-offline-selectData.png)

1. 在 **[!UICONTROL 映射]** 步骤，选择 `Luma Offline Purchase Events Dataset` ，然后选择 **[!UICONTROL 下一个]** 按钮。 消息中请注意，由于我们摄取的数据是JSON文件，因此没有映射步骤，我们将源字段映射到目标字段。 JSON数据必须已在XDM中。 如果您摄取的是CSV，则会在此步骤中看到完整映射用户界面：
   ![选择您的数据集](assets/ingestion-offline-mapping.png)
1. 在 **[!UICONTROL 计划]** 步骤中，选择要从源中提取数据的频率。 请花些时间查看选项。 我们只是要进行一次性摄取，请将 **[!UICONTROL 频率]** on **[!UICONTROL 一次]** ，然后选择 **[!UICONTROL 下一个]** 按钮：
   ![计划数据流](assets/ingestion-offline-scheduling.png)
1. 在 **[!UICONTROL 数据流详细信息]** 步骤中，您可以为数据流选择名称、输入可选描述、打开错误诊断和部分摄取。 保留设置原样，然后选择 **[!UICONTROL 下一个]** 按钮：
   ![编辑数据流的详细信息](assets/ingestion-offline-detail.png)
1. 在 **[!UICONTROL 审阅]** 步骤中，您可以一起查看所有设置，然后对其进行编辑或选择 **[!UICONTROL 完成]** 按钮
1. 保存后，您会在屏幕上看到如下内容：
   ![完成](assets/ingestion-offline-complete.png)

### 验证数据

上传批量后，通过预览数据集来验证上传情况。

您应会看到网页钩的三次点击。

查找具有值的用户档案 `5625458` 在 `loyaltyId` 命名空间，以查看其配置文件中是否存在任何购买事件。 您应会看到一次购买。 您可以通过选择 **[!UICONTROL 查看JSON]**:

![用户档案中的购买事件](assets/ingestion-offline-eventInProfile.png)

## ETL工具

Adobe与多个ETL供应商合作，以支持将数据摄取到Experience Platform中。 由于第三方供应商种类繁多，因此本教程中未介绍ETL，不过欢迎您查看以下一些资源：

* [为Adobe Experience Platform开发ETL集成](https://experienceleague.adobe.com/docs/experience-platform/etl/home.html)
* [Informatica Adobe Experience Platform ConnectorAdobeExchange页面](https://exchange.adobe.com/experiencecloud.details.101570.informatica-adobe-experience-cloud-connector.html)
* [Adobe Experience Platform Connector的信息文档 ](https://docs.informatica.com/integration-cloud/cloud-data-integration-connectors/current-version/adobe-experience-platform-connector/preface.html)
* [从数据派生的独特受众体验：Unifi和Adobe Experience Platform](https://unifisoftware.com/solutions/adobe-experience-platform/)
* [[!DNL Snaplogic] Adobe Experience Platform Snap Pack](https://www.snaplogic.com/resources/videos/august-2020-aep)

## 其他资源

* [批量摄取文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html)
* [批量摄取API参考](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion)

现在，让我们 [使用Web SDK流数据](ingest-streaming-data.md)
