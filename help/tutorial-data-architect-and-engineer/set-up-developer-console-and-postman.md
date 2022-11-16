---
title: 设置开发人员控制台和Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 设置开发人员控制台和Postman
description: 在本课程中，您将在Adobe Developer控制台中设置一个项目，并为您提供 [!DNL Postman] 收藏集，以便您能够开始使用Platform API。
role: Data Architect, Data Engineer
feature: API
kt: 4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 1%

---

# 设置开发人员控制台和 [!DNL Postman]

<!--30min-->

在本课程中，您将在Adobe Developer控制台中设置一个项目并下载 [!DNL Postman] 收藏集，以便您能够开始使用Platform API。

要完成本教程中的API练习， [下载适用于您的操作系统的Postman应用程序。](https://www.postman.com/downloads/) 虽然使用Experience PlatformAPI不是必需的，但Postman可以简化API工作流程，而且Adobe Experience Platform提供了大量Postman集合，帮助您执行API调用并了解其操作方式。 本教程的其余部分假定了一些Postman的工作知识。 如需帮助，请参考 [Postman文档](https://learning.postman.com/).

平台是先构建API的。 虽然所有主要任务都有界面选项，但您可能希望在某个时候使用Platform API。 例如，在构建用户界面之前，要摄取数据、在沙箱之间移动项目、自动执行日常任务或使用新的平台功能。

**数据架构师** 和 **数据工程师** 在本教程之外，可能需要使用Platform API。

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## 设置Adobe Developer控制台

Adobe Developer Console是访问AdobeAPI和SDK、侦听接近实时的事件、在运行时运行函数，或构建插件或应用程序生成器应用程序的开发人员目标。 您将使用它访问Experience PlatformAPI。 有关更多详细信息，请参阅 [Adobe Developer Console文档](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. 在本地计算机上创建一个名为 `Luma Tutorial Assets` ，用于教程中使用的文件。

1. 打开 [Adobe Developer控制台](https://console.adobe.io)

1. 登录并确认您位于正确的组织中

1. 选择 **[!UICONTROL 创建新项目]** in [!UICONTROL 快速入门] 菜单。

   ![创建新项目](assets/adobeio-createNewProject.png)

1. 在新创建的项目中，选择 **[!UICONTROL 添加到项目]** 按钮，然后选择 **[!UICONTROL API]**

   ![Adobe Developer控制台项目API配置](assets/adobeio-addAPI.png)

1. 通过选择 **[!UICONTROL Adobe Experience Platform]**

1. 在可用API列表中，选择 **[!UICONTROL Experience PlatformAPI]** 选择 **[!UICONTROL 下一个]**.

   ![Adobe Developer控制台项目API配置](assets/adobeio-AEPAPI.png)

1. 用于从外部系统(如 [!DNL Postman]，则需要公钥/私钥对。 要生成新键对，请选择 **[!UICONTROL 选项1]**  然后按 **[!UICONTROL 生成密钥对]** 按钮

   ![Adobe Developer控制台项目API配置](assets/adobeio-keypair.png)

1. 密钥准备就绪后，系统可能会提示您将密钥下载到本地计算机。 保存打包在 `config.zip` 到文件夹 `Luma Tutorial Assets`. 下次练习时，我们需要他们。


1. 生成密钥后，公共密钥将自动添加到您的项目，如屏幕截图所示。 选择 **[!UICONTROL 下一个]** 按钮。

   ![ 生成并选择键后查看](assets/adobeio-afterKeyIsGenerated.png)

1. 选择 `Luma Tutorial Platform` 产品配置文件，然后选择 **[!UICONTROL 保存配置的API]** 按钮

   ![选择产品配置文件](assets/adobeio-selectProductProfile.png)

1. 现在，您的开发人员控制台项目已创建！

1. 在 **[!UICONTROL 试试看]** ，请选择 **[!UICONTROL 下载Postman版]** 然后选择 **[!UICONTROL 服务帐户(JWT)]** 下载 [!DNL Postman] 环境json文件。 保存 `service.postman_environment.json` 在 `Luma Tutorial Assets` 文件夹。


   ![Adobe Developer控制台项目API配置](assets/adobeio-io-api.png)

   >[!NOTE]
   >
   >贵组织的系统管理员可以在Admin Console的产品配置文件中将项目视为“API凭据”
   >
   >![Adobe Developer控制台项目API配置](assets/adobeio-io-integrationInAdminConsole.png)

您可能注意到已为项目分配了一个数字，例如“项目12”：

1. 在痕迹导航中选择项目编号
1. 选择 **[!UICONTROL 编辑项目]** 按钮
1. 更改 **[!UICONTROL 项目标题]** to `Luma Tutorial API Project` （如果您公司的多个人员参加了本教程，请将您的姓名添加到结尾）
1. 选择 **[!UICONTROL 保存]** 按钮

   ![Adobe Developer控制台项目API配置](assets/adobeio-renameProject.png)


## 设置Postman

>[!CAUTION]
>
>Postman界面会定期更新。 本教程中的屏幕截图是使用Postman v9.0.5 for Mac拍摄的，但界面选项可能已发生更改。


1. 下载并安装 [[!DNL Postman]](https://www.postman.com/downloads/)
1. 打开 [!DNL Postman] 和导入下载的json环境文件， `service.postman_environment.json`
   ![导入环境](assets/postman-importEnvironment.png)
1. 在 [!DNL Postman]，在下拉菜单中选择您的环境

   ![更改环境](assets/postman-changeEnvironment.png)
1. 选择 **眼睛** 查看环境变量的图标：

   ![Adobe Developer控制台项目API配置](assets/postman-PostmanEnvironment.png)

### 更新环境名称

由于从开发人员控制台导出的环境名称是随机生成的，因此请为其提供一个更具描述性的名称，这样当您稍后开始处理真正的平台实施时，就不会将环境混淆：

1. 当环境变量屏幕仍然打开时，选择 **编辑** 在右上角
1. 更新 **环境名称** to `Luma Tutorial`
1. 离开 **管理环境** 模式窗口打开，因为我们将在下一步中进一步编辑它

   ![更新Postman环境名称](assets/postman-updateEnvName.png)

### 添加私钥

现在，该将PRIVATE_KEY值添加到Postman环境了

1. 解压缩下载的 `config.zip` 文件，该文件是在创建开发人员控制台项目时在上一个练习中生成的。 此zip文件包含两个文件：
   * `private.key`
   * `certificate_pub.crt`
1. 打开 `private.key` 文件，并复制内容。
1. 在Postman，在 **管理环境** > **编辑** 模式窗口，该模式窗口仍然在上一个练习中打开，并将复制的值粘贴到 **PRIVATE_KEY** 在 **初始值** 和 **当前值** 列。
1. 选择 **保存**

   ![粘贴到Postman的私钥](assets/postman-privateKey.png)

### 添加JWT和访问令牌

Adobe提供一组丰富的 [!DNL Postman] 集合，帮助您探索Experience Platform的API。 这些收藏集位于 [Adobe Experience Platform Postman示例GitHub存储库](https://github.com/adobe/experience-platform-postman-samples). 您应将此存储库加入书签，因为在本教程中您将多次使用此存储库，之后在您为自己的公司实施Experience Platform时，您将会多次使用此存储库。

第一个集合适用于AdobeIdentity Management服务(IMS)API。 这是从Postman内填充JWT_TOKEN和ACCESS_TOKEN的一种简便方法 *用于非生产用例* 例如，在沙盒中完成本教程。 或者，也可以在Adobe Developer控制台中生成JWT令牌。 但是，由于它定期过期，因此使用此集合可以刷新它，而无需在完成本教程时再次重新访问Adobe Developer控制台。

>[!WARNING]
>
>如 [AdobeIdentity Management服务API自述文件](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)，表示的生成方法适合于非生产用途。 本地签名从第三方主机加载JavaScript库，远程签名将私钥发送给Adobe拥有和运行的Web服务。 虽然Adobe不存储此私钥，但生产密钥绝不应与任何人共享。

要生成令牌，请执行以下操作：

1. 下载 [开发人员控制台访问令牌生成集合](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/ims/Identity%20Management%20Service.postman_collection.json) 至 `Luma Tutorial Assets` 文件夹
1. 将集合导入 [!DNL Postman]
1. 选择请求 **IMS:JWT通过用户令牌生成+身份验证** 选择 **发送**

   ![请求令牌](assets/postman-requestToken.png)
1. 的 **JWT_TOKEN** 和 **ACCESS_TOKEN** 在 [!DNL Postman].

   ![Postman](assets/postman-config.png)

### 添加沙盒名称和租户ID

的 `SANDBOX_NAME` 和 `TENANT_ID` 和 `CONTAINER_ID` 变量未包含在Adobe Developer控制台导出中，因此我们会手动添加它们：

1. 在 [!DNL Postman]，打开 **环境变量**
1. 选择 **编辑** 环境名称右侧的链接
1. 在 **添加新变量字段**，输入 `SANDBOX_NAME`
1. 在两个值字段中，输入 `luma-tutorial`，上一课程中我们为沙盒提供的名称。 如果您为沙盒使用了其他名称（例如luma-tutorial-ignatiusjreilly），请确保使用该值。
1. 在 **添加新变量字段**，输入 `TENANT_ID`
1. 切换到Web浏览器并查找公司的租户ID，方法是转到Experience Platform的界面并提取URL的部分 *@符号之后*. 例如，我的租户ID是 `techmarketingdemos` 但你的不同：

   ![从平台界面URL获取租户ID](assets/postman-getTenantId.png)

1. 复制此值并返回到 [!DNL Postman] “管理环境”屏幕
1. 将租户ID粘贴到两个值字段中
1. 在 **添加新变量字段**，输入 `CONTAINER_ID`
1. 输入 `global` 同时包含两个值字段

   >[!NOTE]
   >
   >`CONTAINER_ID` 是一个值在教程中多次更改的字段。 When `global` ，则API会与Platform帐户中Adobe提供的元素进行交互。 When `tenant` ，则API会与您自己的自定义元素交互。

1. 选择 **保存**

   ![添加了SANDBOX_NAME、TENANT_ID和CONTAINER_ID字段作为环境变量](assets/postman-addEnvFields.png)


## 进行平台API调用

现在，让我们进行Platform API调用，以确认我们已正确配置了所有内容。

打开 [Experience Platform [!DNL Postman] GitHub中的收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). 本页面上有许多用于各种Platform API的收藏集。 我强烈建议你给它添加书签。

现在，让我们进行第一个API调用：

1. 下载 [架构注册API收集](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) 至 `Luma Tutorial Assets` 文件夹
1. 将其导入 [!DNL Postman]
1. 打开 **架构注册表API >类>列表类**
1. 查看 **参数** 和 **标题** 选项卡，并记下这些选项卡是如何包含我们之前输入的一些环境变量的。
1. 请注意， **标题>接受值字段** 设置为 `application/vnd.adobe.xed-id+json`. 架构注册表API需要其中一个 [指定的接受标头值](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) 在响应中提供不同格式。
1. 选择 **发送** 进行第一个Platform API调用！

希望你成功了 `200 OK` 响应中包含沙盒中可用的标准XDM类列表，如下图所示。

![Postman中的首次API调用](assets/postman-firstAPICall.png)

如果调用失败，请花些时间来使用API调用的错误响应详细信息进行调试，并查看上述步骤。 如果卡住，请在 [社区论坛](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community) 或使用此页右侧的链接“记录问题”。

具有平台权限、沙盒和 [!DNL Postman] 设置，您已准备好 [模式数据](model-data-in-schemas.md)!
