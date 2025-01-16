---
title: 使用Microsoft Azure和预签名URL优化您的Firefly过程
description: 使用Microsoft Azure和预签名URL优化您的Firefly过程
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: a4933bd49988cd16c4382ad4327d01ae58b52bbb
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 1%

---

# 1.1.2使用Microsoft Azure和预签名URL优化您的Firefly过程

## 1.1.2.1创建Azure订阅

>[!NOTE]
>
>如果您已有现有的Azure订阅，则可以跳过此步骤。 请继续该案例中的下一个练习。

转到[https://portal.azure.com](https://portal.azure.com)并使用您的Azure帐户登录。 如果您没有个人电子邮件地址，请使用个人电子邮件地址创建您的Azure帐户。

![Azure存储](./images/02azureportalemail.png)

成功登录后，您将看到以下屏幕：

![Azure存储](./images/03azureloggedin.png)

单击左侧的菜单并选择&#x200B;**所有资源**，如果您尚未订阅，将显示Azure订阅屏幕。 在这种情况下，请选择&#x200B;**开始使用Azure免费试用**。

![Azure存储](./images/04azurestartsubscribe.png)

填写Azure订阅表单，提供用于激活的移动电话和信用卡（您将拥有30天的免费套餐，除非您升级，否则不会向您收费）。

订阅过程完成后，您可以：

![Azure存储](./images/06azuresubscriptionok.png)

## 1.1.2.2创建Azure存储帐户

搜索`storage account`，然后单击&#x200B;**存储帐户**。

![Azure存储](./images/azs1.png)

单击&#x200B;**+创建**。

![Azure存储](./images/azs2.png)

填写以下详细信息：

- 选择您的&#x200B;**订阅**
- 选择（或创建）**资源组**
- **存储帐户名称**：使用`--aepUserLdap--`

单击&#x200B;**审阅+创建**。

![Azure存储](./images/azs3.png)

单击&#x200B;**创建**。

![Azure存储](./images/azs4.png)

然后您会获得类似的确认。 单击&#x200B;**转到资源**。

![Azure存储](./images/azs5.png)

您的Azure存储帐户现已准备就绪，可供使用。

![Azure存储](./images/azs6.png)

单击&#x200B;**数据存储**，然后转到&#x200B;**容器**。 单击&#x200B;**+容器**。

![Azure存储](./images/azs7.png)

对于名称，请使用`--aepUserLdap--`。 单击&#x200B;**创建**。

![Azure存储](./images/azs8.png)

您的容器现已准备就绪，可供使用。

![Azure存储](./images/azs9.png)

## 1.1.2.3安装Azure存储资源管理器

您将使用Microsoft Azure Storage Explorer来管理文件。 您可以通过[此链接](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4)下载它。 为您的特定操作系统选择正确的版本，下载并安装它。

![Azure存储](./images/az10.png)

安装应用程序后，将其打开。 您会看到类似以下的内容。 单击&#x200B;**使用Azure**&#x200B;登录。

![Azure存储](./images/az11.png)

单击&#x200B;**订阅**。

![Azure存储](./images/az12.png)

选择&#x200B;**Azure**&#x200B;并单击&#x200B;**下一步**。

![Azure存储](./images/az13.png)

选择您的Microsoft Azure帐户并完成身份验证过程。

![Azure存储](./images/az14.png)

身份验证后，您将看到如下消息。

![Azure存储](./images/az15.png)

切换回Microsoft Azure Storage Explorer应用程序。 选择您的订阅，然后单击&#x200B;**打开资源管理器**。

![Azure存储](./images/az16.png)

你将在&#x200B;**存储帐户**&#x200B;下找到你的存储帐户。

![Azure存储](./images/az17.png)

打开&#x200B;**Blob容器**，然后单击在上一个练习中创建的容器。

![Azure存储](./images/az18.png)

## 1.1.2.4手动文件上传和使用图像文件作为样式参考

现在，您应该将选择的图像文件上传到容器中。 您可以使用所选的任何图像文件，也可以通过计算机下载[此文件](./images/gradient.jpg)来使用。

![Azure存储](./images/gradient.jpg)

将图像文件放入Azure存储资源管理器中的容器。

上传后，您将在容器中看到该包：

![Azure存储](./images/az19.png)

右键单击文件`gradient.jpg`，然后单击&#x200B;**获取共享访问签名**。

![Azure存储](./images/az20.png)

在&#x200B;**权限**&#x200B;下，只需要&#x200B;**读取**。 单击&#x200B;**创建**。

![Azure存储](./images/az21.png)

然后，您将看到此图像文件的预签名URL。 根据需要复制它，以便下一个API请求Firefly。

![Azure存储](./images/az22.png)

返回Postman。 打开POST **请求 — T2I (styleref) V3** Firefly。 您将在&#x200B;**正文**&#x200B;中看到此内容。

![Azure存储](./images/az23.png)

将占位符URL替换为您从Azure存储资源管理器复制的图像文件的预签名URL。 你就能拥有这个了。 单击&#x200B;**发送**。

![Azure存储](./images/az24.png)

然后，您将再次从Firefly服务中收到包含新图像的响应。 在浏览器中打开图像文件。

![Azure存储](./images/az25.png)

您随后将看到另一个包含`horses in a field`的图像，但这次的样式将与您作为样式引用提供的图像文件类似。

![Azure存储](./images/az26.png)

## 1.1.2.5编程文件上传

若要使用Azure存储帐户的程序化文件上传，您需要创建一个新的&#x200B;**共享访问签名(SAS)**&#x200B;令牌，该令牌具有允许您写入文件的权限。

为此，请返回Azure存储资源管理器。 右键单击容器，然后单击&#x200B;**获取共享访问签名**。

![Azure存储](./images/az27.png)

在&#x200B;**权限**&#x200B;下，需要以下权限：

- **读取**
- **添加**
- **创建**
- **写入**
- **列表**

单击&#x200B;**创建**。

![Azure存储](./images/az28.png)

然后，您将获得您的&#x200B;**SAS令牌**。 单击&#x200B;**复制**。

![Azure存储](./images/az29.png)

您现在可以使用此&#x200B;**SAS-token**&#x200B;将文件上传到您的Azure存储帐户。 返回Postman以执行此操作。

单击以选择文件夹&#x200B;**FF -Firefly服务技术内部人士**，然后单击文件夹&#x200B;**请求**&#x200B;上的3个点&#x200B;**...**，然后单击&#x200B;**添加Firefly**。

![Azure存储](./images/az30.png)

然后，您将有一个空请求。 将请求的名称更改为&#x200B;**将文件上载到Azure Storage Account**，将&#x200B;**请求类型**&#x200B;更改为&#x200B;**PUT**，并在URL部分中粘贴SAS令牌URL。

然后，单击&#x200B;**正文**。

![Azure存储](./images/az31.png)

现在，您需要从本地计算机中选择一个文件。 您可以使用选择的新图像文件，也可以使用可在[此处](./images/gradient2-p.jpg)找到的其他图像文件。

![渐变文件](./images/gradient2-p.jpg)

在&#x200B;**主体**&#x200B;中，选择&#x200B;**二进制文件**，然后单击&#x200B;**选择文件**，然后单击&#x200B;**+本地计算机的新文件**。

![Azure存储](./images/az32.png)

选择您选择的文件，然后单击&#x200B;**打开**。

![Azure存储](./images/az33.png)

你会看到这个。 接下来要做的就是指定将在您的Azure存储帐户中使用的文件名。 要执行此操作，您需要将游标放在问号&#x200B;**之前？URL中的**。 您当前可以在那里看到以下内容：

![Azure存储](./images/az34.png)

当前URL看起来与此类似，但需要更改。

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

要使用的文件名为`gradient2-p.jpg`，这意味着需要更改URL以包含文件名，如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Azure存储](./images/az34a.png)

