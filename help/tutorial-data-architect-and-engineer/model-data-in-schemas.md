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
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 1%

---

# 在架构中对数据进行建模

<!-- 60min -->
在本课程中，您将将Luma的数据建模为架构。 这是教程中最长的课程之一，所以喝杯水吧！

标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验数据模型(XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它提供通用结构和定义，供任何应用程序用于与Platform服务通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并表达客户属性以进行个性化。

XDM是一个基础框架，它允许由Experience Platform提供支持的Adobe Experience Cloud在正确的时间通过正确的渠道向正确的人员传递正确的信息。 构建Experience Platform所基于的方法&#x200B;**XDM System**&#x200B;可使Platform服务使用的Experience Data Model架构可操作化。

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

**数据架构师**&#x200B;需要在本教程之外创建架构，但&#x200B;**数据工程师**&#x200B;将与数据架构师创建的架构密切合作。

在开始练习之前，请观看此简短视频，详细了解架构和Experience Data Model (XDM)：
>[!VIDEO](https://video.tv.adobe.com/v/27105?learn=on&enablevpops)

>[!TIP]
>
> 若要在Experience Platform中更深入地研究数据建模，我们建议观看可在Experience League上免费使用的播放列表[使用XDM对您的客户体验数据进行建模](https://experienceleague.adobe.com/zh-hans/playlists/experience-platform-model-your-customer-experience-data-with-xdm)！

## 所需的权限

在[配置权限](configure-permissions.md)课程中，您已设置完成本课程所需的所有访问控制。

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
1. 在左侧导航中转到&#x200B;**[!UICONTROL 架构]**。
1. 选择右上方的&#x200B;**[!UICONTROL 创建架构]**&#x200B;按钮。
   具有OOTB字段组的![架构](assets/schemas-loyaltyCreateSchema.png)

1. 在创建架构工作流中，选择&#x200B;**[!UICONTROL 个人资料]**&#x200B;作为架构的基类，因为我们将为单个客户的属性（点、状态等）建模。
1. 选择&#x200B;**[!UICONTROL 下一步]**。
   ![选择基类](assets/schemas-loyaltySelectBaseClass.png)

1. 在&#x200B;**[!UICONTROL 架构显示名称]**&#x200B;文本字段中输入`Luma Loyalty Schema`。 在以下画布中，您还可以查看和验证所选类提供的基本架构结构。
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建您的架构。
   ![完成创建忠诚度架构](assets/schemas-loyaltyFinishSchemaCreation.png)

### 添加标准字段组

创建架构后，您将被重定向到架构编辑器，您可以在其中向架构添加字段。 您可以直接将单个字段添加到架构或使用字段组。 请务必注意，所有单个字段仍与类或字段组相关联。 您可以从Adobe提供的大量行业标准字段组中进行选择，也可以创建自己的字段组。 当您开始在Experience Platform中对自己的数据进行建模时，最好熟悉Adobe提供的行业标准字段组。 最佳实践是尽可能使用它们，因为它们有时支持下游服务，例如客户人工智能、归因人工智能和Adobe Analytics。

处理您自己的数据时，重要的一步是确定应在Platform中捕获您自己的哪些数据以及应如何对其进行建模。 播放列表[使用XDM对您的客户体验数据进行建模](https://experienceleague.adobe.com/zh-hans/playlists/experience-platform-model-your-customer-experience-data-with-xdm)中将更深入地讨论这个大主题。 在本教程中，我将指导您完成一些预先确定的架构的实施。

要添加字段组：

1. 在&#x200B;**[!UICONTROL 字段组]**&#x200B;标题下选择&#x200B;**[!UICONTROL 添加]**。
   ![添加新字段组](assets/schemas-loyalty-addFieldGroup.png)
1. 在&#x200B;**[!UICONTROL 添加字段组]**&#x200B;模式中，选择以下字段组：
   1. **[!UICONTROL 人口统计详细信息]**，了解名称和出生日期等基本客户数据
   1. **[!UICONTROL 个人联系人详细信息]**，了解电子邮件地址和电话号码等基本联系人详细信息
1. 您可以通过选择行右侧的图标，预览在字段组中贡献的字段。
   ![选择标准字段组](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. 选中&#x200B;**[!UICONTROL Industry]** > **[!UICONTROL Retail]**&#x200B;框以公开特定于行业的字段组。
1. 选择&#x200B;**[!UICONTROL 忠诚度详细信息]**&#x200B;以添加忠诚度计划字段。
1. 选择&#x200B;**[!UICONTROL 添加字段组]**&#x200B;以将所有三个字段组添加到架构。
   ![将标准字段组添加到忠诚度架构](assets/schemas-loyalty-saveOotbMixins.png)


现在，请花些时间探索架构的当前状态。 字段组已添加与人员、其联系人详细信息和忠诚度计划状态相关的标准字段。 在为自己公司的数据创建架构时，您可能会发现这两个字段组很有用。 选择特定的字段组行，或选中字段组名称旁边的复选框，以查看可视化图表的更改情况。

要保存架构，请选择&#x200B;**[!UICONTROL 保存]**。
![保存架构](assets/schemas-loyalty-saveSchema.png)

>[!NOTE]
>
>如果字段组为未收集的数据点添加字段，这没有关系。 例如，“faxPhone”可能是Luma不为其收集数据的字段。 没关系。 仅仅因为在架构中定义了字段并不意味着以后必须&#x200B;*摄取该字段的数据*。 您还可以从架构中删除字段。

### 添加自定义字段组

现在，让我们创建一个自定义字段组。

虽然忠诚度字段组包含`loyaltyID`字段，但Luma希望在一个组中管理其所有系统标识符，以确保其架构的一致性。

必须在架构工作流中创建字段组。 您可以：

* 先向架构中添加新的自定义字段，然后创建自定义字段组，或
* 先创建自定义字段组，然后向其添加字段。

在本教程中，我们首先会创建一个自定义字段组。

要创建字段组，请执行以下操作：

1. 在&#x200B;**[!UICONTROL 架构字段组]**&#x200B;标题下选择&#x200B;**[!UICONTROL 添加]**
   ![添加新字段组](assets/schemas-loyalty-addFieldGroup.png)
1. 选择&#x200B;**[!UICONTROL 创建新字段组]**
1. 使用`Luma Identity profile field group`作为&#x200B;**[!UICONTROL 显示名称]**
1. 使用`system identifiers for XDM Individual Profile class`作为&#x200B;**[!UICONTROL 描述]**
1. 选择&#x200B;**[!UICONTROL 添加字段组]**
   ![添加新字段组](assets/schemas-loyalty-nameFieldGroup.png)

新的空字段组将会添加到您的架构中。**[!UICONTROL +]**&#x200B;按钮可用于向层次结构中的任何位置添加新字段。 在本例中，我们要在根级别添加字段：

1. 选择架构名称旁边的&#x200B;**[!UICONTROL +]**。 这会在您的租户ID命名空间下添加一个新字段，以管理自定义字段和任何标准字段之间的冲突。
1. 在&#x200B;**[!UICONTROL 字段属性]**&#x200B;侧边栏中添加新字段的详细信息：
   1. **[!UICONTROL 字段名称]**： `systemIdentifier`
   1. **[!UICONTROL 显示名称]**： `System Identifier`
   1. **[!UICONTROL 类型]**：**[!UICONTROL 对象]**
   1. 在&#x200B;**[!UICONTROL 字段组]**&#x200B;下拉列表中，选择我们创建的&#x200B;**Luma标识配置文件字段组**。

      ![添加新字段组](assets/schemas-loyalty-addSystemIdentifier.png)
   1. 选择&#x200B;**[!UICONTROL 应用]**

      ![应用新字段属性](assets/schemas-loyalty-applySystemIdentifier.png)

现在，在`systemIdentifier`对象下添加两个字段：

1. 第一个字段
   1. **[!UICONTROL 字段名称]**： `loyaltyId`
   1. **[!UICONTROL 显示名称：]** `Loyalty Id`
   1. **[!UICONTROL 类型]**： **[!UICONTROL 字符串]**
1. 第二个字段
   1. **[!UICONTROL 字段名称]**： `crmId`
   1. **[!UICONTROL 显示名称]**： `CRM Id`
   1. **[!UICONTROL 类型]**： **[!UICONTROL 字符串]**

您的新字段组应如下所示。 选择&#x200B;**[!UICONTROL Save]**&#x200B;按钮以保存您的架构，但在下一次练习中保持该架构处于打开状态。
![忠诚度字段组完成](assets/schemas-loyalty-identityFieldGroupComplete.png)

## 创建数据类型

字段组（如新`Luma Identity profile field group`）可在其他架构中重用，从而允许您跨多个系统实施标准数据定义。 但它们只能在共享类&#x200B;_的架构中重用_，在本例中为XDM个人资料类。

数据类型是另一个多字段构造，可在多个类&#x200B;_的架构_&#x200B;中重复使用。 让我们将新的`systemIdentifier`对象转换为数据类型：

在`Luma Loyalty Schema`仍然打开的情况下，选择`systemIdentifier`对象并选择&#x200B;**[!UICONTROL 转换为新数据类型]**

![忠诚度字段组完成](assets/schemas-loyalty-convertToDataType.png)

如果您&#x200B;**[!UICONTROL 从架构中取消]**&#x200B;并导航到&#x200B;**[!UICONTROL 数据类型]**&#x200B;选项卡，您将看到新创建的数据类型。 我们将在本课程的后面部分使用此数据类型。

![忠诚度字段组完成](assets/schemas-loyalty-confirmDataType.png)


## 通过API创建CRM架构

现在，我们将使用API创建架构。

>[!TIP]
>
> 如果您希望跳过API练习，则可以使用用户界面方法创建以下架构：
>
> 1. 使用[!UICONTROL 个人资料]类
> 1. 将其命名为`Luma CRM Schema`
> 1. 使用以下字段组：“人口统计详细信息”、“个人联系人详细信息”和“Luma身份配置文件”字段组

首先，创建空架构：

1. 打开[!DNL Postman]
1. 如果您没有访问令牌，请打开请求&#x200B;**[!DNL OAuth: Request Access Token]**&#x200B;并选择&#x200B;**发送**&#x200B;以请求新的访问令牌。
1. 打开您的环境变量，并将&#x200B;**CONTAINER_ID**&#x200B;的值从`global`更改为`tenant`。 请记住，当您想要与Platform中您自己的自定义元素交互时（例如创建架构），必须使用`tenant`。
1. 选择&#x200B;**保存**
   ![将CONTAINER_ID更改为租户](assets/schemas-crm-changeContainerId.png)
1. 打开请求&#x200B;**[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. 打开&#x200B;**主体**&#x200B;选项卡并粘贴以下代码，然后选择&#x200B;**发送**&#x200B;以进行API调用。 此调用使用相同的`XDM Individual Profile`基类创建一个新架构：

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
   >此代码示例和后续代码示例（例如`https://ns.adobe.com/xdm/context/profile`）中的命名空间引用可以通过使用列表API调用和&#x200B;**[!DNL CONTAINER_ID]**&#x200B;以及接受标头设置为正确的值来获取。 部分内容还可在用户界面中轻松访问。

1. 您应会收到`201 Created`响应
1. 从响应正文中复制`meta:altId`。 我们稍后将在另一个练习中使用它。
   ![创建CRM架构](assets/schemas-crm-createSchemaCall.png)

1. 新架构应在用户界面中可见，但不包含任何字段组
   ![创建CRM架构](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> 通过将&#x200B;**[!UICONTROL CONTAINER_ID]**&#x200B;设置为`tenant`并接受标头`application/vnd.adobe.xdm+json`的API请求&#x200B;**[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**，还可以获取`meta:altId`或架构ID。

>[!TIP]
>
> 此调用的常见问题以及可能的修复：
>
> * 无身份验证令牌：运行&#x200B;**OAuth：请求访问令牌**&#x200B;请求以生成新令牌
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`：将&#x200B;**CONTAINER_ID**&#x200B;环境变量从`global`更新为`tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`：在Admin Console中验证您的用户权限

### 添加标准字段组

现在可以将字段组添加到架构中：

1. 在[!DNL Postman]中，打开请求&#x200B;**[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. 在&#x200B;**参数**&#x200B;选项卡中，将上一个响应中的`meta:altId`值粘贴为`SCHEMA_ID`
1. 打开“正文”选项卡并粘贴以下代码，然后选择&#x200B;**发送**&#x200B;以进行API调用。 此调用将标准字段组添加到您的`Luma CRM Schema`：

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

现在，让我们将`Luma Identity profile field group`添加到架构中。 首先，我们需要使用列表API查找新字段组的ID：

1. 打开请求&#x200B;**[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. 选择&#x200B;**发送**&#x200B;按钮以检索您帐户中所有自定义字段组的列表
1. 获取`Luma Identity profile field group`的`$id`值（您的值将与此屏幕快照中的值不同）
   ![检索字段组列表](assets/schemas-crm-getListOfMixins.png)
1. 再次打开请求&#x200B;**[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. **Params**&#x200B;选项卡仍应包含架构的`$id`
1. 打开&#x200B;**正文**&#x200B;选项卡并粘贴以下代码，将`$ref`值替换为您自己的`Luma Identity profile field group`的`$id`：

   ```json
   [{
     "op": "add",
     "path": "/allOf/-",
     "value": {
       "$ref": "REPLACE_WITH_YOUR_OWN_FIELD_GROUP_ID"
     }
   }]
   ```

1. 选择&#x200B;**发送**
   ![添加标识字段组](assets/schemas-crm-addIdentityMixin.png)

通过检查API响应和界面中的字段组，验证该字段组是否已添加到架构中。

## 创建离线购买事件架构

现在，让我们根据&#x200B;**[!UICONTROL Experience Event]**&#x200B;类为Luma的离线购买数据创建架构。 由于您现在已熟悉架构编辑器用户界面，因此我将减少说明中的屏幕截图数量：

1. 创建具有&#x200B;**[!UICONTROL Experience Event]**&#x200B;类的架构。
1. 命名您的架构`Luma Offline Purchase Events Schema`。
1. 添加标准字段组&#x200B;**[!UICONTROL Commerce详细信息]**&#x200B;以捕获通用订单详细信息。 花几分钟研究一下里面有哪些东西。
1. 搜索`Luma Identity profile field group`。 不可用！ 请记住，字段组与类相关联，由于我们对此架构使用不同的类，因此我们无法使用它。 我们需要为包含标识字段的XDM ExperienceEvent类添加新字段组。 我们的数据类型会使其变得非常简单！
1. 选择&#x200B;**[!UICONTROL 创建新字段组]**&#x200B;单选按钮
1. 输入&#x200B;**[!UICONTROL 显示名称]**&#x200B;作为`Luma Identity ExperienceEvent field group`并选择&#x200B;**[!UICONTROL 添加字段组]**&#x200B;按钮
1. 选择架构名称旁边的 **[!UICONTROL +]**。
1. 作为&#x200B;**[!UICONTROL 字段名称]**，输入`systemIdentifier`。
1. 作为&#x200B;**[!UICONTROL 显示名称]**，请输入`System Identifier`。
1. 对于&#x200B;**[!UICONTROL 类型]**，请选择&#x200B;**系统标识符**，这是您之前创建的自定义数据类型。
1. 作为&#x200B;**[!UICONTROL 字段组]**，选择&#x200B;**Luma标识ExperienceEvent字段组**。
1. 选择&#x200B;**[!UICONTROL 应用]**&#x200B;按钮。
1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;按钮。

请注意数据类型如何添加所有字段！

![将数据类型添加到字段组](assets/schemas-offlinePurchases-addDatatype.png)

此外，在&#x200B;**[!UICONTROL Class]**&#x200B;标题下选择&#x200B;**[!UICONTROL XDM ExperienceEvent]**，并检查此类贡献的某些字段。 请注意，使用XDM ExperienceEvent类时需要_id和时间戳字段，使用此架构时摄取的每个记录都必须填充这些字段：

![体验事件基本结构](assets/schemas-offlinePurchase-experienceEventbase.png)

## 创建Web事件架构

现在，我们将为Luma的网站数据再创建一个架构。 此时，您应该成为创建架构的专家！ 使用这些属性构建以下架构

| 属性 | 值 |
|---------------|-----------------|
| 类 | 体验事件 |
| 架构名称 | Luma Web事件架构 |
| 字段组 | AEP Web SDK ExperienceEvent |
| 字段组 | 使用者体验事件 |

选择&#x200B;**[!UICONTROL 使用者体验事件]**&#x200B;字段组。 此字段组包含商业和productListItems对象，这些对象也在[!UICONTROL Commerce详细信息]中。 事实上，[!UICONTROL 使用者体验事件]是另外几个标准字段组的组合，这些字段组也单独提供。 [!UICONTROL AEP Web SDK ExperienceEvent]字段组还包含其他字段组，包括[!UICONTROL 使用者体验事件]中一些相同的字段组。 幸运的是，他们完美地融合在一起。

请注意，我们未将`Luma Identity ExperienceEvent field group`添加到此架构。 这是因为Web SDK具有不同的身份收集方式。 如果您在架构编辑器的&#x200B;**[!UICONTROL 合成]**&#x200B;区域中选择&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;类，您将注意到它默认添加的字段之一名为&#x200B;**[!UICONTROL IdentityMap]**。 各种Adobe应用程序使用[!DNL IdentityMap]链接到Platform。 您将在流摄取课程中看到如何通过identityMap将身份发送到Platform。


## 创建产品目录架构

通过使用[!UICONTROL Commerce详细信息]和[!UICONTROL 使用者体验事件]字段组，Luma通过标准productListItems数据类型报告产品相关事件的某些详细信息。 但是，他们还希望将其他产品详细信息字段发送到Platform。 与其在销售点和电子商务系统中捕获所有这些字段，Luma更愿意直接从他们的产品目录系统中摄取这些字段。 “架构关系”允许您定义两个架构之间的关系，以进行分类或查找。 Luma将使用关系对其产品详细信息进行分类。 我们将立即开始此过程，并在下一课结束时完成此过程。

>[!NOTE]
>
>如果您是现有Analytics或Target客户，则对具有架构关系的实体进行分类类似于SAINT分类或上传产品目录以获取推荐

首先，我们必须使用自定义类为Luma的产品目录创建架构：

1. 选择&#x200B;**[!UICONTROL 创建架构]**&#x200B;按钮。
1. 在创建架构工作流中，选择&#x200B;**[!UICONTROL 其他]**&#x200B;选项。
   ![创建新架构](assets/schemas-newSchema-browseClasses.png)
1. 选择&#x200B;**[!UICONTROL 创建类]**&#x200B;按钮
1. 将其命名为`Luma Product Catalog Class`
1. 将&#x200B;**[!UICONTROL 行为]**&#x200B;保留为&#x200B;**[!UICONTROL 记录]**
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。
   ![创建新类](assets/schemas-productClass.png)
1. 您创建的&#x200B;**Luma产品目录类**&#x200B;出现在下面的“类”表中。 确保已选择类，然后选择&#x200B;**[!UICONTROL 下一步]**。
   ![新类已添加](assets/schemas-productClassSelected.png)
1. 命名架构`Luma Product Catalog Schema`。
1. 使用以下字段创建一个名为`Luma Product Catalog field group`的新[!UICONTROL 字段组]：
   1. productName：产品名称：字符串
   1. productCategory： Product类别：字符串
   1. productColor： Product Color：字符串
   1. productSku： Product SKU：字符串 | 必填
   1. productSize： Product Size：字符串
   1. productPrice： Product Price： Double
1. **[!UICONTROL 保存]**&#x200B;架构

您的新架构应如下所示。 请注意`productSku`字段在[!UICONTROL 必填字段]部分中的列出方式：
![产品架构](assets/schemas-productSchema.png)

下一步是定义两个ExperienceEvent架构与`Luma Product Catalog Schema`之间的关系，但是，在可以执行该操作之前，我们必须在下一课程中执行一些其他步骤。


## 其他资源

* [体验数据模型(XDM)系统文档](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)
* [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


现在您已拥有架构，可以[映射身份](map-identities.md)！
