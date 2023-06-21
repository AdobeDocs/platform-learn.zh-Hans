---
title: 验证和访问 Experience Platform API
description: 了解如何访问 Adobe Experience Platform API。
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 15%

---

# 身份验证和访问 [!DNL Experience Platform] API

要向Adobe Experience Platform API发出请求，您必须具有Experience Platform开发人员帐户。

## 在Adobe Developer控制台中创建项目并导出Postman环境

[[!DNL Postman]](https://www.postman.com/) 是一款允许开发人员快速轻松地与Adobe Experience Platform API进行交互的工具。

Adobe Developer控制台的 **导出Postman的详细信息** 通过功能，可以轻松地在一个Postman Environment文件中导出访问某个Experience PlatformAPI并与之交互所需的所有帐户详细信息，从而无需从Adobe Developer Console复制值并将其粘贴到Postman中。

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>创建API凭据后，公司的系统管理员必须将该凭据与Experience Platform角色关联。


## 使用Postman生成访问令牌

使用 [AdobeIdentity Management服务API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 获取访问Adobe Experience Platform API的访问令牌。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## 使用Postman与Experience PlatformAPI交互

探索使用与Adobe Experience Platform API交互 [Adobe提供的Experience PlatformAPI Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，构建在 [Adobe Developer控制台环境变量](#export-adobe-io-integration-details-to-postman) 和 [生成的访问令牌](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## 其他资源

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman示例](https://github.com/adobe/experience-platform-postman-samples)
   * [用于生成访问令牌的Identity Management System Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [下载Postman](https://www.postman.com/)
