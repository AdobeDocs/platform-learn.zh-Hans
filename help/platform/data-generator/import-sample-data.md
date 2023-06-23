---
title: 将示例数据导入到 Adobe Experience Platform
description: 了解如何使用一些示例数据设置Experience Platform沙盒环境。
role: Developer
feature: API
jira: KT-7349
thumbnail: 7349.jpg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 5%

---

# 将示例数据导入到 Adobe Experience Platform

了解如何使用示例数据设置 Experience Platform 沙盒环境。使用 Postman 集合，您可以创建字段组、架构和数据集，然后将示例数据导入 Experience Platform。

## 示例数据用例

Experience Platform业务用户通常必须完成一系列步骤，包括识别字段组、创建架构、准备数据、创建数据集，然后摄取数据，然后才能探索Experience Platform提供的营销功能。 本教程会自动执行一些步骤，以便您可以尽快将数据导入Platform沙盒。

本教程重点介绍一个名为Luma的虚构零售品牌。 他们投资于Adobe Experience Platform以将忠诚度、CRM、产品目录和离线购买数据组合到实时客户配置文件中，并激活这些配置文件以将他们的营销提升到新的水平。 我们为Luma生成了示例数据，在本教程的其余部分中，您将将此数据导入您的某个Experience Platform沙盒环境中。

>[!NOTE]
>
>本教程的最终结果是一个沙盒，其中包含与相似的数据。 [面向数据架构师和数据工程师的Adobe Experience Platform快速入门教程](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html). 它于2023年4月进行了更新，以支持 [Journey Optimizer挑战](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=zh-Hans). 它于2023年6月更新，以将身份验证方法切换到OAuth。


## 先决条件

