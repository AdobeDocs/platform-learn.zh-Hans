---
title: Content Production Agent
description: Content Production Agent
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: 7ea3bdc9557ea9e88ddd9693f9ffbfbc634857f8
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# 1.6.1 AEM Agent快速入门

>[!IMPORTANT]
>
>要完成此练习，您需要有权访问有效的AEM Sites和具有EDS环境的Assets CS ，并且需要为您使用的IMS组织启用各种AEM代理。
>
>如果您还没有这样的环境，请转到练习[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照上面的说明进行操作，您将有权访问此类环境。

>[!IMPORTANT]
>
>如果您之前已使用AEM Sites和AEM CS环境配置了Assets CS项目，则可能是您的AEM CS沙盒已休眠。 鉴于解除此类沙盒的休眠需要10-15分钟，最好现在就启动解除休眠过程，这样以后就不必等待它。

## 1.6.1.1发现代理

Adobe Experience Manager (AEM) Discovery Agent是AEM as a Cloud Service中由AI提供支持的工具，它使用户能够使用自然语言提示查找、检索和利用内容，包括Assets、内容片段和自适应Forms。 通过了解整个存储库的意图和搜索，无需进行手动、繁重点击或复杂的筛选。

为了使用&#x200B;**发现代理**，您将首先在Adobe Experience Manager中创建一些标记，然后使用这些标记标记标记一些资源。 完成此操作后，您将能够使用AI助手以简单且商业友好的方式发现资产。

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 您应选择的组织是`--aepImsOrgName--`。

### 在Assets中创建和使用标记

单击以打开您的Cloud Manager项目，该项目应称为`--aepUserLdap-- - CitiSignal AEM+ACCS`。

![AEM代理](./images/aemagents1.png)

单击环境的URL以将其打开。

![AEM代理](./images/aemagents2.png)

单击&#x200B;**锤子**&#x200B;图标。

![AEM代理](./images/aemagents3.png)

在&#x200B;**常规**&#x200B;下，单击&#x200B;**标记**。

![AEM代理](./images/aemagents4.png)

您应该会看到此内容。 单击&#x200B;**创建**，然后选择&#x200B;**创建命名空间**。

![AEM代理](./images/aemagents5.png)

在&#x200B;**标题**&#x200B;字段中，输入： `CitiSignal`。 单击&#x200B;**创建**。

![AEM代理](./images/aemagents6.png)

通过单击命名空间&#x200B;**CitiSignal**&#x200B;可深入查看该命名空间。 单击&#x200B;**创建**，然后选择&#x200B;**创建标记**。

![AEM代理](./images/aemagents7.png)

在&#x200B;**标题**&#x200B;字段中，输入： `Campaign`。 单击&#x200B;**提交**。

![AEM代理](./images/aemagents8.png)

单击标记&#x200B;**Campaign**&#x200B;以将其选中。 单击&#x200B;**创建**，然后选择&#x200B;**创建标记**。

![AEM代理](./images/aemagents9.png)

在&#x200B;**标题**&#x200B;字段中，输入： `Winter 2026`。 单击&#x200B;**提交**。

![AEM代理](./images/aemagents10.png)

单击标记&#x200B;**Campaign**&#x200B;以将其选中。 单击&#x200B;**创建**，然后选择&#x200B;**创建标记**。

![AEM代理](./images/aemagents11.png)

在&#x200B;**标题**&#x200B;字段中，输入： `Spring 2026`。 单击&#x200B;**提交**。

![AEM代理](./images/aemagents12.png)

您现在应该拥有此项。

![AEM代理](./images/aemagents13.png)

单击&#x200B;**Adobe Experience Manager**，然后单击&#x200B;**Assets**。

![AEM代理](./images/aemagents14.png)

单击&#x200B;**文件**。

![AEM代理](./images/aemagents15.png)

双击文件夹&#x200B;**CitiSignal**&#x200B;以将其打开。

![AEM代理](./images/aemagents16.png)

单击&#x200B;**创建**，然后选择&#x200B;**文件**。

![AEM代理](./images/aemagents17.png)

下载文件[citisignal-images-campaign.zip](./assets/citisignal-images-campaign.zip)并将其解压缩到桌面上。

![AEM代理](./images/aemagents17a.png)

选择。 您刚刚下载的3个文件，然后单击&#x200B;**打开**。

![AEM代理](./images/aemagents18.png)

单击&#x200B;**上传**。

![AEM代理](./images/aemagents19.png)

您应该会看到此内容。

![AEM代理](./images/aemagents20.png)

选择第一个图像，然后单击&#x200B;**属性**。

![AEM代理](./images/aemagents21.png)

单击“标记”下的&#x200B;**文件夹**&#x200B;图标。

![AEM代理](./images/aemagents22.png)

选择标记&#x200B;**Spring 2026**，然后单击&#x200B;**选择**。 对这些图像重复该过程：

- citisignal_lion.png
- citisignal_leopard.png
- citisignal_gorilla.png
- citisignal_rabbit.png

![AEM代理](./images/aemagents23.png)

为所有图像选择该标记后，请转到&#x200B;**Experience Manager Assets**。

![AEM代理](./images/aemagents24.png)

选择您正在使用的存储库。

![AEM代理](./images/aemagents25.png)

转到&#x200B;**Assets**&#x200B;并打开文件夹&#x200B;**CitiSignal**。

![AEM代理](./images/aemagents26.png)

打开第一个图像。

![AEM代理](./images/aemagents27.png)

选择&#x200B;**已批准**，然后单击&#x200B;**保存**。

![AEM代理](./images/aemagents28.png)

在&#x200B;**标记**&#x200B;下，您可以看到之前选择的标记。

![AEM代理](./images/aemagents29.png)

重复该过程，以便所有4个图像都获得批准。

![AEM代理](./images/aemagents30.png)

接下来，转到&#x200B;**我的工作区**，然后单击以打开&#x200B;**AI助手**。

![AEM代理](./images/aemagents31.png)

输入以下提示并单击&#x200B;**发送**。

```javascript
find all assets tagged with 'Spring 2026'
```

![AEM代理](./images/aemagents32.png)

如果您有权访问多个AEM Assets CS环境，您将看到类似以下内容。 单击要使用的环境的建议答案，然后单击&#x200B;**发送**。

![AEM代理](./images/aemagents34.png)

您应该会看到类似的答案。 单击图标可将AI助手展开到全屏。

![AEM代理](./images/aemagents35.png)

查看答案。

![AEM代理](./images/aemagents36.png)

在AI Assistant窗口中，您可以单击查看其中的任何资源。

![AEM代理](./images/aemagents37.png)

然后，您将直接转到AEM Assets CS中查看特定图像。

![AEM代理](./images/aemagents38.png)

然后，您还可以查看任何其他可用的元数据。

![AEM代理](./images/aemagents39.png)

## 1.6.1.2 Experience生产代理

### 内容更新

内容更新技能可以轻松更新现有内容，包括内容片段、页面、表单和资产。 代理可以执行更新、删除、替换或添加内容元素等操作，以保持体验准确且最新。 输入可以是自然语言描述，在与Jira PDF一起使用时，屏幕截图也可以提供输入。

返回到AI助手屏幕。

![AEM代理](./images/aemagents40.png)

输入以下提示并单击&#x200B;**发送**。

`Generate multiple social media formats (Instagram 1080x1920, Facebook 1200x630, Twitter 1200x675) for the third image`

![AEM代理](./images/aemagents40a.png)

几分钟后，您应该会看到类似的响应。

![AEM代理](./images/aemagents41.png)

查看生成的图像。

![AEM代理](./images/aemagents42.png)

### 表单创建

表单创建技能使用户能够通过自然语言提示构建自适应表单，而无需依赖开发或IT团队。 此功能可加快表单开发，同时保持品牌一致性，并允许业务用户在不具备深入的技术产品知识的情况下创建表单。


## 后续步骤

返回[AEM和代理](./aemagents.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
