---
title: 映射身份
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 映射身份
description: 在本课程中，我们将创建身份命名空间并将身份字段添加到我们的架构。
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 2%

---

# 映射身份

<!-- 30 min-->

在本课程中，我们将创建身份命名空间并将身份字段添加到我们的架构。 这样做后，我们还将能够完成上一课程中的架构关系。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。 身份字段和命名空间是将不同数据源联接在一起以构建360度实时客户用户档案的粘合剂。

**数据架构师** 将需要在本教程之外映射身份。

在开始练习之前，请观看此简短视频，进一步了解Adobe Experience Platform中的身份信息：
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

>[!NOTE]
>
>仅当您构建实时客户用户档案时，才需要填写身份字段。 如果您仅将数据摄取到数据湖中，则不需要使用这些参数。

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 创建身份命名空间

在本练习中，我们将为Luma的自定义身份字段创建身份命名空间， `loyaltyId`, `crmId`和 `productSku`. 身份命名空间在构建实时客户配置文件方面起着关键作用，因为同一命名空间中的两个匹配值允许两个数据源形成身份图。


### 在UI中创建命名空间

让我们首先为Luma忠诚度架构创建一个命名空间：

1. 在Platform用户界面中，转到 **[!UICONTROL 标识]** 在左侧导航中
1. 您会注意到有多个现成的身份命名空间可用。 选择 **[!UICONTROL 创建身份命名空间]** 按钮
1. 提供详细信息，如下所示

   | 字段 | 值 |
   |---------------|-----------|
   | 显示名称 | Luma忠诚度Id |
   | 身份符号 | lumaLoyatyId |
   | 类型 | 跨设备 |

1. 选择 **[!UICONTROL 创建]**

   ![创建命名空间](assets/identity-createNamespace.png)

现在，使用以下详细信息为Luma产品目录架构设置另一个命名空间：

| 字段 | 值 |
|---------------|-----------|
| 显示名称 | Luma产品SKU |
| 身份符号 | lumaProductSKU |
| 类型 | 非人员标识符 |



## 使用API创建身份命名空间

我们将通过API创建CRM命名空间。

>[!NOTE]
>
>如果您希望跳过API练习，请随时通过与以下详细信息一起使用的用户界面方法创建CRM命名空间：
>
> 1. 作为 **[!UICONTROL 显示名称]**，使用 `Luma CRM Id`
> 1. 作为 **[!UICONTROL 身份符号]**，使用 `lumaCrmId`
> 1. 作为 **[!UICONTROL 类型]**，使用跨设备


让我们创建身份命名空间 `Luma CRM Id`:

1. 下载 [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) 至 `Luma Tutorial Assets` 文件夹
1. 将集合导入 [!DNL Postman]
1. 如果您在过去24小时内未发出请求，则授权令牌可能已过期。 打开请求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]**，然后选择 **发送** 请求新的JWT和访问令牌。
1. 选择请求 **[!UICONTROL Identity Service] > [!UICONTROL 身份命名空间] > [!UICONTROL 创建新身份命名空间].**
1. 将以下内容粘贴为 [!DNL Body] 请求：

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. 按 **发送** 按钮，你应该 **200 OK** 响应：

   ![身份命名空间](assets/identity-createUsingApi.png)

如果返回用户界面，您现在应会看到三个新的自定义命名空间：
![身份命名空间 ](assets/identity-newIdentities.png)


## 在架构中标记标识字段

现在，我们拥有了命名空间，接下来的步骤是更新我们的架构，以标记我们的身份字段。


### 为主标识标记XDM字段

需要与实时客户用户档案一起使用的每个架构都指定一个主标识。 并且所摄取的每个记录都必须具有该字段的值。

让我们将主标识添加到 `Luma Loyalty Schema`:

1. 打开 `Luma Loyalty Schema`
1. 选择 `Luma Identity profile field group`
1. 选择 `loyaltyId` 字段
1. 检查 **[!UICONTROL 身份]** 框
1. 检查 **[!UICONTROL 主标识]** 框，也
1. 选择 `Luma Loyalty Id` 命名空间 **[!UICONTROL 身份命名空间]** 下拉列表
1. 选择 **[!UICONTROL 应用]**
1. 选择 **[!UICONTROL 保存]**

   ![主标识 ](assets/identity-loyalty-primary.png)

对您的其他一些架构重复该过程：

1. 在 `Luma CRM Schema`，标记 `crmId` 字段作为主标识，使用 `Luma CRM Id` 命名空间
1. 在 `Luma Offline Purchase Events Schema`，标记 `loyaltyId` 字段作为主标识，使用 `Luma Loyalty Id` 命名空间
1. 在 `Luma Product Catalog Schema`，标记 `productSku` 字段作为主标识，使用 `Luma Product SKU` 命名空间

>[!NOTE]
>
>通过Web SDK收集的数据对模式中标记标识字段的典型实践是一个例外。 Web SDK使用身份映射来标记身份 *在实施端* 这样我们就能确定 `Luma Web Events Schema` 在Luma网站上实施Web SDK时。 在后面的课程中，我们将收集Experience Cloud访客ID(ECID)作为主ID，并将crmId作为辅助ID。

通过我们选择的主要身份，我们可以清楚地看到 `Luma CRM Schema` 可以连接到 `Luma Offline Purchase Events Schema` 因为两者都使用 `loyaltyId` 作为标识符。 但我们如何将线下购买与在线行为联系起来？ 如何对随产品目录一起购买的产品进行分类？ 我们将使用其他身份字段和架构关系。

<!--use a visual-->

### 为次标识标记XDM字段

可以将多个标识字段添加到架构。 非主标识通常称为次标识。 要将离线购买与在线行为关联，我们会将crmId作为辅助标识符添加到我们的 `Luma Loyalty Schema` 和更晚的Web事件数据。 让我们更新 `Luma Loyalty Schema`:

1. 打开 `Luma Loyalty Schema`
1. 选择 `Luma Identity Profile Field group`
1. 选择 `crmId` 字段
1. 检查 **[!UICONTROL 身份]** 框
1. 选择 `Luma CRM Id` 命名空间 **[!UICONTROL 身份命名空间]** 下拉列表
1. 选择 **[!UICONTROL 应用]** ，然后选择 **[!UICONTROL 保存]** 按钮以保存更改

   ![次标识](assets/identity-loyalty-secondaryId.png)

## 完成架构关系

现在，我们已标记了身份字段，接下来，我们可以完成Luma产品目录与事件架构之间架构关系的设置：

1. 打开 `Luma Offline Purchase Events Schema`
1. 选择 **[!UICONTROL 商务详细信息]** 字段组
1. 选择 **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** 字段
1. 检查 **[!UICONTROL 关系]** 框
1. 选择 `Luma Product Catalog Schema` 作为 **[!UICONTROL 参考模式]**
1. `Luma Product SKU` 应自动填充为 **[!UICONTROL 引用身份命名空间]**
1. 选择 **[!UICONTROL 应用]**
1. 选择 **[!UICONTROL 保存]**

   ![引用字段](assets/identity-offlinePurchase-relationship.png)

重复此过程，以在 `Luma Web Events Schema` 和 `Luma Product Catalog Schema`.

请注意，定义关系后，它会在 **[!UICONTROL 组合物]** 和 **[!UICONTROL 结构]** 模式编辑器的部分。

![架构编辑器中的关系可视化](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## 其他资源

* [Identity Service 文档](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hans)
* [Identity Service API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

既然我们的身份已经到位，我们可以 [创建数据集](create-datasets.md)!
