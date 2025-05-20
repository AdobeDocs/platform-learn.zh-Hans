---
title: 使用Microsoft Azure和预签名URL优化您的Firefly进程
description: 了解如何使用Microsoft Azure和预签名URL优化Firefly过程
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: e7f83f362e5c9b2dff93d43a7819f6c23186b456
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 0%

---

# 1.1.2使用Microsoft Azure和预签名URL优化您的Firefly进程

了解如何使用Microsoft Azure和预签名URL优化Firefly过程。

## 1.1.2.1什么是预签名URL？

预签名URL是一种授予您临时访问存储位置中特定对象权限的URL。 例如，使用URL，用户可以读取对象或写入对象（或更新现有对象）。 URL包含由应用程序设置的特定参数。

在创建内容供应链自动化的上下文中，通常需要针对特定用例执行多个文件操作。 例如，可能需要更改文件的背景，可能需要更改各种图层的文本等。 并非总是可以同时执行所有文件操作，这就需要多步方法。 在每个中间步骤之后，输出是执行下一个步骤所需的临时文件。 执行下一步后，临时文件会快速丢失值，通常不再需要它，因此应将其删除。

Adobe Firefly Services当前支持以下域：

- Amazon AWS： *.amazonaws.com
- Microsoft Azure： *.windows.net
- Dropbox： *.dropboxusercontent.com

之所以经常使用云存储解决方案，是因为正在创建的中间资产会迅速失去价值。 通过预签名URL解决的问题通常最好通过商品存储解决方案（通常是上述云服务之一）来解决。

在Adobe生态系统中，还有存储解决方案，如Frame.io、Workfront Fusion和Adobe Experience Manager资源。 这些解决方案还支持预签名的URL，因此往往需要在实施期间做出选择。 然后，选择通常基于现有应用程序和存储成本的组合。

因此，预签名URL将与Adobe Firefly Services操作结合使用，因为：

- 企业通常需要在中间步骤中处理对同一映像的多项更改，并且需要中间存储才能做到这一点。
- 从云存储位置进行读写的访问应该是安全的，并且在服务器端环境中，无法手动登录，因此需要将安全性直接写入URL。

预签名URL使用三个参数来限制用户的访问：

- 存储位置：这可以是AWS S3存储段位置、带有容器的Microsoft Azure存储帐户位置
- 文件名：需要读取、更新、删除的特定文件。
- 查询字符串参数：查询字符串参数始终以问号开头，后跟一系列复杂的参数

示例：

- **Amazon AWS**： `https://bucket.s3.eu-west-2.amazonaws.com/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AXXXXXXXXXX%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250510T171315Z&X-Amz-Expires=1800&X-Amz-Signature=XXXXXXXXX&X-Amz-SignedHeaders=host`
- **Microsoft Azure**： `https://storageaccount.blob.core.windows.net/container/image.png?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=XXXXXX%3D`

## 1.1.2.2创建Azure订阅

>[!NOTE]
>
>如果您已有现有的Azure订阅，则可以跳过此步骤。 请继续该案例中的下一个练习。

>[!NOTE]
>
>如果您作为现场指导研讨会或指导式按需培训的一部分学习本教程，则可能已有权访问Microsoft Azure Storage帐户。 在这种情况下，您无需创建自己的帐户 — 请使用已在培训中提供给您的帐户。

