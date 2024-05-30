---
title: 在架构中对数据进行建模
seo-title: Model data in schemas | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 在架构中对数据进行建模
description: 在本课程中，您将将Luma的数据建模为架构。 这是教程中最长的课程之一，所以喝杯水吧！
role: Data Architect
feature: Schemas
jira: KT-4348
thumbnail: 4348-model-data-in-schemas.jpg
exl-id: 317f1c39-7f76-4074-a246-ef19f044cb85
source-git-commit: 8e470d8a0c9fee7389ac60a743431fe81012fa0f
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 1%

---

# 在架构中对数据进行建模

<!-- 60min -->
在本课程中，您将将Luma的数据建模为架构。 这是教程中最长的课程之一，所以喝杯水吧！

标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验数据模型(XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它提供通用结构和定义，供任何应用程序用于与Platform服务通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并表达客户属性以进行个性化。

XDM是一个基础框架，它允许Adobe Experience Cloud由Experience Platform提供支持，在正确的时间通过正确的渠道向正确的人员传递正确的信息。 构建Experience Platform所基于的方法， **XDM系统**，可将Experience Data Model架构可操作以供Platform服务使用。

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

**数据架构师** 将需要在本教程之外创建架构，但是 **数据工程师** 将与数据架构师创建的架构密切合作。

在开始练习之前，请观看此简短视频，详细了解架构和Experience Data Model (XDM)：
>[!VIDEO](https://video.tv.adobe.com/v/27105?learn=on)

>[!TIP]
>
> 要更深入地探讨Experience Platform中的数据建模，我们建议您参加此课程 [使用XDM对您的客户体验数据进行建模](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)，可在Experience League上免费使用！

## 所需的权限

在 [配置权限](configure-permissions.md) 课程：您已设置完成本课程所需的所有访问控制。

<!--, specifically:

* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)-->


<!--
## Luma's goals
-->

## 通过UI创建忠诚度模式

在本练习中，我们将为Luma的忠诚度数据创建一个架构。

1. 转到Platform用户界面，并确保已选择您的沙盒。
1. 转到 **[!UICONTROL 架构]** 在左侧导航中。
1. 选择 **[!UICONTROL 创建架构]** 按钮。
   ![具有OOTB字段组的架构](assets/schemas-loyaltyCreateSchema.png)

1. 在创建模式工作流中，选择 **[!UICONTROL 个人资料]** 作为架构的基类，因为我们将对单个客户的属性（点、状态等）进行建模。
1. 选择 **[!UICONTROL 下一个]**.
   ![选择基类](assets/schemas-loyaltySelectBaseClass.png)

1. 输入 `Luma Loyalty Schema` 在 **[!UICONTROL 架构显示名称]** 文本字段。 在以下画布中，您还可以查看和验证所选类提供的基本架构结构。
1. 选择 **[!UICONTROL 完成]** 以创建您的架构。
   ![完成创建忠诚度模式](assets/schemas-loyaltyFinishSchemaCreation.png)

### 添加标准字段组

创建架构后，您将被重定向到架构编辑器，您可以在其中向架构添加字段。 您可以直接将单个字段添加到架构或使用字段组。 请务必注意，所有单个字段仍与类或字段组相关联。 您可以从Adobe提供的大量行业标准字段组中进行选择，也可以创建自己的字段组。 当您开始在Experience Platform中对自己的数据进行建模时，最好熟悉Adobe提供的行业标准字段组。 最佳实践是尽可能使用它们，因为它们有时支持下游服务，例如客户人工智能、Attribution AI和Adobe Analytics。

处理您自己的数据时，重要的一步是确定应在Platform中捕获您自己的哪些数据以及应如何对其进行建模。 本课程将更深入地讨论这个大主题 [使用XDM对您的客户体验数据进行建模](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm). 在本教程中，我将指导您完成一些预先确定的架构的实施。

要添加字段组：

1. 选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 字段组]** 标题。
   ![添加新字段组](assets/schemas-loyalty-addFieldGroup.png)
