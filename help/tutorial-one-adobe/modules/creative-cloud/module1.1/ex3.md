---
title: 使用Photoshop API
description: 了解如何使用Photoshop API和Firefly服务
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: 8e410ad378d61f23d1d880d12e57f9d5e4e523c1
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 使用Photoshop API

了解如何使用Photoshop API和Firefly服务。

## 更新您的Adobe I/O集成

1. 转到[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新集成](./images/iohome.png)

1. 转到&#x200B;**项目**，然后选择您在上一个练习中创建的项目，该项目名为`--aepUserLdap-- Firefly`。

![Azure存储](./images/ps1.png)

1. 选择&#x200B;**+添加到项目**，然后选择&#x200B;**API**。

![Azure存储](./images/ps2.png)

1. 选择&#x200B;**Creative Cloud**&#x200B;并选择&#x200B;**Photoshop -Firefly服务**。 选择&#x200B;**下一步**。

![Azure存储](./images/ps3.png)

1. 选择&#x200B;**下一步**。

![Azure存储](./images/ps4.png)

接下来，您需要选择一个产品配置文件，以定义此集成可用的权限。

1. 选择&#x200B;**默认Firefly服务配置**&#x200B;和&#x200B;**默认Creative Cloud自动化服务配置**。

1. 选择&#x200B;**保存配置的API**。

![Azure存储](./images/ps5.png)

您的Adobe I/O项目现已更新为使用Photoshop和Firefly服务API。

![Azure存储](./images/ps6.png)

## 以编程方式与PSD文件交互

1. 将[citisignal-fibre.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"}下载到桌面。

1. 在Photoshop中打开&#x200B;**citisignal-fibre.psd**。

![Azure存储](./images/ps7.png)

在&#x200B;**层**&#x200B;窗格中，文件的设计者为每个层提供了唯一的名称。 您可以通过在Photoshop中打开PSD文件来查看图层信息，但您也可以通过编程方式来查看图层信息。

让我们将您的第一个API请求发送到Photoshop API。

1. 在Postman中，在向Photoshop发送API请求之前，您需要对Adobe I/O进行身份验证。打开名为&#x200B;**POST的上一个请求 — 获取访问令牌**。

1. 转到&#x200B;**Params**&#x200B;并验证参数&#x200B;**Scope**&#x200B;是否设置正确。 **作用域**&#x200B;的&#x200B;**值**&#x200B;应如下所示：

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

1. 选择&#x200B;**发送**。

![Azure存储](./images/ps8.png)

现在，您拥有有效的访问令牌以与Photoshop API交互。

![Azure存储](./images/ps9.png)

### Photoshop API - Hello World

接下来，让我们向Photoshop API问好，以测试是否正确设置了所有权限和访问权限。

1. 在集合&#x200B;**Photoshop**&#x200B;中，打开请求&#x200B;**Photoshop Hello（测试身份验证）**&#x200B;的问题。选择&#x200B;**发送**。

![Azure存储](./images/ps10.png)

您应会收到响应&#x200B;**欢迎使用Photoshop API！**。

![Azure存储](./images/ps11.png)

接下来，为了以编程方式与PSD文件&#x200B;**citisignal-fibre.psd**&#x200B;交互，您需要将其上传到您的存储帐户。 您可以手动执行此操作，方法是使用Azure存储资源管理器将其拖放到容器中，但此时您应通过API执行此操作。

### 将PSD上传到Azure

1. 在Postman中，打开请求&#x200B;**将PSD上载到Azure Storage帐户**。 在上一个练习中，您已在Postman中配置这些环境变量，现在将使用这些变量：

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

正如您在请求&#x200B;**将PSD上载到Azure Storage Account**&#x200B;中看到的，URL已配置为使用这些变量。

![Azure存储](./images/ps12.png)

1. 在&#x200B;**主体**&#x200B;中，选择文件&#x200B;**citisignal-fiber.psd**。

![Azure存储](./images/ps13.png)

1. 您的屏幕应如下所示。 选择&#x200B;**发送**。

![Azure存储](./images/ps14.png)

您应从Azure中获取此空响应，这意味着您的文件存储在您的Azure存储帐户的容器中。

![Azure存储](./images/ps15.png)

如果使用Azure存储资源管理器查看文件，请确保刷新文件夹。

![Azure存储](./images/ps16.png)

### Photoshop API — 获取清单

接下来，您需要获取PSD文件的清单文件。

1. 在Postman中，打开请求&#x200B;**Photoshop — 获取PSD清单**。 转到&#x200B;**正文**。

正文应如下所示：

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "thumbnails": {
      "type": "image/jpeg"
    }
  }
}
```

1. 选择&#x200B;**发送**。

在响应中，您现在会看到一个链接。 由于Photoshop中的操作有时需要一些时间才能完成，因此Photoshop会提供状态文件作为对大多数传入请求的响应。 要了解您的请求发生了什么情况，您需要读取状态文件。

![Azure存储](./images/ps17.png)

1. 要读取状态文件，请打开请求&#x200B;**Photoshop — 获取PS状态**。 您可以看到此请求正在使用变量作为URL，该URL是由您发送的上一个请求&#x200B;**Photoshop — 获取PSD清单**&#x200B;设置的变量。 变量在每个请求的&#x200B;**脚本**&#x200B;中设置。 选择&#x200B;**发送**。

![Azure存储](./images/ps18.png)

您的屏幕应如下所示。 目前，状态设置为&#x200B;**挂起**，这意味着该进程尚未完成。

![Azure存储](./images/ps19.png)

1. 在&#x200B;**Photoshop — 获取PS状态**&#x200B;上再选择发送几次，直到状态更改为&#x200B;**succeeded**。 这可能需要几分钟的时间。

当响应可用时，您可以看到json文件包含有关PSD文件所有层的信息。 这是有用的信息，因为可以识别层名称或层ID等。

![Azure存储](./images/ps20.png)

例如，搜索文本`2048x2048-cta`。 屏幕应如下所示：

![Azure存储](./images/ps21.png)

### Photoshop API — 更改文本

接下来，您需要使用API更改行动号召的文本。

1. 在Postman中，打开请求&#x200B;**Photoshop — 更改文本**，然后转到&#x200B;**正文**。

屏幕应如下所示：

- 首先，指定了输入文件： `citisignal-fiber.psd`
- 其次，指定要更改的图层，文本将更改为
- 第三，指定了输出文件： `citisignal-fiber-changed-text.psd`

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

输出文件的名称不同，因为您不想覆盖原始输入文件。

1. 选择&#x200B;**发送**。

![Azure存储](./images/ps23.png)

与之前一样，响应包含一个指向跟踪进度的状态文件的链接。

![Azure存储](./images/ps22.png)

1. 要读取状态文件，请打开请求&#x200B;**Photoshop — 获取PS状态**，然后选择&#x200B;**发送**。 如果状态未立即设置为&#x200B;**succeeded**，请等待几秒钟，然后再次选择&#x200B;**发送**。

1. 选择用于下载输出文件的URL。

![Azure存储](./images/ps24.png)

1. 将文件下载到计算机后，打开&#x200B;**citisignal-fibre-changed-text.psd**。 您应该会看到行动号召的占位符已被文本&#x200B;**立即获取Fiber！**&#x200B;替换。

![Azure存储](./images/ps25.png)

您还可以使用Azure存储资源管理器在容器中查看此文件。

![Azure存储](./images/ps26.png)

## 后续步骤

转到[Firefly自定义模型API](./ex4.md){target="_blank"}

返回[Adobe Firefly服务概述](./firefly-services.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}