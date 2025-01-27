---
title: PostBuster -Adobe员工
description: PostBuster -Adobe员工
doc-type: multipage-overview
exl-id: 01e30878-e1a9-4f46-bcf2-0074686ec1b5
source-git-commit: 54303033e23a28c45e9ef6c7a85135b21b3e29dc
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>以下说明仅适用于Adobe员工。

## 安装PostBuster

转到[https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542)。

单击以下载&#x200B;**PostBuster**&#x200B;的最新版本。

![PostBuster](./assets/images/pb1.png)

下载适用于您的操作系统的正确版本。

![PostBuster](./assets/images/pb2.png)

下载完成并安装后，打开PostBuster。 您应该会看到此内容。 单击&#x200B;**导入**。

![PostBuster](./assets/images/pb3.png)

下载[postbuster.json.zip](./assets/postman/postbuster.json.zip)并将其解压缩到桌面上。

![PostBuster](./assets/images/pbpb.png)

单击&#x200B;**选择文件**。

![PostBuster](./assets/images/pb4.png)

选择文件&#x200B;**postbuster.json**。 单击&#x200B;**打开**。

![PostBuster](./assets/images/pb5.png)

您应该会看到此内容。 单击&#x200B;**扫描**。

![PostBuster](./assets/images/pb6.png)

单击&#x200B;**导入**。

![PostBuster](./assets/images/pb7.png)

您应该会看到此内容。 单击以打开导入的收藏集。

![PostBuster](./assets/images/pb8.png)

现在，您可以看到自己的收藏集。 您仍需要配置环境以保存某些环境变量。

![PostBuster](./assets/images/pb9.png)

单击&#x200B;**基本环境**，然后单击&#x200B;**编辑**&#x200B;图标。

![PostBuster](./assets/images/pb10.png)

您应该会看到此内容。

![PostBuster](./assets/images/pb11.png)

复制以下环境占位符并将其粘贴到&#x200B;**基本环境**&#x200B;中。

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

然后您应该拥有此项。

![PostBuster](./assets/images/pb12.png)

完成&#x200B;**Firefly服务**&#x200B;模块后，您的环境应如下所示。 您现在不需要执行此操作，将在稍后阶段解决此问题。

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![技术内部人士](./assets/images/techinsiders.png){width="50px" align="left"}
>
>如果您有任何疑问，希望分享对未来内容提出建议的一般反馈，请直接联系技术业内人士，方式是向&#x200B;**techinsiders@adobe.com**&#x200B;发送电子邮件。

[返回所有模块](./overview.md)