* 您有权访问Experience PlatformAPI并了解如何进行身份验证。 如果没有，请查看 [教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=zh-Hans).
* 您有权访问Experience Platform开发沙盒。
* 您知道您的Experience Platform租户ID。 您可以通过进行身份验证来获取它 [API请求](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#know-your-tenant_id)
或者在您登录Platform帐户时从URL中提取该变量。 例如，在以下URL中，租户是&quot;`techmarketingdemos`” `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## 使用 [!DNL Postman] {#postman}

### 设置环境变量

在执行以下步骤之前，请确保您已下载 [Postman](https://www.postman.com/downloads/) 应用程序。 让我们开始吧！

1. 下载 [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) 文件，其中包含本教程所需的所有文件。

   >[!NOTE]
   >
   >中包含的用户数据 [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) 文件是虚构的，仅用于演示目的。

1. 从下载文件夹中，将 `platform-utils-main.zip` 文件移动到计算机上的所需位置，然后将其解压缩。
1. 在 `luma-data` 文件夹，打开所有 `json` 文件并替换的所有实例 `_yourTenantId` 您自己的租户id，前面加有下划线。
1. 打开 `luma-offline-purchases.json`， `luma-inventory-events.json`、和 `luma-web-events.json` 在文本编辑器中并更新所有时间戳，以便事件发生在上个月(例如，搜索 `"timestamp":"2022-11` 并替换年和月)
1. 请注意解压缩文件夹的位置，因为您稍后在设置 `FILE_PATH` [!DNL Postman] 环境变量：

   >[!NOTE]
   > 要在Mac上获取文件路径，请导航至 `platform-utils-main` 文件夹，右键单击该文件夹并选择 **获取信息** 选项。
   >
   > ![Mac文件路径](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > 要在窗口中获取文件路径，请单击以打开所需文件夹的位置，然后在地址栏中右键单击路径右侧。 复制地址以获取文件路径。
   > 
   > ![Windows文件路径](../assets/data-generator/images/windows-file-path.png)

1. 打开 [!DNL Postman] 并从创建工作区 **工作区** 下拉菜单：\
   ![创建工作区](../assets/data-generator/images/create-workspace.png)
1. 输入 **名称** 和可选 **摘要** （对于工作区），然后单击 **创建工作区**. [!DNL Postman] 将在您创建新工作区时切换到新工作区。
   ![保存工作区](../assets/data-generator/images/save-workspace.png)
1. 现在调整一些设置以运行 [!DNL Postman] 收藏集。 在的标题中 [!DNL Postman]，单击齿轮图标并选择 **设置** 以打开设置模式窗口。 您还可以使用键盘快捷键(CMD/CTRL + ，)打开相应模式。
1. 在 `General` 选项卡，将请求超时（以毫秒为单位）更新为 `5000 ms` 并启用 `allow reading file outside this directory`
   ![设置](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > 如果文件是从工作目录中加载的，如果将相同的文件存储在其他设备上，则该文件将跨设备平稳运行。 但是，如果您希望从工作目录外部运行文件，则必须打开设置以声明相同的意图。 如果您的 `FILE_PATH` 与 [!DNL Postman]的工作目录路径，则应启用此选项。

1. 关闭 **设置** 面板。
1. 选择 **环境** 然后选择 **导入**：
   ![环境导入](../assets/data-generator/images/env-import.png)
1. 导入下载的json环境文件， `DataInExperiencePlatform.postman_environment`
1. 在Postman中，从右上角的下拉菜单中选择您的环境，然后单击眼睛图标以查看环境变量：
   ![环境选择](../assets/data-generator/images/env-selection.png)

1. 确保填充了以下环境变量。 要了解如何获取环境变量的值，请查看 [对Experience PlatformAPI进行身份验证](/help/platform/authentication/platform-api-authentication.md) 分步说明教程。

   * `CLIENT_SECRET`
   * `API_KEY`—`Client ID` 在Adobe Developer控制台中
   * `SCOPES`
   * `TECHNICAL_ACCOUNT_ID`
   * `IMS`
   * `IMS_ORG`—`Organization ID` 在Adobe Developer控制台中
   * `SANDBOX_NAME`
   * `TENANT_ID` — 确保以下划线开头，例如 `_techmarketingdemos`
   * `CONTAINER_ID`
   * `platform_end_point`
   * `FILE_PATH` — 使用解压的本地文件夹路径 `platform-utils-main.zip` 文件。 确保它包含文件夹名称，例如 `/Users/dwright/Desktop/platform-utils-main`

1. **保存** 更新的环境

### 导入Postman收藏集

接下来，您需要将收藏集导入Postman。

1. 选择 **收藏集** 然后选择导入选项：

   ![收藏集](../assets/data-generator/images/collections.png)

1. 导入以下收藏集：

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`
   * `5-Luma-Product-Inventory-Events.postman_collection.json`
   * `6-Luma-Test-Profiles.postman_collection.json`
   * `7-Luma-Web-Events.postman_collection.json`

   ![收藏集导入](../assets/data-generator/images/collection-files.png)

### 身份验证

接下来，您需要进行身份验证并生成用户令牌。 请注意，本教程中使用的令牌生成方法仅适用于非生产用途。 本地签名从第三方主机加载JavaScript库，而远程签名将私钥发送到Adobe拥有并操作的Web服务。 虽然Adobe不会存储此私钥，但绝不应该与任何人共享生产密钥。

1. 打开 `0-Authentication` 收藏集，选择 `OAuth: Request Access Token` 请求，然后单击 `SEND` 验证并获取访问令牌。

   ![收藏集导入](../assets/data-generator/images/authentication.png)

1. 查看环境变量，并注意 `ACCESS_TOKEN` 现已填充。

### 导入数据

现在，您可以准备数据并将其导入Platform沙盒。 您导入的Postman系列将完成所有繁重的工作！

1. 打开 `1-Luma-Loyalty-Data` 收藏集并单击 **运行** 在“概述”选项卡上启动收藏集运行器。

   ![收藏集导入](../assets/data-generator/images/loyalty.png)

1. 在收集运行程序窗口中，确保从下拉列表中选择环境，然后更新 **延迟** 到 `4000ms`，查看 **保存响应** 选项，并确保运行顺序正确。 单击 **运行Luma忠诚度数据** 按钮

   ![收藏集导入](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-Data** 为客户忠诚度数据创建架构。 该架构基于XDM Individual Profile类、标准字段组以及自定义字段组和数据类型。 收藏集使用架构创建数据集，并将示例客户忠诚度数据上传到Adobe Experience Platform。

   >[!NOTE]
   >
   >如果在Postman收集运行程序期间有任何收集请求失败，请停止执行并逐一运行收集请求。

1. 如果一切顺利，则所有请求 `Luma-Loyalty-Data` 收藏集应通过。

   ![忠诚度结果](../assets/data-generator/images/loyalty-result.png)

1. 现在，让我们登录到 [Adobe Experience Platform界面](https://platform.adobe.com/) 和导航到数据集。
1. 打开 `Luma Loyalty Dataset` 在数据集活动窗口下，您可以查看摄取1000条记录的成功批量运行。 您还可以单击预览数据集选项以验证摄取的记录。 您可能需要等待几分钟来确认1000 [!UICONTROL 新配置文件片段] 创建。
   ![忠诚度数据集](../assets/data-generator/images/loyalty-dataset.png)
1. 重复步骤1-3以运行其他收藏集：
   * `2-Luma-CRM-Data.postman_collection.json` 为客户的CRM数据创建架构和填充的数据集。 该架构基于XDM个人资料类，该类包含人口统计详细信息、个人联系详细信息、首选项详细信息和自定义标识字段组。
   * `3-Luma-Product-Catalog.postman_collection.json` 为产品目录信息创建架构和填充的数据集。 该架构基于自定义产品目录类，并使用自定义产品目录字段组。
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` 为客户离线购买事件数据创建架构和填充的数据集。 该架构基于XDM ExperienceEvent类，并包含自定义身份和商务详细信息字段组。
   * `5-Luma-Product-Inventory-Events.postman_collection.json` 为与进货和缺货产品相关的事件创建架构并填充数据集。 架构基于自定义业务事件类和自定义字段组。
   * `6-Luma-Test-Profiles.postman_collection.json` 创建一个架构并填充有测试配置文件的数据集，以便在Adobe Journey Optimizer中使用
   * `7-Luma-Web-Events.postman_collection.json` 创建一个架构并使用简单的历史Web数据填充数据集。


## 验证

样本数据经过专门设计，以便在集合运行时，构建可组合来自多个系统的数据的实时客户档案。 忠诚度、CRM和离线购买数据集的第一个记录就是一个很好的例子。 查找该配置文件以确认数据已摄取。 在 [Adobe Experience Platform界面](https://experience.adobe.com/platform/)：

1. 转到 **[!UICONTROL 配置文件]** > **[!UICONTROL 浏览]**
1. 选择 `Luma Loyalty Id` 作为 **[!UICONTROL 身份命名空间]**
1. 搜索 `5625458` 作为 **[!UICONTROL 标识值]**
1. 打开 `Daniel Wright` 个人资料

>[!TIP]
>
>如果您看不到配置文件，请检查 [!UICONTROL 数据集] 页面，确认已成功创建和摄取所有数据集。 如果一切正常，请等待15分钟，然后查看查看查看器中是否有该配置文件。  如果摄取数据时出现问题，请检查错误消息以尝试找到问题。 您还可以尝试对以下对象启用错误诊断 [!UICONTROL 数据集] 并拖放json数据文件以重新摄取数据。


![打开用户档案](../assets/data-generator/images/validation-profile-open.png)

浏览中的数据 **[!UICONTROL 属性]** 和 **[!UICONTROL 事件]** 选项卡中，您应该会看到配置文件包含来自各种数据文件的数据：
![离线购买事件文件中的事件数据](../assets/data-generator/images/validation-profile-events.png)

## 后续步骤

如果您想了解Adobe Journey Optimizer，此沙盒包含您需要获取 [Journey Optimizer挑战](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=zh-Hans)

如果您想了解合并策略、数据管理、查询服务和区段生成器，请跳转到 [数据架构师和数据工程师入门教程中的第11课](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=en). 本其他教程的前几个课程让您可以手动构建这些Postman收藏集刚刚填充的所有内容 — 开门见山吧！

如果要构建链接到此沙盒的示例Web SDK实施，请查看
[使用Web SDK实施Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans). 设置Web SDK教程的“初始配置”、“标记配置”和“设置Experience Platform”课程后，使用中的前十个电子邮件地址登录Luma网站 `luma-crm.json` 使用密码的文件 `test` 查看配置文件片段与本教程中上传的数据的合并情况。

如果要构建一个链接到此沙盒的示例Mobile SDK实施，请查看
[在移动应用程序中实施Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=zh-Hans). 设置Web SDK教程的“初始配置”、“应用程序实施”和“Experience Platform”课程后，使用中的第一个电子邮件地址登录Luma网站 `luma-crm.json` 文件，查看配置文件片段与本教程中上传的数据的合并。

## 重置沙盒环境 {#reset-sandbox}

重置非生产沙盒会删除与该沙盒关联的所有资源（架构、数据集等），同时维护沙盒的名称和关联的权限。 对于有权访问此“清理”沙盒的用户，将继续以相同的名称提供该沙盒。

按照以下步骤操作 [此处](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=en#reset-a-sandbox) 重置沙盒环境。
