---
title: 配置权限
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 配置权限
description: 在本课程中，您将使用Adobe Experience Platform的Admin Console配置Adobe用户权限。
role: Data Architect, Data Engineer
feature: Access Control
kt: 4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 2%

---

# 配置权限

<!--30min-->

在本课程中，您将使用配置Adobe Experience Platform用户权限 [!DNL Adobe's Admin Console].

访问控制是Experience Platform中一项关键的隐私功能，我们建议将权限限制为用户执行其工作职能所需的最低权限。 请参阅 [访问控制文档](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hans) 以了解更多信息。

数据架构师和数据工程师是Adobe Experience Platform的高级用户，您需要许多权限才能完成本教程，并且稍后会在日常工作中完成本教程。 数据架构师可能参与 *其他平台用户* 营销人员、分析人员和数据科学家等。 完成本课程时，请考虑如何使用这些功能来管理公司的其他用户。

**数据架构师** 在本教程之外，通常会为其他用户配置权限。

>[!IMPORTANT]
>
>Adobe Experience Cloud产品的系统管理员必须完成本课程中的某些步骤，这些步骤在部分标题中有所说明。 如果您不是系统管理员，请联系贵公司的一位管理员，要求他们完成这些任务。

## 关于Admin Console

的 [!DNL Admin Console] 是用于管理用户对所有Adobe Experience Cloud产品的访问权限的界面。 请参阅 [Adobe Admin Console文档](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 以了解更多详细信息。 以下是一些关键 [!DNL Admin Console] 概念：

* A **产品配置文件** 是与特定Adobe产品绑定的权限、角色和沙盒环境的组合。 可以为单个产品创建多个产品配置文件Adobe。 例如，“营销人员”配置文件可以将权限限制为典型营销人员在生产平台环境中完成关键任务所需的权限，而“数据架构师”配置文件则可用于在多个平台环境中授予不同权限。 在本课程中，您将创建一个“Luma教程”产品用户档案，其中包含数据架构师和数据工程师在沙盒环境中完成本教程所需的所有权限。
* 安 **集成** 是与 *项目* 在Adobe Developer控制台中。 Adobe Developer控制台是AdobeAPI身份验证和配置的核心。 您将在开发人员控制台中配置集成，并 [!DNL Postman] 课程。

以下是对Platform中存在的角色的快速摘要：

* **用户** 产品配置文件的用户可以根据产品配置文件中分配的权限，在Platform的用户界面中完成任务。
* **开发人员** 产品配置文件的用户可以根据产品配置文件中的权限，使用Platform的API完成任务。
* **产品配置文件管理员** 可以编辑 *具体的用户档案* 权限并添加用户、开发人员和其他配置文件管理员。
* **产品管理员** 可以管理 *所有产品配置文件* ，并添加新的产品配置文件。
* **系统管理员** 可以添加产品管理员并管理所有Adobe Experience Cloud产品的基本权限。

## 创建Experience Platform产品配置文件（需要系统管理员或产品管理员）

在本练习中，您或您公司的系统管理员将为Adobe Experience Platform创建产品配置文件，并将您添加为该产品配置文件的管理员。

>[!NOTE]
>
>如果您是系统管理员，协助同事学习本教程，请考虑将您的同事添加为 *产品管理员* Adobe Experience Platform。 作为产品管理员，他们将能够自行完成这些步骤并在将来管理其他Experience Platform用户。

要创建产品配置文件，请执行以下操作：

1. 登录 [Adobe Admin Console](https://adminconsole.adobe.com)
1. 选择 **[!UICONTROL 产品]** 在顶部导航中
1. 选择 **[!UICONTROL Adobe Experience Platform]** (您可能需要将 **[!UICONTROL Experience Cloud]** 部分)
1. 您的Experience Platform实例中可能已有多个用户档案。 选择 **[!UICONTROL 新建用户档案]** 按钮添加其他
   ![选择添加新配置文件](assets/adminconsole-newProfile.png)
1. 命名配置文件 `Luma Tutorial Platform` （如果您公司的多个人员正在学习本教程，请将教程参与者的姓名添加到结尾）并选择 **[!UICONTROL 下一个]** 按钮
   ![将配置文件命名为Luma Tutorial Platform](assets/adminconsole-nameProfile.png)
1. 根据您的产品许可证的详细信息，您可能会看到，也可能看不到 **[!UICONTROL 服务]** 屏幕。 在本教程中，我们将不会使用这些服务中的任何一项，因此请取消选中 **[!UICONTROL 启用所有服务]** to *删除* 所有服务和选择 **[!UICONTROL 保存]**.
   ![禁用服务](assets/adminconsole-createProfile-services.png)

现在，将教程参与者添加为新创建产品用户档案的管理员。 如果 *you* 是教程参与者，请跳到 [配置Experience Platform产品配置文件](#configure-experience-platform-product-profile):

1. 选择 `Luma Tutorial Platform` 产品配置文件：

   ![打开用户档案](assets/adminconsole-newProfileInList.png)

1. 选择 **[!UICONTROL 管理员]** ，然后选择 **[!UICONTROL 添加管理员]** 按钮：

   ![转到管理员选项卡，然后选择添加管理员](assets/adminconsole-addAdmin.png)

1. 完成工作流以将教程参与者添加为管理员。

完成这些步骤后，您应会看到 `Luma Tutorial Platform` 配置文件由一个管理员设置。
![已创建平台配置文件](assets/adminconsole-platform-profileCreated.png)

## 配置Experience Platform产品配置文件

现在，您是 `Luma Tutorial Platform` 产品配置文件您可以配置完成本教程所需的权限和角色。

### 添加权限

现在，您将向用户档案添加单个权限项：

1. 打开 `Luma Tutorial Platform` 产品配置文件
1. 选择 **[!UICONTROL 权限]** 选项卡
1. 在 **[!UICONTROL 沙箱]**，添加 **[!UICONTROL 生产]** 沙盒添加到用户档案。 必须能够访问 [!DNL Prod] 沙盒，以创建其他沙箱。 在下一课程中添加教程沙盒后，我们将删除 [!DNL Prod] 沙盒。
1. 在 [!UICONTROL 数据摄取]，添加 [!UICONTROL 管理源] 和 [!UICONTROL 查看源] 权限项。
1. 为以下项添加所有权限项：
   1. [!UICONTROL 数据建模]
   1. [!UICONTROL 数据管理]
   1. [!UICONTROL 用户档案管理]
   1. [!UICONTROL Identity Management]
   1. [!UICONTROL 沙盒管理]
   1. [!UICONTROL 查询服务]
   1. [!UICONTROL 数据收集]
   1. [!UICONTROL 数据管理]
   1. [!UICONTROL 仪表板]
   1. [!UICONTROL 警报]

1. 添加所有权限项后，请务必选择 **[!UICONTROL 保存]** 按钮

### 将您自己添加为用户

此时，如果 `Luma Tutorial Platform` 你 *仅* Experience Platform产品配置文件时，您仍无法登录Experience Platform的用户界面。 为此，你需要成为 *用户* 中。 幸运的是，既然你是 *管理员* 在产品配置文件中，您可以将自己添加为 *用户*!

1. 转到 **[!UICONTROL 用户]** 选项卡
1. 选择 **[!UICONTROL 添加用户]** 按钮
   ![选择添加用户](assets/adminconsole-addUser.png)
1. 完成工作流，将您自己作为用户添加到产品配置文件

### 将您自己添加为开发人员

要使用平台API，请将自己添加为开发人员：

1. 转到 **[!UICONTROL 开发人员]** 选项卡
1. 选择 **[!UICONTROL 添加开发人员]** 按钮
   ![选择添加用户](assets/adminconsole-addDeveloper.png)
1. 完成工作流，将您自己作为开发人员添加到产品用户档案

## 创建数据收集产品配置文件（需要系统管理员或产品管理员）

在本练习中，您或贵公司的系统管理员将为数据收集(以前称为Adobe Experience Platform Launch)创建产品配置文件，并将您添加为产品配置文件管理员。

>[!NOTE]
>
>如果您是系统管理员，在本教程中协助同事，请考虑将他们添加为 *产品管理员* （用于数据收集）。 作为产品管理员，他们将能够自行完成这些步骤并在将来管理数据收集的其他用户。

要创建产品配置文件，请执行以下操作：

1. 在 [!DNL Adobe Admin Console] 转到Adobe Experience Platform数据收集产品
1. 添加名为 `Luma Tutorial Data Collection` （如果您公司的多个人员正在学习本教程，请将教程参与者的姓名添加到结尾）
1. 关闭 **[!UICONTROL 属性]** > **[!UICONTROL 自动包含]** 设置
1. 此时不分配任何资产或权限
1. 将教程参与者添加为此用户档案的管理员

完成这些步骤后，您应会看到 `Luma Tutorial Data Collection` 配置文件由一个管理员设置。
![数据收集配置文件已创建](assets/adminconsole-dc-profileCreated.png)

## 配置数据收集产品配置文件

现在，您是 `Luma Tutorial Data Collection` 产品配置文件您可以配置完成本教程所需的权限和角色。

### 添加权限

现在，您将向用户档案添加单个权限项：

1. 在 [Adobe Admin Console](https://adminconsole.adobe.com)，转到 **[!UICONTROL 产品]** > **[!UICONTROL 数据收集]**
1. 打开 `Luma Tutorial Data Collection` 个人资料
1. 转到 **[!UICONTROL 权限]** 选项卡
1. 打开 **[!UICONTROL 平台]**
1. 确保选择所有可用平台（您可能会根据许可证看到不同的选项）
1. **[!UICONTROL 保存]** 任何更改
   ![添加平台](assets/adminconsole-launch-addPlatforms.png)
1. 打开 **[!UICONTROL 属性]**
1. 确保 **[!UICONTROL 自动包含]** 关闭，以便您无权访问任何属性（我们稍后会添加一个）
1. **[!UICONTROL 保存]** 任何更改
   ![删除属性](assets/adminconsole-launch-removeProperties.png)
1. 打开 **[!UICONTROL 资产权限]**
1. 选择 **[!UICONTROL 全部添加]** 添加所有资产权限
1. **[!UICONTROL 进行保存]**
   ![删除属性](assets/adminconsole-launch-addPropertyRights.png)
1. 打开 **[!UICONTROL 公司权限]**
1. 添加 **[!UICONTROL 管理资产]**
1. 选择 **[!UICONTROL 保存]**

   ![删除属性](assets/adminconsole-launch-companyRights.png)


### 将您自己添加为用户

现在，将您自己作为用户添加到数据收集配置文件：

1. 转到 **[!UICONTROL 用户]** 选项卡
1. 选择 **[!UICONTROL 添加用户]** 按钮
   ![选择添加用户](assets/adminconsole-launch-addUser.png)
1. 完成工作流，将您自己作为用户添加到产品配置文件

您无需将自己添加为数据收集开发人员。

现在，您几乎拥有完成本教程所需的所有权限！ 你将在内部再做两次调整 [!DNL Adobe Admin Console]，包括一个 [创建沙盒](create-a-sandbox.md)!
