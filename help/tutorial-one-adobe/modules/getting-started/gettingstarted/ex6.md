---
title: 快速入门 — Adobe I/O
description: 快速入门 — Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: 3b6ae4bb4eb2d9f189438dddc461bb0f2a0a9aac
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 配置Adobe I/O项目

## 创建您的Adobe I/O项目

在本练习中，Adobe I/O用于查询各种Adobe端点。 按照以下步骤设置Adobe I/O。

转到[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新集成](./images/iohome.png){zoomable="yes"}

确保在屏幕右上角选择正确的实例。 您的实例为`--aepImsOrgName--`。

>[!NOTE]
>
> 以下屏幕截图显示了正在选择的特定组织。 在阅读本教程时，您的组织很可能具有不同的名称。 当您注册本教程时，系统已为您提供了要使用的环境详细信息，请按照这些说明操作。

接下来，选择&#x200B;**新建项目**。

![Adobe I/O新集成](./images/iocomp.png){zoomable="yes"}

### FIREFLY SERVICES API

您应该会看到此内容。 选择&#x200B;**+添加到项目**&#x200B;并选择&#x200B;**API**。

![Adobe I/O新集成](./images/adobe_io_access_api.png){zoomable="yes"}

您的屏幕应如下所示。

![Adobe I/O新集成](./images/api1.png){zoomable="yes"}

选择&#x200B;**Creative Cloud**&#x200B;并选择&#x200B;**Firefly - Firefly Services**，然后选择&#x200B;**下一步**。

![Adobe I/O新集成](./images/api3.png){zoomable="yes"}

为您的凭据提供一个名称： `--aepUserLdap-- - One Adobe OAuth credential`并选择&#x200B;**下一步**。

![Adobe I/O新集成](./images/api4.png){zoomable="yes"}

选择默认配置文件&#x200B;**默认Firefly Services配置**，然后选择&#x200B;**保存配置的API**。

![Adobe I/O新集成](./images/api9.png){zoomable="yes"}

您应该会看到此内容。

![Adobe I/O新集成](./images/api10.png){zoomable="yes"}

### PHOTOSHOP SERVICES API

选择&#x200B;**+添加到项目**，然后选择&#x200B;**API**。

![Azure存储](./images/ps2.png){zoomable="yes"}

选择&#x200B;**Creative Cloud**，然后选择&#x200B;**Photoshop - Firefly Services**。 选择&#x200B;**下一步**。

![Azure存储](./images/ps3.png){zoomable="yes"}

选择&#x200B;**下一步**。

![Azure存储](./images/ps4.png){zoomable="yes"}

接下来，您需要选择一个产品配置文件，以定义此集成可用的权限。

选择&#x200B;**默认Firefly Services配置**&#x200B;和&#x200B;**默认Creative Cloud自动化服务配置**。

选择&#x200B;**保存配置的API**。

![Azure存储](./images/ps5.png){zoomable="yes"}

您应该会看到此内容。

![Adobe I/O新集成](./images/ps7.png){zoomable="yes"}

### ADOBE EXPERIENCE PLATFORM API

选择&#x200B;**+添加到项目**，然后选择&#x200B;**API**。

![Azure存储](./images/aep1.png){zoomable="yes"}

选择&#x200B;**Adobe Experience Platform**，然后选择&#x200B;**Experience Platform API**。 选择&#x200B;**下一步**。

![Azure存储](./images/aep2.png){zoomable="yes"}

选择&#x200B;**下一步**。

![Azure存储](./images/aep3.png){zoomable="yes"}

接下来，您需要选择一个产品配置文件，以定义此集成可用的权限。

选择&#x200B;**Adobe Experience Platform — 所有用户 — PROD**。

>[!NOTE]
>
>AEP的产品配置文件的名称取决于环境的配置方式。 如果您没有看到上述产品配置文件，则可能有一个名为&#x200B;**默认的生产所有访问权限**&#x200B;的产品配置文件。 如果您不确定要选择哪一个，请咨询您的AEP系统管理员。

选择&#x200B;**保存配置的API**。

![Azure存储](./images/aep4.png){zoomable="yes"}

您应该会看到此内容。

![Adobe I/O新集成](./images/aep5.png){zoomable="yes"}

### 项目名称

单击您的项目名称。

![Adobe I/O新集成](./images/api13.png){zoomable="yes"}

选择&#x200B;**编辑项目**。

![Adobe I/O新集成](./images/api14.png){zoomable="yes"}

为您的集成输入友好名称： `--aepUserLdap-- One Adobe tutorial`，然后选择&#x200B;**保存**。

![Adobe I/O新集成](./images/api15.png){zoomable="yes"}

Adobe I/O项目的设置现已完成。

![Adobe I/O新集成](./images/api16.png){zoomable="yes"}

## 后续步骤

转到[选项1：Postman设置](./ex7.md){target="_blank"}

转到[选项2：PostBuster设置](./ex8.md){target="_blank"}

返回[开始使用](./getting-started.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