1. 在 **[!UICONTROL 添加字段组]** 模式窗口中，选择以下字段组：
   1. **[!UICONTROL 人口统计详细信息]** 获取名称和出生日期等基本客户数据
   1. **[!UICONTROL 个人联系人详细信息]** 以了解基本联系详细信息，如电子邮件地址和电话号码
1. 您可以通过选择行右侧的图标，预览在字段组中贡献的字段。
   ![选择标准字段组](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. 查看 **[!UICONTROL 行业]** > **[!UICONTROL 零售]** 框以显示特定行业的字段组。
1. 选择 **[!UICONTROL 忠诚度详细信息]** 以添加忠诚度计划字段。
1. 选择 **[!UICONTROL 添加字段组]** 以将所有三个字段组添加到该架构。
   ![将标准字段组添加到忠诚度模式](assets/schemas-loyalty-saveOotbMixins.png)


现在，请花些时间探索架构的当前状态。 字段组已添加与人员、其联系人详细信息和忠诚度计划状态相关的标准字段。 在为自己公司的数据创建架构时，您可能会发现这两个字段组很有用。 选择特定的字段组行，或选中字段组名称旁边的复选框，以查看可视化图表的更改情况。

要保存架构，请选择 **[!UICONTROL 保存]**.
![保存架构](assets/schemas-loyalty-saveSchema.png)

>[!NOTE]
>
>如果字段组为未收集的数据点添加字段，这没有关系。 例如，“faxPhone”可能是Luma不为其收集数据的字段。 没关系。 仅仅因为在架构中定义了字段并不意味着它的数据是 *必须* 稍后摄取。 您还可以从架构中删除字段。

### 添加自定义字段组

现在，让我们创建一个自定义字段组。

而忠诚度字段组包含 `loyaltyID` 字段，Luma希望在一个组中管理其所有系统标识符，以确保其架构的一致性。

必须在架构工作流中创建字段组。 您可以：

* 先向架构中添加新的自定义字段，然后创建自定义字段组，或
* 先创建自定义字段组，然后向其添加字段。

在本教程中，我们首先会创建一个自定义字段组。

要创建字段组，请执行以下操作：

1. 选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 架构字段组]** 标题
   ![添加新字段组](assets/schemas-loyalty-addFieldGroup.png)
1. 选择 **[!UICONTROL 创建新字段组]**
1. 使用 `Luma Identity profile field group` 作为 **[!UICONTROL 显示名称]**
1. 使用 `system identifiers for XDM Individual Profile class` 作为 **[!UICONTROL 描述]**
1. 选择 **[!UICONTROL 添加字段组]**
   ![添加新字段组](assets/schemas-loyalty-nameFieldGroup.png)

新的空字段组将会添加到您的架构中。此 **[!UICONTROL +]** 按钮可用于向层次结构中的任何位置添加新字段。 在本例中，我们要在根级别添加字段：

1. 选择 **[!UICONTROL +]** 位于架构名称旁边。 这会在您的租户ID命名空间下添加一个新字段，以管理自定义字段和任何标准字段之间的冲突。
1. 在 **[!UICONTROL 字段属性]** 侧栏添加了新字段的详细信息：
   1. **[!UICONTROL 字段名称]**： `systemIdentifier`
   1. **[!UICONTROL 显示名称]**： `System Identifier`
   1. **[!UICONTROL 类型]**： **[!UICONTROL 对象]**
   1. 在 **[!UICONTROL 字段组]** 下拉菜单选择 **Luma身份配置文件字段组** 我们创造的。
      ![添加新字段组](assets/schemas-loyalty-addSystemIdentifier.png)
   1. 选择 **[!UICONTROL 应用]**
      ![应用新字段属性](assets/schemas-loyalty-applySystemIdentifier.png)

现在，在 `systemIdentifier` 对象：

