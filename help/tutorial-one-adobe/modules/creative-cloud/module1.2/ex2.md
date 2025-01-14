---
title: Firefly服务快速入门
description: Firefly服务快速入门
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: a0c16a47372d322a7931578adca30a246b537183
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---

# 1.2.2在Workfront Fusion中使用AdobeAPI

## 1.2.2.1通过Workfront Fusion使用Firefly文本到图像API

将鼠标悬停在第二个&#x200B;**设置多个变量**&#x200B;节点上，然后单击&#x200B;**+**&#x200B;以添加另一个模块。

![WF Fusion](./images/wffusion48.png)

搜索&#x200B;**http**，然后选择&#x200B;**HTTP**。

![WF Fusion](./images/wffusion49.png)

选择&#x200B;**发出请求**。

![WF Fusion](./images/wffusion50.png)

选择以下变量：

- **URL**： `https://firefly-api.adobe.io/v3/images/generate`
- **方法**： `POST`

单击&#x200B;**添加标题**。

![WF Fusion](./images/wffusion51.png)

您需要输入以下标题：

| 键 | 值 |
|:-------------:| :---------------:| 
| `x-api-key` | 您为`CONST_client_id`存储的变量 |
| `Authorization` | `Bearer ` +您为`bearer_token`存储的变量 |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

输入`x-api-key`的详细信息。 单击&#x200B;**添加**。

![WF Fusion](./images/wffusion52.png)

单击&#x200B;**添加标题**。

![WF Fusion](./images/wffusion53.png)

输入`Authorization`的详细信息。 单击&#x200B;**添加**。

![WF Fusion](./images/wffusion54.png)

单击&#x200B;**添加标题**。 输入`Content-Type`的详细信息。 单击&#x200B;**添加**。

![WF Fusion](./images/wffusion541.png)

单击&#x200B;**添加标题**。 输入`Accept`的详细信息。 单击&#x200B;**添加**。

![WF Fusion](./images/wffusion542.png)

将&#x200B;**Body类型**&#x200B;设置为&#x200B;**Raw**。 对于&#x200B;**内容类型**，请选择&#x200B;**JSON (application/json)**。

![WF Fusion](./images/wffusion55.png)

将此有效负载粘贴到&#x200B;**请求内容**&#x200B;字段中。

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

选中&#x200B;**分析响应**&#x200B;的复选框。 单击&#x200B;**确定**。

![WF Fusion](./images/wffusion56.png)

单击&#x200B;**运行一次**。

![WF Fusion](./images/wffusion57.png)

场景运行后，您应该会看到此内容。

![WF Fusion](./images/wffusion58.png)

单击&#x200B;**？第四个节点HTTP上的**&#x200B;图标以查看响应。 您应该会在响应中看到图像文件。

![WF Fusion](./images/wffusion59.png)

复制图像URL并在浏览器窗口中将其打开。 然后，您应该会看到如下所示的内容：

![WF Fusion](./images/wffusion60.png)

右键单击&#x200B;**HTTP**&#x200B;对象并将其重命名为&#x200B;**FireflyT2I**。

![WF Fusion](./images/wffusion62.png)

单击&#x200B;**保存**&#x200B;以保存更改。

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2将Photoshop API用于Workfront Fusion

单击&#x200B;**设置持有者令牌**&#x200B;和&#x200B;**FireflyT2I**&#x200B;之间的&#x200B;**扳手**&#x200B;图标。 选择&#x200B;**添加路由器**。

![WF Fusion](./images/wffusion63.png)

右键单击&#x200B;**FireflyT2I**&#x200B;对象并选择&#x200B;**克隆**。

![WF Fusion](./images/wffusion64.png)

将克隆的对象拖放到&#x200B;**Router**&#x200B;对象附近，它将自动连接到&#x200B;**Router**。 然后您应该拥有此项。

![WF Fusion](./images/wffusion65.png)

您现在具有基于&#x200B;**FireflyT2I** HTTP请求的相同副本。 **FireflyT2I** HTTP请求的某些设置类似于与&#x200B;**Photoshop API**&#x200B;交互所需的设置，后者是节省时间的。 现在，您只需更改不相同的变量即可，例如请求URL和有效负载。

将&#x200B;**URL**&#x200B;更改为`https://image.adobe.io/pie/psdService/text`。

![WF Fusion](./images/wffusion66.png)

使用以下有效负载替换&#x200B;**请求内容**：

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

为了使此&#x200B;**请求内容**&#x200B;正常工作，缺少一些变量：

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

返回第一个节点，单击&#x200B;**初始化常量**，然后为每个变量选择&#x200B;**添加项**。

![WF Fusion](./images/wffusion69.png)

| 键 | 示例值 |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

您可以通过返回Postman并打开&#x200B;**环境变量**&#x200B;来查找变量。

![Azure存储](./../module1.1/images/az105.png)

将这些值复制到Workfront Fusion，并为这4个变量中的每一个添加新项。

然后您应该拥有此项。 单击&#x200B;**确定**。

![WF Fusion](./images/wffusion68.png)

接下来，返回克隆的HTTP请求以更新&#x200B;**请求内容**。 您会在&#x200B;**请求内容**&#x200B;中注意到这些黑色变量，它们是从Postman复制的变量。 现在，您需要将这些变量更改为之前在Workfront Fusion中定义的变量。 通过删除黑色文本并用正确的变量替换它，逐一替换每个变量。

![WF Fusion](./images/wffusion70.png)

在&#x200B;**输入**&#x200B;部分中有3项更改要进行。

![WF Fusion](./images/wffusion71.png)

**输出**&#x200B;部分还有3项要做的更改。 单击&#x200B;**确定**。

![WF Fusion](./images/wffusion72.png)

右键单击克隆的节点，然后选择&#x200B;**重命名**。 将名称更改为&#x200B;**Photoshop更改文本**。

![WF Fusion](./images/wffusion73.png)

然后您应该拥有此项。

![WF Fusion](./images/wffusion74.png)

下一步： [1.2.3 ...](./ex3.md)

[返回模块1.2](./automation.md)

[返回所有模块](./../../../overview.md)
