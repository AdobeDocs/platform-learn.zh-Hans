---
title: 验证和访问 Experience Platform API
description: 了解如何访问 Adobe Experience Platform API。
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# 身份验证和访问[!DNL Experience Platform] API

了解如何开始使用Adobe Experience Platform API。 本教程将指导您完成创建身份验证凭据并开始发出Experience Platform API请求的过程。

## 在Adobe Developer Console中创建项目并导出Postman环境{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/)是第三方应用程序，可帮助开发人员快速轻松地与Adobe Experience Platform API交互。

[Adobe Developer Console的](https://developer.adobe.com/console/home) **Postman的导出详细信息**&#x200B;功能提供了一种简单的方法，可以将访问单个Postman环境文件中与Experience Platform API交互所需的帐户详细信息导出，从而无需将值从Adobe Developer Console复制粘贴到Postman中。

>[!IMPORTANT]
>
>要访问[Adobe Developer Console](https://developer.adobe.com/console/home)，您必须是[Adobe Admin Console](https://adminconsole.adobe.com)中的[系统管理员](https://helpx.adobe.com/enterprise/using/admin-roles.html)或[开发人员](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.)。
>
> 创建API凭据后，系统管理员必须将该凭据与Experience Platform中的角色关联。

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&enablevpops)

## 使用Postman生成访问令牌{#generate-an-access-token-with-postman}

使用[Adobe Identity Management服务API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)获取访问令牌以访问Adobe Experience Platform API。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on&enablevpops)


## 使用Postman与Experience Platform API交互

利用[Adobe Experience Platform环境变量](#export-integration-details-to-postman)和[生成的访问令牌](#generate-an-access-token-with-postman)，探索使用[Adobe提供的Experience Platform API Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)与Adobe Developer Console API交互。

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on&enablevpops)


## 这些视频中引用的资源

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman示例](https://github.com/adobe/experience-platform-postman-samples)
   * 用于生成访问令牌的[Identity Management System Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [下载Postman](https://www.postman.com/)