1. 第一个字段
   1. **[!UICONTROL 字段名称]**： `loyaltyId`
   1. **[!UICONTROL 显示名称：]** `Loyalty Id`
   1. **[!UICONTROL 类型]**： **[!UICONTROL 字符串]**
1. 第二个字段
   1. **[!UICONTROL 字段名称]**： `crmId`
   1. **[!UICONTROL 显示名称]**： `CRM Id`
   1. **[!UICONTROL 类型]**： **[!UICONTROL 字符串]**

您的新字段组应如下所示。 选择 **[!UICONTROL 保存]** 按钮以保存架构，但保持架构处于打开状态，以供下一个练习使用。
![忠诚度字段组完成](assets/schemas-loyalty-identityFieldGroupComplete.png)

## 创建数据类型

字段组，如您的新组 `Luma Identity profile field group`，可在其他架构中重用，从而允许您跨多个系统实施标准数据定义。 但它们只能重复使用 _在共享类的架构中_，在本例中为XDM Individual Profile类。

数据类型是另一个可在架构中重用的多字段结构 _跨多个类_. 让我们转换新的 `systemIdentifier` 对象转换为数据类型：

使用 `Luma Loyalty Schema` 仍然打开，请选择 `systemIdentifier` 对象并选择  **[!UICONTROL 转换为新数据类型]**

![忠诚度字段组完成](assets/schemas-loyalty-convertToDataType.png)

如果您 **[!UICONTROL 取消]** 退出架构并导航到 **[!UICONTROL 数据类型]** 选项卡，您将看到新创建的数据类型。 我们将在本课程的后面部分使用此数据类型。

![忠诚度字段组完成](assets/schemas-loyalty-confirmDataType.png)


## 通过API创建CRM架构

现在，我们将使用API创建架构。

>[!TIP]
>
> 如果您希望跳过API练习，则可以使用用户界面方法创建以下架构：
>
> 1. 使用 [!UICONTROL 个人资料] 类
> 1. 将其命名为 `Luma CRM Schema`
> 1. 使用以下字段组：“人口统计详细信息”、“个人联系人详细信息”和“Luma身份配置文件”字段组

首先，创建空架构：

1. 打开 [!DNL Postman]
1. 如果您没有访问令牌，请打开请求 **[!DNL OAuth: Request Access Token]** 并选择 **发送** 以请求新的访问令牌。
1. 打开您的环境变量并更改的值 **CONTAINER_ID** 从 `global` 到 `tenant`. 请记住，您必须使用 `tenant` 当您想要与Platform中的自定义元素交互时，例如创建架构。
1. 选择 **保存**
   ![将CONTAINER_ID更改为租户](assets/schemas-crm-changeContainerId.png)