转到[https://portal.azure.com](https://portal.azure.com){target="_blank"}并使用您的Azure帐户登录。 如果您没有个人电子邮件地址，请使用个人电子邮件地址创建您的Azure帐户。

![Azure存储](./images/02azureportalemail.png){zoomable="yes"}

成功登录后，您应该会看到以下屏幕：

![Azure存储](./images/03azureloggedin.png){zoomable="yes"}

在左侧菜单上选择&#x200B;**所有资源**，如果您尚未订阅，则会显示Azure订阅屏幕。

如果未订阅，请选择&#x200B;**开始使用Azure免费试用**。

![Azure存储](./images/04azurestartsubscribe.png){zoomable="yes"}

填写Azure订阅表，并提供用于激活的移动电话和信用卡（您将拥有30天的免费套餐，除非您升级，否则不会向您收费）。

订阅过程完成后，您就可以开始了。

![Azure存储](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.3创建Azure存储帐户

搜索`storage account`，然后选择&#x200B;**存储帐户**。

![Azure存储](./images/azs1.png){zoomable="yes"}

选择&#x200B;**+创建**。

![Azure存储](./images/azs2.png){zoomable="yes"}

选择您的&#x200B;**订阅**&#x200B;并选择（或创建）**资源组**。

在&#x200B;**存储帐户名称**&#x200B;下，使用`--aepUserLdap--`。

选择&#x200B;**审阅+创建**。

![Azure存储](./images/azs3.png){zoomable="yes"}

选择&#x200B;**创建**。

![Azure存储](./images/azs4.png){zoomable="yes"}

确认后，选择&#x200B;**转到资源**。

![Azure存储](./images/azs5.png){zoomable="yes"}

您的Azure存储帐户现已准备就绪，可供使用。

![Azure存储](./images/azs6.png){zoomable="yes"}

选择&#x200B;**数据存储**，然后转到&#x200B;**容器**。 选择&#x200B;**+容器**。

![Azure存储](./images/azs7.png){zoomable="yes"}

使用`--aepUserLdap--`作为名称，并选择&#x200B;**创建**。

![Azure存储](./images/azs8.png){zoomable="yes"}

您的容器现已准备就绪，可供使用。

![Azure存储](./images/azs9.png){zoomable="yes"}

## 1.1.2.4安装Azure存储资源管理器

[下载Microsoft Azure Storage Explorer以管理您的文件](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}。 为您的特定操作系统选择正确的版本，然后下载并安装该版本。

![Azure存储](./images/az10.png){zoomable="yes"}

打开应用程序并选择&#x200B;**使用Azure登录**。

![Azure存储](./images/az11.png){zoomable="yes"}

选择&#x200B;**订阅**。

![Azure存储](./images/az12.png){zoomable="yes"}

选择&#x200B;**Azure**，然后选择&#x200B;**下一步**。

![Azure存储](./images/az13.png){zoomable="yes"}

选择您的Microsoft Azure帐户并完成身份验证过程。

![Azure存储](./images/az14.png){zoomable="yes"}

验证后，将显示此消息。

![Azure存储](./images/az15.png){zoomable="yes"}

返回Microsoft Azure Storage Explorer应用，选择您的订阅，然后选择&#x200B;**打开资源管理器**。

>[!NOTE]
>
>如果未显示您的帐户，请单击电子邮件地址旁边的&#x200B;**齿轮**&#x200B;图标，然后选择&#x200B;**取消筛选**。

![Azure存储](./images/az16.png){zoomable="yes"}

你的存储帐户出现在&#x200B;**存储帐户**&#x200B;下。

![Azure存储](./images/az17.png){zoomable="yes"}

打开&#x200B;**Blob容器**，然后选择在上一个练习中创建的容器。

![Azure存储](./images/az18.png){zoomable="yes"}

## 1.1.2.5手动文件上传并使用图像文件作为样式引用

将您选择的图像文件或[此文件](./images/gradient.jpg){target="_blank"}上载到容器。

![Azure存储](./images/gradient.jpg)

上传后，您可以在容器中看到该包：

![Azure存储](./images/az19.png){zoomable="yes"}

右键单击`gradient.jpg`，然后选择&#x200B;**获取共享访问签名**。

![Azure存储](./images/az20.png){zoomable="yes"}

在&#x200B;**权限**&#x200B;下，只需要&#x200B;**读取**。 选择&#x200B;**创建**。

![Azure存储](./images/az21.png){zoomable="yes"}

将此图像文件的预签名URL复制到下一个API请求到Firefly。

![Azure存储](./images/az22.png){zoomable="yes"}

返回Postman打开请求&#x200B;**POST - Firefly - T2I (styleref) V3**。
这出现在&#x200B;**正文**&#x200B;中。

![Azure存储](./images/az23.png){zoomable="yes"}

将占位符URL替换为图像文件的预签名URL，然后选择&#x200B;**发送**。

![Azure存储](./images/az24.png){zoomable="yes"}

在浏览器中打开响应Firefly Services新图像。

![Azure存储](./images/az25.png){zoomable="yes"}

另一个图像以`horses in a field`显示，但这次的样式与作为样式引用提供的图像文件类似。

![Azure存储](./images/az26.png){zoomable="yes"}

## 1.1.2.6编程文件上传

若要通过Azure存储帐户使用编程文件上传，您需要创建一个新的&#x200B;**共享访问签名(SAS)**&#x200B;令牌，该令牌具有允许您写入文件的权限。

在Azure Storage Explorer中，右键单击您的容器，然后选择&#x200B;**获取共享访问签名**。

![Azure存储](./images/az27.png){zoomable="yes"}

在&#x200B;**权限**&#x200B;下，选择以下所需权限：

- **读取**
- **添加**
- **创建**
- **写入**
- **列表**

选择&#x200B;**创建**。

![Azure存储](./images/az28.png){zoomable="yes"}

收到&#x200B;**共享访问签名**&#x200B;后，选择&#x200B;**复制**&#x200B;以复制URL。

![Azure存储](./images/az29.png){zoomable="yes"}

使用&#x200B;**SAS-token**&#x200B;将文件上传到您的Azure存储帐户。

返回Postman，选择文件夹&#x200B;**FF - Firefly Services Tech Insiders**，然后在&#x200B;**Firefly**&#x200B;文件夹中选择&#x200B;**...**，然后选择&#x200B;**添加请求**。

![Azure存储](./images/az30.png){zoomable="yes"}

将空请求的名称更改为&#x200B;**将文件上载到Azure Storage Account**，将&#x200B;**请求类型**&#x200B;更改为&#x200B;**PUT**，并在URL部分中粘贴SAS令牌URL，然后选择&#x200B;**正文**。

![Azure存储](./images/az31.png){zoomable="yes"}

接下来，从本地计算机中选择文件，或使用位于[此处](./images/gradient2-p.jpg){target="_blank"}的其他图像文件。

![渐变文件](./images/gradient2-p.jpg)

在&#x200B;**主体**&#x200B;中，选择&#x200B;**二进制文件**，然后&#x200B;**选择文件**，然后从本地计算机&#x200B;**中选择**+新建文件。

![Azure存储](./images/az32.png){zoomable="yes"}

选择您选择的文件，然后选择&#x200B;**打开**。

![Azure存储](./images/az33.png){zoomable="yes"}

接下来，将光标放在问号&#x200B;**前面，指定要在Azure存储帐户中使用的文件名？URL中的**，如下所示：

![Azure存储](./images/az34.png){zoomable="yes"}

URL当前看起来像这样，但需要更改。

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

将文件名更改为`gradient2-p.jpg`，并将URL更改为包括文件名，如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Azure存储](./images/az34a.png){zoomable="yes"}

接下来，转到&#x200B;**标头**&#x200B;以手动添加新标头，如下所示：

| 键 | 值 |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Azure存储](./images/az35.png){zoomable="yes"}