接下来，转到&#x200B;**标头**，您需要在该处手动添加新标头。 使用此：

| 键 | 值 |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Azure存储](./images/az35.png)

转到&#x200B;**授权**&#x200B;并将&#x200B;**身份验证类型**&#x200B;设置为&#x200B;**无身份验证**。 单击&#x200B;**发送**。

![Azure存储](./images/az36.png)

然后，您将在Postman中看到此空响应，这意味着您的文件上传运行正常。

![Azure存储](./images/az37.png)

如果您随后返回Azure存储资源管理器并刷新文件夹的内容，您现在将在该文件夹中找到新上传的文件。

![Azure存储](./images/az38.png)

## 1.1.2.6编程文件使用

为了长期以编程方式从Azure存储帐户中读取文件，您需要创建一个新的&#x200B;**共享访问签名(SAS)**&#x200B;令牌，该令牌具有允许您读取文件的权限。 从技术上讲，您可以使用在上一个练习中创建的SAS令牌，但最佳实践是让单独的令牌仅具有&#x200B;**读取**&#x200B;权限，而单独的令牌仅具有&#x200B;**写入**&#x200B;权限。

### 长期读取SAS令牌

为此，请返回Azure存储资源管理器。 右键单击容器，然后单击&#x200B;**获取共享访问签名**。

