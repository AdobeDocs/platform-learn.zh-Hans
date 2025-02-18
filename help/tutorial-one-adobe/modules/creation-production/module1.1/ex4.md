---
title: Firefly自定义模型API
description: 使用Firefly自定义模型API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 330f4492-d0df-4298-9edc-4174b0065c9a
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# 1.1.4 Firefly自定义模型API

## 1.1.4.1配置自定义模型

转到[https://firefly.adobe.com/](https://firefly.adobe.com/)。 单击&#x200B;**自定义模型**。

![Firefly自定义模型](./images/ffcm1.png){zoomable="yes"}

您可能会看到此消息。 如果是，请单击&#x200B;**同意**&#x200B;以继续。

![Firefly自定义模型](./images/ffcm2.png){zoomable="yes"}

您应该会看到此内容。 单击&#x200B;**训练模型**。

![Firefly自定义模型](./images/ffcm3.png){zoomable="yes"}

配置以下字段：

- **名称**：使用`--aepUserLdap-- - Citi Signal Router Model`
- **培训模式**：选择&#x200B;**主题（技术预览）**
- **概念**：输入`router`
- **保存到**：打开下拉列表并单击&#x200B;**+新建项目**

![Firefly自定义模型](./images/ffcm4.png){zoomable="yes"}

为新项目提供一个名称： `--aepUserLdap-- - Custom Models`。 单击&#x200B;**创建**。

![Firefly自定义模型](./images/ffcm5.png){zoomable="yes"}

您应该会看到此内容。 单击&#x200B;**创建**。

![Firefly自定义模型](./images/ffcm6.png){zoomable="yes"}

现在，您需要提供参考图像以便对自定义模型进行培训。 单击&#x200B;**从您的计算机中选择图像**。

![Firefly自定义模型](./images/ffcm7.png){zoomable="yes"}

在[此处](https://tech-insiders.s3.us-west-2.amazonaws.com/CitiSignal_router.zip)下载参考图像。 解压缩下载文件，这将为您提供此内容。

![Firefly自定义模型](./images/ffcm8.png){zoomable="yes"}

导航到包含下载的图像文件的文件夹。 全部选择并单击&#x200B;**打开**。

![Firefly自定义模型](./images/ffcm9.png){zoomable="yes"}

然后，您会看到正在加载您的图像。

![Firefly自定义模型](./images/ffcm10.png){zoomable="yes"}

几分钟后，您的图像将正确加载。 您可能会看到某些图像有错误，这是由于图像的标题尚未生成或时间不够长所致。 检查每个有错误的图像，并输入符合要求并描述该图像的标题。

![Firefly自定义模型](./images/ffcm11.png){zoomable="yes"}

一旦所有图像都有符合要求的字幕，您仍需要提供示例提示。 输入使用“router”一词的任何提示。 完成此操作后，即可开始训练您的模型。 单击&#x200B;**训练**。

![Firefly自定义模型](./images/ffcm12.png){zoomable="yes"}

你会看到这个。 训练模型可能需要20-30分钟或更长时间。

![Firefly自定义模型](./images/ffcm13.png){zoomable="yes"}

20-30分钟后，您的模型将接受培训并可发布。 单击&#x200B;**发布**。

![Firefly自定义模型](./images/ffcm14.png){zoomable="yes"}

再次单击&#x200B;**发布**。

![Firefly自定义模型](./images/ffcm15.png){zoomable="yes"}

关闭&#x200B;**共享自定义模型**&#x200B;弹出窗口。

![Firefly自定义模型](./images/ffcm16.png){zoomable="yes"}

## 1.1.4.2在UI中使用自定义模型

转到[https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train)。 单击自定义模型以将其打开。

![Firefly自定义模型](./images/ffcm19.png){zoomable="yes"}

单击&#x200B;**预览和测试**。

![Firefly自定义模型](./images/ffcm17.png){zoomable="yes"}

然后，您将看到在执行之前输入的示例提示。

![Firefly自定义模型](./images/ffcm18.png){zoomable="yes"}

## 1.1.4.3为Firefly Services自定义模型API启用自定义模型

自定义模型一旦训练完成，也可以通过API使用。 在练习1.1.1中，您已配置Adobe I/O项目以通过API与Firefly服务交互。

转到[https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train)。 单击自定义模型以将其打开。

![Firefly自定义模型](./images/ffcm19.png){zoomable="yes"}

单击3个点&#x200B;**...**，然后单击&#x200B;**共享**。

![Firefly自定义模型](./images/ffcm20.png){zoomable="yes"}

要访问Firefly自定义模型，需要将该自定义模型共享到Adobe I/O项目的&#x200B;**技术帐户ID**。

要检索您的&#x200B;**技术帐户ID**，请转到[https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)。 单击以打开名为`--aepUserLdap-- Firefly`的项目。

![Firefly自定义模型](./images/ffcm24.png){zoomable="yes"}

单击&#x200B;**OAuth服务器到服务器**。

![Firefly自定义模型](./images/ffcm25.png){zoomable="yes"}

单击以复制您的&#x200B;**技术帐户ID**。

![Firefly自定义模型](./images/ffcm23.png){zoomable="yes"}

粘贴您的&#x200B;**技术帐户ID**&#x200B;并单击&#x200B;**邀请进行编辑**。

![Firefly自定义模型](./images/ffcm21.png){zoomable="yes"}

**技术帐户ID**&#x200B;现在应该能够访问自定义模型。

![Firefly自定义模型](./images/ffcm22.png){zoomable="yes"}

## 1.1.4.4与Firefly服务自定义模型API交互

在练习1.1.1的Firefly服务快速入门中，您已将此文件[postman-ff.zip](./../../../assets/postman/postman-ff.zip)下载到本地桌面，然后将该收藏集导入Postman。

打开Postman并转到文件夹&#x200B;**FF — 自定义模型API**。

![Firefly自定义模型](./images/ffcm30.png){zoomable="yes"}

打开请求&#x200B;**1。 FF - getCustomModels**&#x200B;并单击&#x200B;**发送**。

![Firefly自定义模型](./images/ffcm31.png){zoomable="yes"}

您应该看到之前创建的名为`--aepUserLdap-- - Citi Signal Router Model`的自定义模型作为响应的一部分。 字段&#x200B;**assetId**&#x200B;是自定义模型的唯一标识符，将在下一个请求中引用。

![Firefly自定义模型](./images/ffcm32.png){zoomable="yes"}

打开请求&#x200B;**2。 生成图像异步**。 在此示例中，您将请求根据自定义模型生成2个变体。 请随时更新在此例中为`a white router on a volcano in Africa`的提示。

单击&#x200B;**发送**。

![Firefly自定义模型](./images/ffcm33.png){zoomable="yes"}

响应包含字段&#x200B;**jobId**。 生成这2个图像的作业正在运行，您可以使用下一个请求来检查状态。

![Firefly自定义模型](./images/ffcm34.png){zoomable="yes"}

打开请求&#x200B;**3。 获取CM状态**&#x200B;并单击&#x200B;**发送**。 然后，您应该看到状态设置为正在运行。

![Firefly自定义模型](./images/ffcm35.png){zoomable="yes"}

几分钟后，再次单击请求&#x200B;**3的**&#x200B;发送&#x200B;**。 获取CM状态** 然后，您应该会看到状态更改为&#x200B;**succeeded**，并且在输出中应该会看到两个图像URL。 单击以打开这两个文件。

![Firefly自定义模型](./images/ffcm36.png){zoomable="yes"}

这是本示例中生成的第一个图像。

![Firefly自定义模型](./images/ffcm37.png){zoomable="yes"}

这是此示例中生成的第二个图像。

![Firefly自定义模型](./images/ffcm38.png){zoomable="yes"}

您现在已经完成了此练习。

## 后续步骤

转到[摘要和优点](./summary.md){target="_blank"}

返回至[使用Photoshop API](./ex3.md){target="_blank"}

返回[Adobe Firefly服务概述](./firefly-services.md){target="_blank"}