转到&#x200B;**授权**&#x200B;并将&#x200B;**身份验证类型**&#x200B;设置为&#x200B;**无身份验证**，然后选择&#x200B;**发送**。

![Azure存储](./images/az36.png){zoomable="yes"}

接下来，Postman中会显示此空响应，这意味着您的文件上传可以正常进行。

![Azure存储](./images/az37.png){zoomable="yes"}

返回到Azure存储资源管理器中刷新文件夹的内容，新上传的文件随即显示。

![Azure存储](./images/az38.png){zoomable="yes"}

## 1.1.2.7编程文件使用

若要以编程方式长期读取Azure存储帐户中的文件，您需要创建一个新的&#x200B;**共享访问签名(SAS)**&#x200B;令牌，该令牌具有允许您读取文件的权限。 从技术上讲，您可以使用在上一个练习中创建的SAS令牌，但最佳实践是让单独的令牌仅具有&#x200B;**读取**&#x200B;权限，而单独的令牌仅具有&#x200B;**写入**&#x200B;权限。

### 长期读取SAS令牌

返回到Azure存储资源管理器，右键单击您的容器，然后选择&#x200B;**获取共享访问签名**。

![Azure存储](./images/az27.png){zoomable="yes"}

在&#x200B;**权限**&#x200B;下，选择以下所需权限：

