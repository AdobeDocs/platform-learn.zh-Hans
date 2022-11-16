---
title: 模式中的数据模型
seo-title: Model data in schemas | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 模式中的数据模型
description: 在本课程中，您将为Luma的数据建模为模式。 这是教程中最长的课程之一，所以请你喝杯水，然后系好安全带！
role: Data Architect
feature: Schemas
kt: 4348
thumbnail: 4348-model-data-in-schemas.jpg
exl-id: 317f1c39-7f76-4074-a246-ef19f044cb85
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 1%

---

# 模式中的数据模型

<!-- 60min -->
在本课程中，您将为Luma的数据建模为模式。 这是教程中最长的课程之一，所以请你喝杯水，然后系好安全带！

标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验数据模型(XDM)是一种旨在标准化客户体验数据并定义客户体验管理架构的工作。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它为用于与Platform服务通信的任何应用程序提供了通用结构和定义。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以便以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及为个性化目的表达客户属性。

XDM是基础框架，它允许Adobe Experience Cloud在Experience Platform的支持下，在适当的时间，通过适当的渠道向适当的人员提供适当的信息。 构建Experience Platform的方法， **XDM系统**，可操作供Platform服务使用的Experience Data Model模式。

<!--
This seems too lengthy. The video should suffice

Key terms:

* **Schema**: a representation of your data. A schema is comprised of a class and optional field groups and is used to create datasets. A schema includes behavioral attributes, timestamp, identity, attribute definitions, and relationships.
* **XDM Profile Class**: a common schema class used to represent record data
* **XDM ExperienceEvent Class**: a common schema class used to represent time-series data
* **Field group**: allows users to extend reusable fields that contain variables defining one or more attribute intended to be included in a schema or added to a class.
* **Standard Field group**: an open-source Field group built to conform to common industry standards, used to accelerate implementation and support repeatable services operating on the data
* **Data type**: a reusable object with properties in a hierarchical representation. These can be standard types or custom-defined defined types to describe your own data in your own way (for example, a collection of fields that you use to describe your products). Unlike Field groups, data types can be used in schemas regardless of the class.
* **Field**: a field is the lowest level element of a schema. Each field has a name for referencing and a type to identify the type of data that it contains. Field types can include, integer, number, string, Boolean and schema.
-->

**数据架构师** 将需要在本教程之外创建模式，但 **数据工程师** 将与Data Architect创建的架构密切配合。

在开始练习之前，请观看此简短视频，以详细了解模式和体验数据模型(XDM):
>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

>[!TIP]
>
> 为了更深入地了解Experience Platform中的数据建模，我们建议您参加课程 [使用XDM为您的客户体验数据建模](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)，可在Experience League上免费使用！

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--, specifically:

* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)-->


<!--
## Luma's goals
-->

## 通过UI创建忠诚度架构

在此练习中，我们将为Luma的忠诚度数据创建架构。

1. 转到Platform用户界面，并确保已选择您的沙盒。
1. 转到 **[!UICONTROL 模式]** 在左侧导航中
1. 选择 **[!UICONTROL 创建架构]** 按钮
1. 从下拉菜单中，选择 **[!UICONTROL XDM个人配置文件]**，因为我们将为单个客户的属性（点、状态等）建模。
   ![具有OOTB字段组的架构](assets/schemas-loyaltyCreateSchema.png)

### 添加标准字段组

接下来，系统将提示您向架构添加字段组。 必须使用组将所有字段添加到架构。 您可以从由Adobe提供的大量行业标准字段组中进行选择，也可以创建您自己的字段组。 在Experience Platform中开始建模您自己的数据时，最好熟悉Adobe提供的行业标准字段组。 尽可能地，最好使用它们，因为它们有时会支持下游服务，例如Customer AI、Attribution AI和Adobe Analytics。

使用您自己的数据时，一个重要步骤是确定应在平台中捕获哪些您自己的数据以及应如何建模。 本课程将更深入地讨论这一大主题 [使用XDM为您的客户体验数据建模](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm). 在本教程中，我将指导您完成一些预定模式的实施。