1. 打开请求 **[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. 打开 **正文** 制表符并粘贴以下代码，然后选择 **发送** 进行API调用。 此调用使用相同的方法创建新架构 `XDM Individual Profile` 基类：

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
   >此代码和后续代码示例中的命名空间引用(例如 `https://ns.adobe.com/xdm/context/profile`)，可以通过使用列表API调用获取 **[!DNL CONTAINER_ID]** 和接受标头设置为正确的值。 部分内容还可在用户界面中轻松访问。

1. 您应该获得一个 `201 Created` 响应
1. 复制 `meta:altId` 来自响应正文。 我们稍后将在另一个练习中使用它。
   ![创建CRM架构](assets/schemas-crm-createSchemaCall.png)

1. 新架构应在用户界面中可见，但不包含任何字段组
   ![创建CRM架构](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> 此 `meta:altId` 或模式ID也可以通过发出API请求来获取 **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]** 使用 **[!UICONTROL CONTAINER_ID]** 设置为 `tenant` 和接受标头 `application/vnd.adobe.xdm+json`.

>[!TIP]
>
> 此调用的常见问题以及可能的修复：
>
> * 无身份验证令牌：运行 **Oauth：请求访问令牌** 请求生成新令牌
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`：更新 **CONTAINER_ID** 环境变量来源 `global` 到 `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`：在Admin Console中验证您的用户权限

### 添加标准字段组

现在可以将字段组添加到架构中：

1. 在 [!DNL Postman]，打开请求 **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. 在 **参数** 选项卡，粘贴 `meta:altId` 上次响应中的值，作为 `SCHEMA_ID`
1. 打开正文选项卡，粘贴以下代码并选择 **发送** 进行API调用。 此调用会将标准字段组添加到 `Luma CRM Schema`：

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

1. 您应该会为响应获得“200 OK”状态，并且字段组应该作为架构的一部分显示在UI中

   ![已添加标准字段组](assets/schemas-crm-addMixins.png)


### 添加自定义字段组

现在，让我们添加我们的 `Luma Identity profile field group` 到架构中。 首先，我们需要使用列表API查找新字段组的ID：

1. 打开请求 **[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. 选择 **发送** 按钮以检索您帐户中所有自定义字段组的列表
1. 抓住 `$id` 的值 `Luma Identity profile field group` （您的值与此屏幕快照中的值不同）
   ![检索字段组列表](assets/schemas-crm-getListOfMixins.png)
1. 打开请求 **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]** 再次
1. 此 **参数** 选项卡仍应具有 `$id` 架构的
1. 打开 **正文** 制表符并粘贴以下代码，替换 `$ref` 带有的值 `$id` 您自己的 `Luma Identity profile field group`：

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
   ![添加身份字段组](assets/schemas-crm-addIdentityMixin.png)

通过检查API响应和界面中的字段组，验证该字段组是否已添加到架构中。

## 创建离线购买事件架构

现在，让我们根据 **[!UICONTROL 体验事件]** 类，用于Luma的离线购买数据。 由于您现在已熟悉架构编辑器用户界面，因此我将减少说明中的屏幕截图数量：

1. 创建架构，使用 **[!UICONTROL 体验事件]** 类。
1. 命名您的架构 `Luma Offline Purchase Events Schema`.
1. 添加标准字段组 **[!UICONTROL Commerce详细信息]** 以捕获常见订单详细信息。 花几分钟研究一下里面有哪些东西。
1. 搜索 `Luma Identity profile field group`. 不可用！ 请记住，字段组与类相关联，由于我们对此架构使用不同的类，因此我们无法使用它。 我们需要为包含标识字段的XDM ExperienceEvent类添加新字段组。 我们的数据类型会使其变得非常简单！
1. 选择 **[!UICONTROL 创建新字段组]** 单选按钮
1. 输入 **[!UICONTROL 显示名称]** 作为 `Luma Identity ExperienceEvent field group` 并选择 **[!UICONTROL 添加字段组]** 按钮
1. 选择架构名称旁边的 **[!UICONTROL +]**。
1. 作为 **[!UICONTROL 字段名称]**，输入 `systemIdentifier`.
1. 作为 **[!UICONTROL 显示名称]**，输入 `System Identifier`.
1. 作为 **[!UICONTROL 类型]**，选择 **系统标识符** 这是您之前创建的自定义数据类型。
1. 作为 **[!UICONTROL 字段组]** 选择 **Luma Identity ExperienceEvent字段组**.
1. 选择 **[!UICONTROL 应用]** 按钮。
1. 选择 **[!UICONTROL 保存]** 按钮。

请注意数据类型如何添加所有字段！

![将数据类型添加到字段组](assets/schemas-offlinePurchases-addDatatype.png)

此外，选择 **[!UICONTROL XDM ExperienceEvent]** 在 **[!UICONTROL 类]** 标题并检查由此类贡献的某些字段。 请注意，使用XDM ExperienceEvent类时需要_id和时间戳字段，使用此架构时摄取的每个记录都必须填充这些字段：

![体验事件基本结构](assets/schemas-offlinePurchase-experienceEventbase.png)

## 创建Web事件架构

现在，我们将为Luma的网站数据再创建一个架构。 此时，您应该成为创建架构的专家！ 使用这些属性构建以下架构

| 属性 | 值 |
|---------------|-----------------|
| 类 | 体验事件 |
| 架构名称 | Luma Web事件架构 |
| 字段组 | AEP Web SDK ExperienceEvent |
| 字段组 | 使用者体验事件 |

选择 **[!UICONTROL 使用者体验事件]** 字段组。 此字段组包含同时位于以下位置的commerce和productListItems对象 [!UICONTROL Commerce详细信息]. 的确 [!UICONTROL 使用者体验事件] 是另外几个标准字段组的组合，这些标准字段组也可单独使用。 [!UICONTROL AEP Web SDK ExperienceEvent] 字段组还包含其他字段组，包括中的一些相同的字段组 [!UICONTROL 使用者体验事件]. 幸运的是，他们完美地融合在一起。

请注意，我们没有添加 `Luma Identity ExperienceEvent field group` 到此架构。 这是因为Web SDK具有不同的身份收集方式。 如果您选择 **[!UICONTROL XDM ExperienceEvent]** 中的类 **[!UICONTROL 合成]** 架构编辑器部分中，您会注意到它默认添加的其中一个字段名为 **[!UICONTROL Identitymap]**. [!DNL IdentityMap] 供各种Adobe应用程序用于链接到Platform。 您将在流摄取课程中看到如何通过identityMap将身份发送到Platform。


## 创建产品目录架构

通过使用  [!UICONTROL Commerce详细信息] 和 [!UICONTROL 使用者体验事件] 字段组，Luma通过标准的productListItems数据类型报告产品相关事件的一些详细信息。 但是，他们还希望将其他产品详细信息字段发送到Platform。 与其在销售点和电子商务系统中捕获所有这些字段，Luma更愿意直接从他们的产品目录系统中摄取这些字段。 “架构关系”允许您定义两个架构之间的关系，以进行分类或查找。 Luma将使用关系对其产品详细信息进行分类。 我们将立即开始此过程，并在下一课结束时完成此过程。

>[!NOTE]
>
>如果您是现有Analytics或Target客户，则对具有架构关系的实体进行分类类似于SAINT分类或上传Recommendations的产品目录

首先，我们必须使用自定义类为Luma的产品目录创建架构：

1. 选择 **[!UICONTROL 创建架构]** 按钮。
1. 在创建模式工作流中，选择 **[!UICONTROL 其他]** 选项。
   ![创建新架构](assets/schemas-newSchema-browseClasses.png)
1. 选择 **[!UICONTROL 创建类]** 按钮
1. 将其命名为 `Luma Product Catalog Class`
1. 离开 **[!UICONTROL 行为]** 作为 **[!UICONTROL 记录]**
1. 选择 **[!UICONTROL 创建]** 按钮。
   ![创建新类](assets/schemas-productClass.png)
1. 此 **Luma产品目录类** 创建的将出现在下面的“类”表中。 确保已选择类，然后选择 **[!UICONTROL 下一个]**.
   ![已添加新类](assets/schemas-productClassSelected.png)
1. 命名架构 `Luma Product Catalog Schema`.
1. 新建 [!UICONTROL 字段组] 已调用 `Luma Product Catalog field group` 包含以下字段：
   1. productName：产品名称：字符串
   1. productCategory： Product类别：字符串
   1. productColor： Product Color：字符串
   1. productSku： Product SKU：字符串 | 必填
   1. productSize： Product Size：字符串
   1. productPrice： Product Price： Double
1. **[!UICONTROL 保存]** 架构

您的新架构应如下所示。 请注意 `productSku` 字段中列出 [!UICONTROL 必填字段] 部分：
![产品架构](assets/schemas-productSchema.png)

下一步是定义两个ExperienceEvent架构与 `Luma Product Catalog Schema`但是，在我们可以执行此操作之前，我们必须在下一个课程中执行一些其他步骤。


## 其他资源

* [Experience Data Model (XDM)系统文档](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)
* [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


现在您已拥有架构，您可以 [映射身份](map-identities.md)！
