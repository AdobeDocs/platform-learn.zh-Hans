---
title: 映射身份标识
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 映射身份标识
description: 在本课程中，我们将创建身份命名空间并将身份字段添加到架构中。
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: 73645b8b088cfdfe6f256c187b3c510dcc2386fc
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 6%

---

# 映射身份标识

<!-- 30 min-->

在本课程中，我们将创建身份命名空间并将身份字段添加到架构中。 完成此操作后，我们还将能够完成上一课程中的架构关系。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。 身份字段和命名空间是将不同数据源连接在一起的粘合剂，可构建360度实时客户档案。

**数据架构师**&#x200B;需要在本教程之外映射身份。

在开始练习之前，请观看此简短视频，了解有关Adobe Experience Platform中标识的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/3422769?learn=on&enablevpops&captions=chi_hans)

>[!NOTE]
>
>只有在构建实时客户配置文件时，才需要填写身份字段。 如果您只将数据摄取到数据湖中，则不需要使用CSV。

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## 所需的权限

在[配置权限](configure-permissions.md)课程中，您已设置完成本课程所需的所有访问控制。

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 创建身份命名空间

在本练习中，我们将为Luma的自定义身份字段`loyaltyId`、`crmId`和`productSku`创建身份命名空间。 身份标识命名空间在构建实时客户轮廓方面发挥着关键作用，因为同一命名空间的两个匹配值会让两个数据源形成身份标识图。


### 在UI中创建命名空间

让我们首先为Luma忠诚度模式创建命名空间：

1. 在Platform用户界面中，转到左侧导航中的&#x200B;**[!UICONTROL 标识]**
1. 您会发现有多个现成的身份命名空间可用。 选择&#x200B;**[!UICONTROL 创建身份命名空间]**&#x200B;按钮
1. 提供详细信息，如下所示

   | 字段 | 值 |
   |---------------|-----------|
   | 显示名称 | Luma忠诚度Id |
   | 身份标识符号 | lumaLoyaltyId |
   | 类型 | 跨设备 |

1. 选择&#x200B;**[!UICONTROL 创建]**

   ![创建命名空间](assets/identity-createNamespace.png)

现在，为Luma产品目录架构设置另一个命名空间，并提供以下详细信息：

| 字段 | 值 |
|---------------|-----------|
| 显示名称 | Luma产品SKU |
| 身份标识符号 | lumaProductSKU |
| 类型 | 非人员标识符 |



## 使用API创建身份命名空间

我们将通过API创建我们的CRM命名空间。

>[!NOTE]
>
>如果您希望跳过API练习，请随时通过您使用的用户界面方法创建CRM命名空间，并提供以下详细信息：
>
> 1. 作为&#x200B;**[!UICONTROL 显示名称]**，使用`Luma CRM Id`
> 1. 作为&#x200B;**[!UICONTROL 身份符号]**，使用`lumaCrmId`
> 1. 作为&#x200B;**[!UICONTROL 类型]**，使用跨设备

让我们创建身份命名空间`Luma CRM Id`：

1. 将[Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json)下载到`Luma Tutorial Assets`文件夹
1. 将集合导入[!DNL Postman]
1. 如果您没有访问令牌，请打开请求&#x200B;**[!DNL OAuth: Request Access Token]**&#x200B;并选择&#x200B;**发送**&#x200B;以请求新的访问令牌。
1. 选择请求&#x200B;**[!UICONTROL 身份服务] > [!UICONTROL 身份命名空间] > [!UICONTROL 创建新的身份命名空间]。**
1. 将以下内容粘贴为请求的[!DNL Body]：

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. 按&#x200B;**发送**&#x200B;按钮，您应会收到&#x200B;**200 OK**&#x200B;响应：

   ![身份标识命名空间](assets/identity-createUsingApi.png)

如果您返回用户界面，现在应会看到三个新的自定义命名空间：
![身份命名空间](assets/identity-newIdentities.png)


## 为架构中的标识字段设置标签

现在，我们有了命名空间，下一步是更新架构以标记身份字段。


### 为主要标识的XDM字段添加标签

需要为与Real-time Customer Profile一起使用的每个架构指定主标识。 并且每个摄取的记录都必须具有该字段的值。

让我们向`Luma Loyalty Schema`添加一个主要身份：