要添加字段组，请执行以下操作：

1. 在 **[!UICONTROL 添加字段组]** 模式窗口中，选择以下字段组：
   1. **[!UICONTROL 人口统计详细信息]** 对于基本客户数据（如名称和出生日期）
   1. **[!UICONTROL 个人联系详细信息]** 有关基本联系详细信息（如电子邮件地址和电话号码）
1. 您可以通过选择行右侧的图标来预览字段组中贡献的字段。
   ![选择标准字段组](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. 检查 **[!UICONTROL 行业]** > **[!UICONTROL 零售]** 框来显示特定于行业的字段组。
1. 选择 **[!UICONTROL 忠诚度]** 添加忠诚度计划字段。
1. 选择 **[!UICONTROL 添加字段组]** 将所有三个字段组添加到架构。
   ![将标准字段组添加到忠诚度架构](assets/schemas-loyalty-saveOotbMixins.png)


现在，需要一些时间来探索架构的当前状态。 字段组添加了与人员、其联系详细信息和忠诚度计划状态相关的标准字段。 在为自己公司的数据创建架构时，您可能会发现这两个字段组非常有用。 选择特定字段组行或选中字段组名称旁边的复选框，以查看可视化图表的更改方式。

要保存架构，请执行以下操作：

1. 选择架构的顶级节点。
1. 输入 `Luma Loyalty Schema` 作为 **[!UICONTROL 显示名称]**.
1. 选择&#x200B;**[!UICONTROL 保存]**。
   ![命名并保存架构](assets/schemas-loyalty-nameAndSave.png)

>[!NOTE]
>
>字段组是否为您未收集的数据点添加字段，这是可以的。 例如，“faxPhone”可能是Luma不收集数据的字段。 没关系。 仅因架构中定义了字段，并不意味着该架构的数据 *必须* 稍后被摄食。

### 添加自定义字段组

现在，让我们创建一个自定义字段组。

而忠诚度字段组包含 `loyaltyID` 字段中，Luma希望在单个组中管理其所有系统标识符，以帮助确保其架构之间的一致性。

必须在架构工作流中创建字段组。 要创建字段组，请执行以下操作：

1. 选择 **[!UICONTROL 添加]** 下 **[!UICONTROL 架构字段组]** 标题
   ![添加新字段组](assets/schemas-loyalty-addFieldGroup.png)
1. 选择 **[!UICONTROL 创建新字段组]**
1. 使用 `Luma Identity profile field group` 作为 **[!UICONTROL 显示名称]**
1. 使用 `system identifiers for XDM Individual Profile class` 作为 **[!UICONTROL 描述]**
1. 选择 **[!UICONTROL 添加字段组]**

   ![添加新字段组](assets/schemas-loyalty-nameFieldGroup.png)

新的空字段组将添加到您的架构中。 的 **[!UICONTROL +]** 按钮可用于向层次结构中的任意位置添加新字段。 在本例中，我们希望在根级别添加字段：

1. 选择 **[!UICONTROL +]** 架构名称旁边。 这会在租户ID命名空间下添加一个新字段，以管理自定义字段与任何标准字段之间的冲突。
1. 在 **[!UICONTROL 字段属性]** 侧栏添加新字段的详细信息：
   1. **[!UICONTROL 字段名称]**: `systemIdentifier`
   1. **[!UICONTROL 显示名称]**: `System Identifier`
   1. **[!UICONTROL 类型]**: **[!UICONTROL 对象]**
   1. 选择 **[!UICONTROL 应用]**

   ![添加新字段组](assets/schemas-loyalty-addSystemIdentifier.png)

现在，在 `systemIdentifier` 对象：

1. 第一个字段
   1. **[!UICONTROL 字段名称]**: `loyaltyId`
   1. **[!UICONTROL 显示名称：]** `Loyalty Id`
   1. **[!UICONTROL 类型]**: **[!UICONTROL 字符串]**
1. 第二个字段
   1. **[!UICONTROL 字段名称]**: `crmId`
   1. **[!UICONTROL 显示名称]**: `CRM Id`
   1. **[!UICONTROL 类型]**: **[!UICONTROL 字符串]**

您的新字段组应如下所示。 选择 **[!UICONTROL 保存]** 按钮来保存您的架构，但请保持架构处于打开状态，以供下一个练习使用。
![忠诚度字段组结束](assets/schemas-loyalty-identityFieldGroupComplete.png)

## 创建数据类型

字段组，如新 `Luma Identity profile field group`，可在其他架构中重复使用，从而允许您跨多个系统强制实施标准数据定义。 但它们只能被重复利用 _在共享类的架构中_，在本例中为XDM个人用户档案类。

数据类型是另一个可在架构中重用的多字段结构 _跨多个类_. 让我们转换新 `systemIdentifier` 对象转换为数据类型：

使用 `Luma Loyalty Schema` 仍然打开，选择 `systemIdentifier` 对象和选择  **[!UICONTROL 转换为新数据类型]**

![忠诚度字段组结束](assets/schemas-loyalty-convertToDataType.png)

如果您 **[!UICONTROL 取消]** 退出架构，然后导航到 **[!UICONTROL 数据类型]** 选项卡，则会看到新创建的数据类型。 我们将在课程的稍后部分使用此数据类型。

![忠诚度字段组结束](assets/schemas-loyalty-confirmDataType.png)


## 通过API创建CRM架构

现在，我们将使用API创建模式。

>[!TIP]
>
> 如果您希望跳过API练习，可以使用用户界面方法创建以下架构：
>
> 1. 使用 [!UICONTROL XDM个人配置文件] 类
> 1. 将其命名为 `Luma CRM Schema`
> 1. 使用以下字段组：人口统计详细信息、个人联系人详细信息和Luma身份配置文件字段组


首先，我们创建空架构：

1. Open [!DNL Postman]
1. 如果您在过去24小时内未发出请求，则授权令牌可能已过期。 打开请求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 选择 **发送** 请求新的JWT和访问令牌。
1. 打开环境变量并更改 **CONTAINER_ID** 从 `global` to `tenant`. 请记住，您必须使用 `tenant` 当您想要在Platform中与自己的自定义元素进行交互时，例如创建架构。
1. 选择 **保存**
   ![将CONTAINER_ID更改为租户](assets/schemas-crm-changeContainerId.png)
1. 打开请求 **[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. 打开 **正文** 选项卡，然后粘贴以下代码并选择 **发送** 以进行API调用。 此调用使用 `XDM Individual Profile` 基类：

   ```json
   {
     "type": "object",
     "title": "Luma CRM Schema",
     "description": "Schema for CRM data of Luma Retail ",
     "allOf": [{
       "$ref": "https://ns.adobe.com/xdm/context/profile"
     }]
   }
   ```

   >[!NOTE]
   >
   >此代码示例和后续代码示例中的命名空间引用(例如 `https://ns.adobe.com/xdm/context/profile`)，则可以将列表API调用与 **[!DNL CONTAINER_ID]** 并接受标头设置为正确的值。 部分用户也可以在用户界面中轻松访问。

1. 你应该得到 `201 Created` 响应
1. 复制 `meta:altId` 从响应主体。 我们稍后会在另一个练习中使用它。
   ![创建CRM架构](assets/schemas-crm-createSchemaCall.png)

1. 新架构应在用户界面中可见，但没有任何字段组
   ![创建CRM架构](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> 的 `meta:altId` 或架构id也可通过发出API请求来获取 **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]** 和 **[!UICONTROL CONTAINER_ID]** 设置为 `tenant` 和接受标头 `application/vnd.adobe.xdm+json`.

>[!TIP]
>
> 此调用的常见问题和可能的修复：
>
> * 无身份验证令牌：运行 **IMS:JWT通过用户令牌生成+身份验证** 调用以生成新令牌
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`:更新 **CONTAINER_ID** 环境变量 `global` to `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`:在Admin Console中验证用户权限


### 添加标准字段组

现在该将字段组添加到架构了：

1. 在 [!DNL Postman]，打开请求 **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. 在 **参数** 选项卡，粘贴 `meta:altId` 值 `SCHEMA_ID`
1. 打开“正文”选项卡并粘贴以下代码，然后选择 **发送** 以进行API调用。 此调用会将标准字段组添加到 `Luma CRM Schema`:

   ```json
   [{
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
       }
     },
     {
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
       }
     }
   ]
   ```

1. 您应该获得响应的200 OK状态，并且字段组应作为架构的一部分在UI中可见

   ![添加了标准字段组](assets/schemas-crm-addMixins.png)


### 添加自定义字段组

现在，让我们将 `Luma Identity profile field group` 到架构。 首先，我们需要使用列表API来查找新字段组的ID:

1. 打开请求 **[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. 选择 **发送** 用于检索帐户中所有自定义字段组的列表的按钮
1. 抓住 `$id` 值 `Luma Identity profile field group` （您的将与此屏幕截图中的值不同）
   ![检索字段组列表](assets/schemas-crm-getListOfMixins.png)
1. 打开请求 **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]** 再次
1. 的 **参数** 选项卡 `$id` 您的架构
1. 打开 **正文** 选项卡，并粘贴以下代码， `$ref` 值 `$id` 你自己 `Luma Identity profile field group`:

   ```json
   [{
     "op": "add",
     "path": "/allOf/-",
     "value": {
       "$ref": "REPLACE_WITH_YOUR_OWN_FIELD_GROUP_ID"
     }
   }]
   ```

1. 选择 **发送**

   ![添加标识字段组](assets/schemas-crm-addIdentityMixin.png)

通过检查API响应和界面中的，验证字段组是否已添加到架构中。

## 创建离线购买事件架构

现在，让我们基于 **[!UICONTROL XDM ExperienceEvent]** Luma的离线购买数据的类。 由于您现在已熟悉架构编辑器用户界面，因此我将减少说明中屏幕截图的数量：

1. 使用创建架构 **[!UICONTROL XDM ExperienceEvent]** 类
1. 添加标准字段组 **[!UICONTROL 商务详细信息]** 以捕获常见订单详细信息。 花几分钟时间探索里面的物体。
1. 搜索 `Luma Identity profile field group`. 它不可用！ 请记住，字段组已绑定到类，由于我们在此架构中使用不同的类，因此无法使用它。 我们需要为XDM ExperienceEvent类添加一个包含标识字段的新字段组。 我们的数据类型将使这变得非常简单！
1. 选择 **[!UICONTROL 创建新字段组]** 单选按钮
1. 输入 **[!UICONTROL 显示名称]** as `Luma Identity ExperienceEvent field group` ，然后选择 **[!UICONTROL 添加字段组]** 按钮
1. 确保 **[!UICONTROL +]** 按钮显示在 **[!UICONTROL 结构]** 部分，以便您能够添加新字段
1. 在 **[!UICONTROL 结构]** 选择 **[!UICONTROL +]** 在架构的顶级
1. 作为 **[!UICONTROL 字段名称]**，输入 `systemIdentifier`
1. 作为 **[!UICONTROL 显示名称]**，输入 `System Identifier`
1. 作为 **[!UICONTROL 类型]**，选择 **系统标识符** 这是您之前创建的自定义数据类型
1. 选择 **[!UICONTROL 应用]** 按钮
1. 命名架构 `Luma Offline Purchase Events Schema`
1. 选择 **[!UICONTROL 保存]** 按钮

请注意数据类型如何添加所有字段！

![将数据类型添加到字段组](assets/schemas-offlinePurchases-addDatatype.png)

此外，选择 **[!UICONTROL XDM ExperienceEvent]** 下 **[!UICONTROL 类]** 标题并检查本课贡献的一些字段。 请注意，使用XDM ExperienceEvent类时，需要_id和时间戳字段，因为在使用此架构时，必须为您摄取的每个记录填充这些字段：

![体验事件基础结构](assets/schemas-offlinePurchase-experienceEventbase.png)

## 创建Web事件模式

现在，我们将为Luma的网站数据再创建一个模式。 此时，您应该是创建模式的专家！ 使用这些属性构建以下架构

| 属性 | 值 |
|---------------|-----------------|
| 类 | XDM ExperienceEvent |
| 字段组 | AEP Web SDK ExperienceEvent Mixin |
| 字段组 | 消费者体验事件 |
| 架构名称 | Luma Web事件架构 |

选择 **[!UICONTROL 消费者体验事件]** 字段组。 此字段组包含商务和productListItems对象，这些对象也位于 [!UICONTROL 商务详细信息]. 的确 [!UICONTROL 消费者体验事件] 是其他几个标准字段组的组合，这些字段组也可单独使用。 [!UICONTROL AEP Web SDK ExperienceEvent Mixin] 字段组还包含其他字段组，包括 [!UICONTROL 消费者体验事件]. 幸运的是，它们完美地融合在一起。

请注意，我们未在 `Luma Identity ExperienceEvent field group` 到此模式。 这是因为Web SDK有不同的身份收集方式。 如果您选择 **[!UICONTROL XDM ExperienceEvent]** 类 **[!UICONTROL 组合物]** 在架构编辑器的部分中，您会注意到它添加的默认字段之一称为 **[!UICONTROL IdentityMap]**. [!DNL IdentityMap] 被各种Adobe应用程序用来链接到平台。 您将在流摄取课程中了解如何通过identityMap将身份发送到平台。


## 创建产品目录架构

通过使用  [!UICONTROL 商务详细信息] 和 [!UICONTROL 消费者体验事件] 字段组中，Luma会通过标准productListItems数据类型报告产品相关事件的一些详细信息。 但是，他们还有其他产品详细信息字段，要发送到Platform。 Luma不愿在其销售点和电子商务系统中捕获所有这些字段，而是希望直接从其产品目录系统中摄取这些字段。 “架构关系”允许您为分类或查找目的定义两个架构之间的关系。 Luma将使用关系对其产品详细信息进行分类。 我们将立即开始该过程，并在下一课程结束时完成该过程。

>[!NOTE]
>
>如果您是现有Analytics或Target客户，则使用架构关系对实体进行分类类似于SAINT分类或上传Recommendations产品目录

首先，我们必须使用自定义类为Luma的产品目录创建架构：

1. 选择 **[!UICONTROL 创建架构]** 按钮并选择 **[!UICONTROL 浏览]** 下拉菜单中的选项
   ![创建新架构](assets/schemas-newSchema-browseClasses.png)
1. 选择 **[!UICONTROL 创建新类]** 单选按钮
1. 将其命名为 `Luma Product Catalog Class`
1. 离开 **[!UICONTROL 行为]** as **[!UICONTROL 记录]**
1. 选择 **[!UICONTROL 分配类]** 按钮
   ![创建新类](assets/schemas-productClass.png)
1. 新建 [!UICONTROL 字段组] 调用 `Luma Product Catalog field group` ，其中包含以下字段：
   1. productName:产品名称：字符串
   1. productCategory:产品类别：字符串
   1. productColor:产品颜色：字符串
   1. productSku:产品SKU:字符串 |必需
   1. productSize:产品大小：字符串
   1. productPrice:产品价格：双精度
1. 命名架构 `Luma Product Catalog Schema` （请务必更新正确的字段，而不更新类名）
1. **[!UICONTROL 保存]** 架构

您的新架构应当如下所示。 请注意 `productSku` 字段 [!UICONTROL 必填字段] 部分：
![产品架构](assets/schemas-productSchema.png)

下一步是定义两个ExperienceEvent架构与 `Luma Product Catalog Schema`但是，在执行此操作之前，我们必须在下一课程中执行一些其他步骤。


## 其他资源

* [Experience Data Model(XDM)系统文档](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)
* [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


现在，您的模式可以 [映射标识](map-identities.md)!
