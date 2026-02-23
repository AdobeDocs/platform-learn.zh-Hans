---
title: 创建您的第一个表单
description: 创建您的第一个表单
kt: 5342
doc-type: tutorial
source-git-commit: 8f59b9fdadc9c5aeadb1d4ecccd75090c339b43e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 9%

---

# 1.3.1创建您的第一个表单

>[!IMPORTANT]
>
>要完成本练习，您需要有权访问启用了AEM Assets Dynamic Media的有效AEM Assets CS创作环境。
>
>如果没有此类环境，请转到[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照上面的说明进行操作，您将有权访问此类环境。

>[!IMPORTANT]
>
>如果您之前已使用AEM CS环境配置了AEM Assets CS项目，则可能是您的AEM CS沙盒已休眠。 鉴于解除此类沙盒的休眠需要10-15分钟，最好现在就启动解除休眠过程，这样以后就不必等待它。

## 1.3.1.1 -

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 您应选择的组织是`--aepImsOrgName--`。 打开您的环境。

![AEM 表单](./images/aemforms1.png)

转到&#x200B;**Forms**。

![AEM 表单](./images/aemforms2.png)

转到&#x200B;**Forms和文档**。

![AEM 表单](./images/aemforms3.png)

单击&#x200B;**创建**，然后选择&#x200B;**自适应表单**。

![AEM 表单](./images/aemforms4.png)

选择&#x200B;**Edge Delivery Services**，然后选择&#x200B;**空白页面**。 单击&#x200B;**创建**。

![AEM 表单](./images/aemforms5.png)

您应该会看到此内容。 填写以下字段：

- **标题**： `Fiber Max Interest Form`
- **名称**：应基于字段&#x200B;**标题**&#x200B;自动填充。
- **Github URL**：提供链接到您网站的Github存储库的路径

单击&#x200B;**创建**。

![AEM 表单](./images/aemforms6.png)

单击&#x200B;**创建**&#x200B;后，**Universal Editor**&#x200B;应会自动打开，您应该会看到类似这样的内容。 单击图标以打开&#x200B;**内容树**。

![AEM 表单](./images/aemforms7.png)

在&#x200B;**内容树**&#x200B;中选择对象&#x200B;**自适应表单**。

![AEM 表单](./images/aemforms8.png)

然后，单击&#x200B;**+**&#x200B;图标以添加新元素，并选择&#x200B;**文本输入**。

![AEM 表单](./images/aemforms9.png)

在&#x200B;**内容树**&#x200B;中，选择字段&#x200B;**文本输入**。

![AEM 表单](./images/aemforms10.png)

转到&#x200B;**基本**&#x200B;视图。 你应该看看这个。

填写以下字段：

- **名称**： `first-name`
- **标题**： `First Name`

然后，转到&#x200B;**验证**。

![AEM 表单](./images/aemforms11.png)

翻转开关以使其成为必填字段。 填写以下字段：

- **错误消息**： `Enter your first name`
- **模式**： `[A-Za-z][A-Za-z ]+`
- **模式错误消息**： `Letters only!`

![AEM 表单](./images/aemforms12.png)

在&#x200B;**内容树**&#x200B;中，选择字段&#x200B;**自适应表单**。 单击&#x200B;**+**&#x200B;图标，然后选择&#x200B;**文本输入**。

![AEM 表单](./images/aemforms13.png)

在&#x200B;**内容树**&#x200B;中，选择新创建的字段&#x200B;**文本输入**。 转到&#x200B;**属性**。

![AEM 表单](./images/aemforms14.png)

转到&#x200B;**基本**&#x200B;视图。 你应该看看这个。

填写以下字段：

- **名称**： `last-name`
- **标题**： `Last Name`

然后，转到&#x200B;**验证**。

![AEM 表单](./images/aemforms15.png)

翻转开关以使其成为必填字段。 填写以下字段：

- **错误消息**： `Enter your last name`
- **模式**： `[A-Za-z][A-Za-z ]+`
- **模式错误消息**： `Letters only!`

![AEM 表单](./images/aemforms16.png)

在&#x200B;**内容树**&#x200B;中，选择字段&#x200B;**自适应表单**。 单击&#x200B;**+**&#x200B;图标，然后选择&#x200B;**文本输入**。

![AEM 表单](./images/aemforms17.png)

在&#x200B;**内容树**&#x200B;中，选择新创建的字段&#x200B;**文本输入**。 转到&#x200B;**属性**。

![AEM 表单](./images/aemforms18.png)

转到&#x200B;**基本**&#x200B;视图。 你应该看看这个。

填写以下字段：

- **名称**： `email`
- **标题**： `Email`

然后，转到&#x200B;**验证**。

![AEM 表单](./images/aemforms19.png)

翻转开关以使其成为必填字段。 填写以下字段：

- **错误消息**： `Enter your email address`
- **模式**： `^[^@]+@[^@]+\.[^@]+$`
- **模式错误消息**： `Please verify your email address!`

![AEM 表单](./images/aemforms20.png)

在&#x200B;**内容树**&#x200B;中，选择字段&#x200B;**自适应表单**。 单击&#x200B;**+**&#x200B;图标，然后选择&#x200B;**文本输入**。

![AEM 表单](./images/aemforms21.png)

在&#x200B;**内容树**&#x200B;中，选择新创建的字段&#x200B;**文本输入**。

![AEM 表单](./images/aemforms22.png)

转到&#x200B;**基本**&#x200B;视图。 你应该看看这个。

填写以下字段：

- **名称**： `city`
- **标题**： `city`

然后，转到&#x200B;**验证**。

![AEM 表单](./images/aemforms23.png)

翻转开关以使其成为必填字段。 填写以下字段：

- **错误消息**： `Enter your city`
- **模式**： `[A-Za-z][A-Za-z ]+`
- **模式错误消息**： `Letters only!`

![AEM 表单](./images/aemforms24.png)

单击&#x200B;**发布**。

![AEM 表单](./images/aemforms25.png)

再次单击&#x200B;**发布**。

![AEM 表单](./images/aemforms26.png)

单击以打开您的表单。

![AEM 表单](./images/aemforms27.png)

然后，您可以填写表单，但您尚无法提交表单。

![AEM 表单](./images/aemforms28.png)

## 后续步骤

下一步： [-](./ex1.md){target="_blank"}

返回至[Adobe Experience Manager Forms和Edge Delivery Services](./aemforms.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
