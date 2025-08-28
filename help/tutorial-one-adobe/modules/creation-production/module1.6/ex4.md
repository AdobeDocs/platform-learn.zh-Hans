---
title: 部署代码并私下发布应用程序
description: 部署代码并私下发布应用程序
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 5a77ccdd-4000-4fb7-b696-dec40d01b41b
source-git-commit: 8219f3bd33448f90b87bf9ccb15738f1294e5965
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# 1.6.4部署代码并私下发布应用程序

私密发布应用程序意味着，您的应用程序可在GenStudio for Performance Marketing中使用，而无需使用查询字符串参数。

## 1.6.4.1发布您的应用程序

转到[https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects){target="_blank"}。

>[!NOTE]
>
> 以下屏幕截图显示了正在选择的特定组织。 在阅读本教程时，您的组织很可能具有不同的名称。 当您注册本教程时，系统已为您提供了要使用的环境详细信息，请按照这些说明操作。

使用App Builder打开Adobe IO项目，其名称应为`--aepUserLdap-- GSPeM EXT`。

![GSPeM可扩展性](./images/gspemextpub1.png)

转到&#x200B;**生产**。

![GSPeM可扩展性](./images/gspemextpub2.png)

单击&#x200B;**单独发布**。

![GSPeM可扩展性](./images/gspemextpub3.png)

然后，您需要填写多个字段。

![GSPeM可扩展性](./images/gspemextpub4.png)

填写以下字段，如下所示：

- **应用标题**： `--aepUserLdap-- - External DAM AWS S3`。
- **应用程序说明**： `External DAM AWS S3`
- **联系电子邮件**：输入您的电子邮件地址
- **应用程序图标**：下载并使用此图像： [S3图像](./images/s3.jpeg)
- **审核者注意**：外部DAM AWS S3

单击&#x200B;**提交**。

![GSPeM可扩展性](./images/gspemextpub5.png)

单击&#x200B;**提交**。

![GSPeM可扩展性](./images/gspemextpub6.png)

## 1.6.4.2批准您的应用程序

>[!IMPORTANT]
>
>此步骤只能由Adobe Admin Console中的系统管理员执行。 如果您不是系统管理员，则无法执行此命令。 请联系您的系统管理员以请求批准您的应用程序。

开发人员提交新应用程序以进行发布后，将会通知您组织的系统管理员，并会要求他们进行审查和批准。

如果您是系统管理员，将会收到此电子邮件，然后您可以单击&#x200B;**我的Exchange**&#x200B;以启动该进程。

![GSPeM可扩展性](./images/gspemextpub7.png)

在&#x200B;**Adobe Exchange**&#x200B;上，将显示App Builder应用程序，刚刚提交的应用程序正在等待审核。 单击应用程序&#x200B;**的**&#x200B;审核`--aepUserLdap-- - External DAM AWS S3`按钮。

![GSPeM可扩展性](./images/gspemextpub8.png)

添加评论并单击&#x200B;**批准**。

![GSPeM可扩展性](./images/gspemextpub9.png)

您的应用程序现已获得批准，并将在GenStudio for Performance Marketing中自动运行，无需指定查询字符串参数。

## 后续步骤

转到[摘要和优点](./summary.md){target="_blank"}

返回至[GenStudio for Performance Marketing — 可扩展性](./genstudioext.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