1. 打开`Luma Loyalty Schema`
1. 选择`Luma Identity profile field group`
1. 选择`loyaltyId`字段
1. 选中&#x200B;**[!UICONTROL 标识]**&#x200B;框
1. 同时选中&#x200B;**[!UICONTROL 主标识]**&#x200B;框
1. 从&#x200B;**[!UICONTROL 身份命名空间]**&#x200B;下拉列表中选择`Luma Loyalty Id`命名空间
1. 选择&#x200B;**[!UICONTROL 应用]**
1. 选择&#x200B;**[!UICONTROL 保存]**

   ![主要身份](assets/identity-loyalty-primary.png)

对您的其他某些架构重复该过程：

1. 在`Luma CRM Schema`中，使用`Luma CRM Id`命名空间将`crmId`字段标记为主标识
1. 在`Luma Offline Purchase Events Schema`中，使用`Luma Loyalty Id`命名空间将`loyaltyId`字段标记为主标识
1. 在`Luma Product Catalog Schema`中，使用`Luma Product SKU`命名空间将`productSku`字段标记为主标识

>[!NOTE]
>
>通过Web SDK收集的数据是架构中标记身份字段的典型实践的例外。 Web SDK使用标识映射来标记实施端&#x200B;*上的标识*，因此我们将在Luma网站上实施Web SDK时确定`Luma Web Events Schema`的标识。 在稍后的课程中，我们将将Experience Cloud访客ID (ECID)收集为主要ID，将crmId收集为次要ID。

通过选择主要身份，可以清楚地了解`Luma Loyalty Schema`如何连接到`Luma Offline Purchase Events Schema`，因为它们都使用loyaltyId作为标识符。 但是，CRM如何连接到离线购买事件？ 如何将离线购买与在线行为相关联？ 我们如何对随产品目录一起购买的产品进行分类？ 我们将使用其他标识字段和架构关系。

<!--use a visual-->

### 为辅助标识标记XDM字段

可以将多个标识字段添加到架构。 非主标识通常称为辅助标识。 要将离线购买与在线行为关联，我们将将crmId作为辅助标识符添加到`Luma Loyalty Schema`中，并稍后添加到Web事件数据中。 让我们更新`Luma Loyalty Schema`：

1. 打开`Luma Loyalty Schema`
1. 选择`Luma Identity Profile Field group`
1. 选择`crmId`字段
1. 选中&#x200B;**[!UICONTROL 标识]**&#x200B;框
1. 从&#x200B;**[!UICONTROL 身份命名空间]**&#x200B;下拉列表中选择`Luma CRM Id`命名空间
1. 选择&#x200B;**[!UICONTROL 应用]**，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;按钮以保存更改

   ![辅助标识](assets/identity-loyalty-secondaryId.png)

## 完成架构关系

现在，我们对身份字段进行了标记，我们可以完成Luma产品目录与事件架构之间的架构关系设置：

1. 打开`Luma Offline Purchase Events Schema`
1. 选择&#x200B;**[!UICONTROL Commerce详细信息]**&#x200B;字段组
1. 选择&#x200B;**[!UICONTROL productListItems]** > **[!UICONTROL SKU]**&#x200B;字段
1. 检查&#x200B;**[!UICONTROL 关系]**&#x200B;框
1. 选择`Luma Product Catalog Schema`作为&#x200B;**[!UICONTROL 引用架构]**
1. `Luma Product SKU`应自动填充为&#x200B;**[!UICONTROL 引用标识命名空间]**
1. 选择&#x200B;**[!UICONTROL 应用]**
1. 选择&#x200B;**[!UICONTROL 保存]**

   ![引用字段](assets/identity-offlinePurchase-relationship.png)

重复此过程以创建`Luma Web Events Schema`和`Luma Product Catalog Schema`之间的关系。

请注意，在定义关系后，它在架构编辑器的&#x200B;**[!UICONTROL 构成]**&#x200B;和&#x200B;**[!UICONTROL 结构]**&#x200B;部分都指示了。

架构编辑器中的![关系可视化图表](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## 其他资源

* [Identity Service文档](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hans)
* [标识服务API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

现在，我们的身份已准备就绪，我们可以[创建数据集](create-datasets.md)！