![Azure存储](./images/az27.png)

在&#x200B;**权限**&#x200B;下，需要以下权限：

- **读取**
- **列表**

将&#x200B;**过期时间**&#x200B;设置为从现在起的1年。

单击&#x200B;**创建**。

![Azure存储](./images/az100.png)

然后，您将获得具有读取权限的长期SAS令牌。 复制URL并将其写入计算机上的文件中。

![Azure存储](./images/az101.png)

您的URL将如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

您可以从上述URL派生出几个值：

- `AZURE_STORAGE_URL`： `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`： `vangeluw`
- `AZURE_STORAGE_SAS_READ`： `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### 长期写入SAS令牌

为此，请返回Azure存储资源管理器。 右键单击容器，然后单击&#x200B;**获取共享访问签名**。

![Azure存储](./images/az27.png)

在&#x200B;**权限**&#x200B;下，需要以下权限：

- **添加**
- **创建**
- **写入**

将&#x200B;**过期时间**&#x200B;设置为从现在起的1年。

单击&#x200B;**创建**。

![Azure存储](./images/az102.png)

然后，您将获得具有读取权限的长期SAS令牌。 复制URL并将其写入计算机上的文件中。

![Azure存储](./images/az103.png)

您的URL将如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

您可以再次从上述URL中派生出几个值：

- `AZURE_STORAGE_URL`： `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`： `vangeluw`
- `AZURE_STORAGE_SAS_READ`： `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`： `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Postman中的变量

如上节所示，读取和写入令牌中都有一些常见的变量。

您现在需要在Postman中创建用于存储上述SAS令牌的各种元素的变量。
这两个URL中的一些值是相同的：

- `AZURE_STORAGE_URL`： `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`： `vangeluw`
- `AZURE_STORAGE_SAS_READ`： `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`： `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

对于将来进行的API交互，主要的变化是资源名称，而上述变量将保持不变。 在这种情况下，最好在Postman中创建变量，这样您就无需每次都手动指定它们。

为此，请打开Postman。 单击&#x200B;**环境**&#x200B;图标，打开&#x200B;**所有变量**&#x200B;菜单，然后单击&#x200B;**环境**。

![Azure存储](./images/az104.png)

然后您会看到此内容。 在显示的表中创建这4个变量，对于&#x200B;**初始值**&#x200B;和&#x200B;**当前值**&#x200B;列，请输入特定的个人值。

- `AZURE_STORAGE_URL`：您的url
- `AZURE_STORAGE_CONTAINER`：您的容器名称
- `AZURE_STORAGE_SAS_READ`：您的SAS读取令牌
- `AZURE_STORAGE_SAS_WRITE`：您的SAS写入令牌

单击&#x200B;**保存**。

![Azure存储](./images/az105.png)

在前面的练习中，请求&#x200B;**Firefly- T2I (styleref) V3**&#x200B;的&#x200B;**Body**&#x200B;如下所示：

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Azure存储](./images/az24.png)

您现在可以将URL更改为：

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

单击&#x200B;**发送**&#x200B;以测试您所做的更改。

![Azure存储](./images/az106.png)

如果变量配置正确，您将看到返回的图像URL。

![Azure存储](./images/az107.png)

打开图像URL以验证您的图像。

![Azure存储](./images/az108.jpg)

下一步：[1.1.3Adobe Firefly和Adobe Photoshop](./ex3.md)

[返回模块1.1](./firefly-services.md)

[返回所有模块](./../../../overview.md)