- **读取**
- **列表**

将&#x200B;**过期时间**&#x200B;设置为从现在起的1年。

选择&#x200B;**创建**。

![Azure存储](./images/az100.png){zoomable="yes"}

复制URL并将其写到计算机上的文件中，以获得具有读取权限的长期SAS令牌。

![Azure存储](./images/az101.png){zoomable="yes"}

您的URL应如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

您可以从上述URL派生出几个值：

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### 长期写入SAS令牌

返回到Azure存储资源管理器，右键单击您的容器并选择&#x200B;**获取共享访问签名**。

![Azure存储](./images/az27.png){zoomable="yes"}

在&#x200B;**权限**&#x200B;下，选择以下所需权限：

- **读取**
- **列表**
- **添加**
- **创建**
- **写入**

将&#x200B;**过期时间**&#x200B;设置为从现在起的1年。

选择&#x200B;**创建**。

![Azure存储](./images/az102.png){zoomable="yes"}

复制URL并将其写到计算机上的文件中，以获得具有读取权限的长期SAS令牌。

![Azure存储](./images/az103.png){zoomable="yes"}

您的URL应如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

您可以从上述URL派生出几个值：

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Postman中的变量

如上节所示，读取和写入令牌中都有一些常见的变量。

接下来，您需要在Postman中创建用于存储上述SAS令牌的各种元素的变量。 这两个URL中的一些值是相同的：

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

对于将来的API交互，主要的变化是资源名称，而上述变量保持不变。 在这种情况下，最好在Postman中创建变量，这样您就无需每次都手动指定它们。

在Postman中，选择&#x200B;**环境**，打开&#x200B;**所有变量**，然后选择&#x200B;**环境**。

![Azure存储](./images/az104.png){zoomable="yes"}

在显示的表中创建这4个变量，对于&#x200B;**初始值**&#x200B;和&#x200B;**当前值**&#x200B;列，请输入特定的个人值。

- `AZURE_STORAGE_URL`：您的url
- `AZURE_STORAGE_CONTAINER`：您的容器名称
- `AZURE_STORAGE_SAS_READ`：您的SAS读取令牌
- `AZURE_STORAGE_SAS_WRITE`：您的SAS写入令牌

选择&#x200B;**保存**。

![Azure存储](./images/az105.png){zoomable="yes"}

### PostBuster中的变量

如上节所示，读取和写入令牌中都有一些常见的变量。

接下来，您需要在PostBuster中创建用于存储上述SAS令牌的各种元素的变量。 这两个URL中的一些值是相同的：

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

打开PostBuster。 选择&#x200B;**基本环境**，然后单击&#x200B;**编辑**&#x200B;图标以打开基本环境。

![Azure存储](./images/pbbe1.png)

然后，您将看到4个空变量。 在此处输入您的Azure存储帐户详细信息。

![Azure存储](./images/pbbe2.png)

您的基本环境文件现在应如下所示。 单击&#x200B;**关闭**。

![Azure存储](./images/pbbe3.png)

### 测试您的配置

在前面的练习中，请求&#x200B;**Firefly - T2I (styleref) V3**&#x200B;的&#x200B;**Body**&#x200B;如下所示：

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Azure存储](./images/az24.png){zoomable="yes"}

将URL更改为：

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

选择&#x200B;**发送**&#x200B;以测试您所做的更改。

![Azure存储](./images/az106.png){zoomable="yes"}

如果变量配置正确，则会返回图像URL。

![Azure存储](./images/az107.png){zoomable="yes"}

打开图像URL以验证您的图像。

![Azure存储](./images/az108.jpg)

## 后续步骤

转到[使用Photoshop API](./ex3.md){target="_blank"}

返回[Adobe Firefly Services概述](./firefly-services.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}