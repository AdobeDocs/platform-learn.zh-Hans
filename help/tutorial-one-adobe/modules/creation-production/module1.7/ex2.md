---
title: 以编程方式执行自定义工作流
description: 以编程方式执行自定义工作流
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2以编程方式执行自定义工作流

## 1.7.2.1使用Postman执行自定义工作流

在上一个练习中发布工作流后，您应会看到类似以下的内容。 单击&#x200B;**复制**&#x200B;按钮以复制示例有效负载。

![Firefly自定义工作流](./images/ffcw61.png)

打开Postman并使用名称&#x200B;**Firefly自定义工作流**&#x200B;创建新的&#x200B;**收藏集**。 然后单击&#x200B;**添加请求**。

![Firefly自定义工作流](./images/ffcw62.png)

然后，您应该会看到一个新的空请求。 在地址栏中，粘贴您从已发布工作流复制的有效负载。

Postman将识别您粘贴的cURL命令，并从有效负载中获取所有信息，然后以正确的方式将其添加到请求中。

![Firefly自定义工作流](./images/ffcw63.png)

您现在应会看到这些&#x200B;**标头**&#x200B;变量。

![Firefly自定义工作流](./images/ffcw64.png)

转到&#x200B;**Body**，您应在该处看到与此类似的内容。

![Firefly自定义工作流](./images/ffcw65.png)

您现在需要在本请求正文中提供所需的说明。 以编程方式处理文件时，需要使用预签名URL。 在本练习中，您可以在下面找到本练习中包含的3个图像的预签名URL。 这些预签名URL是使用Microsoft Azure存储功能创建的。 如果您想了解有关如何创建预签名URL的更多信息，请访问此处：[使用Microsoft Azure和预签名URL优化Firefly过程](./../module1.1/ex2.md)。

在本练习中，您可以使用以下URL，这样您就不需要自己创建新的预签名URL。

- **airpods.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **phone.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

您还需要在Postman请求中提供提示。 以下是您可以使用的提示。

- **提示1**：

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **提示2**：

```
background hearts fluttering
```

这是一个有效负载示例，但由于&#x200B;**node_id**&#x200B;字段是您的工作流所独有的，因此您不能复制和重复使用它，这样做只是为了让您了解有效负载的外观：

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

在对有效负载进行更改后，它应该如下所示。 完成后，单击&#x200B;**发送**。 然后，使用&#x200B;**CMD + S**&#x200B;或&#x200B;**CTRL + S**&#x200B;来&#x200B;**保存**&#x200B;您的请求。

![Firefly自定义工作流](./images/ffcw66.png)

在响应有效负载中，您现在可以找到几个链接。 通过这些链接可以查询工作流的&#x200B;**状态**，一旦状态为&#x200B;**已完成**，则可以使用&#x200B;**结果** URL检索生成的图像和视频。

选择&#x200B;**状态** URL并复制它。

![Firefly自定义工作流](./images/ffcw67.png)

单击当前使用的请求上的3个圆点，然后选择&#x200B;**复制**。

![Firefly自定义工作流](./images/ffcw69.png)

在新请求中，将请求类型更改为&#x200B;**GET**，并用您刚刚复制的状态URL替换URL。

![Firefly自定义工作流](./images/ffcw70.png)

在&#x200B;**正文**&#x200B;下，确保已删除所有内容。 然后，单击&#x200B;**发送**。 然后，您应会收到一个类似的响应有效负载，该有效负载将显示状态。 您可以重新发送此请求，直到状态更改为&#x200B;**已完成**。 不要忘记使用&#x200B;**CMD + S**&#x200B;或&#x200B;**CTRL + S**&#x200B;来&#x200B;**保存**&#x200B;您的请求。

![Firefly自定义工作流](./images/ffcw71.png)

返回第一个&#x200B;**POST**&#x200B;请求。 现在复制&#x200B;**结果** URL。

![Firefly自定义工作流](./images/ffcw72.png)

在您创建的第二个请求上单击这3个点&#x200B;**...**，然后选择&#x200B;**复制**。

![Firefly自定义工作流](./images/ffcw73.png)

在新请求中，粘贴您复制的&#x200B;**结果** URL，然后单击&#x200B;**发送**。 不要忘记使用&#x200B;**CMD + S**&#x200B;或&#x200B;**CTRL + S**&#x200B;来&#x200B;**保存**&#x200B;您的请求。

![Firefly自定义工作流](./images/ffcw74.png)

在响应有效负载中向下滚动，您将在该有效负载中找到对已创建图像和视频的引用。 单击链接以打开这些文件。

![Firefly自定义工作流](./images/ffcw75.png)

这是生成的图像。

![Firefly自定义工作流](./images/ffcw76.png)

## 1.7.2.2使用Workfront Fusion执行自定义工作流

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 打开&#x200B;**Workfront Fusion**。

![WF Fusion](./images/wffusion1.png)

转到&#x200B;**方案**。 如果您还没有文件夹，请创建一个文件夹，并为该文件夹名称使用： `--aepUserLdap--`。 选择您的文件夹，然后选择&#x200B;**创建新方案**。

![WF Fusion](./images/wffusion2.png)

您应该会看到此内容。

![WF Fusion](./images/wffusion3.png)

在上一个练习中发布工作流后，您应会看到类似以下的内容。 单击&#x200B;**复制**&#x200B;按钮以复制示例有效负载。

![Firefly自定义工作流](./images/ffcw61.png)

返回到Workfront Fusion场景。 使用&#x200B;**CMD + V**&#x200B;或&#x200B;**CTRL + V**&#x200B;将您复制的有效负载粘贴到方案中。 Workfront Fusion将自动检测cURL请求，并将创建一个新的&#x200B;**HTTP — 自动发出请求**&#x200B;模块。

将&#x200B;**clock**&#x200B;图标拖动到&#x200B;**HTTP — 发出请求**&#x200B;模块。

![WF Fusion](./images/wffusion5.png)

您应该会看到此内容。 单击&#x200B;**HTTP — 发出请求**&#x200B;模块以将其打开。

![WF Fusion](./images/wffusion6.png)

然后，您应该看到&#x200B;**标头**&#x200B;变量已经可用。

![WF Fusion](./images/wffusion7.png)

向下滚动以查看默认有效负载。 单击指示的&#x200B;**图标**&#x200B;以美化JSON有效负载。

![WF Fusion](./images/wffusion8.png)

返回Postman，返回第一个&#x200B;**POST**&#x200B;请求。 复制有效负载。

![WF Fusion](./images/wffusion9.png)

返回到Workfront Fusion场景。 使用您从Postman复制的有效负载替换现有的默认有效负载。 单击指示的&#x200B;**图标**&#x200B;以美化JSON有效负载。

选中&#x200B;**分析响应**&#x200B;的复选框。

单击&#x200B;**确定**。

![WF Fusion](./images/wffusion10.png)

保存更改，然后单击&#x200B;**运行一次**。

![WF Fusion](./images/wffusion11.png)

场景运行后，您可以看到与您在Postman中得到的响应类似。 由于此信息可在Workfront Fusion中使用，您现在可以基于此信息轮询&#x200B;**状态** URL，直到状态完成，一旦完成，您即可使用&#x200B;**结果** URL收集生成的图像和视频。

![WF Fusion](./images/wffusion12.png)

## 后续步骤

返回[Firefly自定义工作流](./workflowbuilder.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
