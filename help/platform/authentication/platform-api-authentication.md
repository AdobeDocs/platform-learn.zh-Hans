---
title: 验证和访问 Experience Platform API
description: 了解如何访问 Adobe Experience Platform API。
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 10%

---

# 身份验证和访问 [!DNL Experience Platform] API

要调用Adobe Experience Platform API，您必须先获取Experience Platform开发人员帐户的访问权限。

有关如何获取开发人员帐户访问权限的分步说明，请访问 [Experience PlatformAPI身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 创建Experience PlatformAPI并将其导出到Postman

[Postman](https://www.getpostman.com/) 是一个工具，允许开发人员快速轻松地与Adobe Experience Platform API交互。

Adobe Developer Console **导出详细信息Postman** 该功能提供了一种轻松的方法，可导出在单个Postman环境文件中访问Experience PlatformAPI并与之交互所需的所有帐户详细信息，从而无需将值从Adobe Developer控制台复制并粘贴到Postman中。

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## 使用Postman生成访问令牌

使用 [AdobeIdentity Management服务API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 获取访问令牌以访问非生产用的Adobe Experience Platform API

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> 如Adobe I/O访问令牌生成Postman集合中所述，表示的生成方法适用于非生产用途。 本地签名从第三方主机加载JavaScript库，远程签名将私钥发送给Adobe拥有和运行的Web服务。 虽然Adobe不存储此私钥，但生产密钥绝不应与任何人共享。

## 使用Postman与Adobe I/OAPI交互

探索与Adobe I/OAPI交互的方法 [Adobe提供的Experience PlatformAPI Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，在 [Adobe I/O环境变量](#export-adobe-io-integration-details-to-postman) 和 [生成的访问令牌](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

请注意，并非每个Adobe I/OAPI都存在Adobe提供的Postman集合，但提供的 [Experience PlatformAPI Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) 可用作有关如何为这些用例定义您自己的Postman收藏集的指南。

## 其他资源

* [Adobe I/O控制台](https://console.adobe.io)
* [Adobe Experience Platform Postman示例](https://github.com/adobe/experience-platform-postman-samples)
   * [Adobe I/O访问令牌生成Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [下载Postman](https://www.getpostman.com/)
