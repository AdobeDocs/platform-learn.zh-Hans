---
title: 在Workfront Fusion中使用Adobe API
description: 了解如何在Workfront Fusion中使用Adobe API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 1.2.2在Workfront Fusion中使用Adobe API

了解如何在Workfront Fusion中使用Adobe API。

## 1.2.2.1使用Firefly文本通过Workfront Fusion对API进行成像

将鼠标悬停在第二个&#x200B;**设置多个变量**&#x200B;节点上，并选择&#x200B;**+**&#x200B;以添加另一个模块。

![WF Fusion](./images/wffusion48.png)

搜索&#x200B;**http**&#x200B;并选择&#x200B;**HTTP**。

![WF Fusion](./images/wffusion49.png)

选择&#x200B;**发出请求**。

![WF Fusion](./images/wffusion50.png)

选择以下变量：

- **URL**： `https://firefly-api.adobe.io/v3/images/generate`
- **方法**： `POST`

选择&#x200B;**添加标头**。

![WF Fusion](./images/wffusion51.png)

输入以下标题：

| 键 | 值 |
|:-------------:| :---------------:| 
| `x-api-key` | 您为`CONST_client_id`存储的变量 |
| `Authorization` | `Bearer ` +您为`bearer_token`存储的变量 |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

输入`x-api-key`的详细信息。 选择&#x200B;**添加**。

![WF Fusion](./images/wffusion52.png)

选择&#x200B;**添加标头**。

![WF Fusion](./images/wffusion53.png)

输入`Authorization`的详细信息。 选择&#x200B;**添加**。

![WF Fusion](./images/wffusion54.png)

选择&#x200B;**添加标头**。 输入`Content-Type`的详细信息。 选择&#x200B;**添加**。

![WF Fusion](./images/wffusion541.png)

选择&#x200B;**添加标头**。 输入`Accept`的详细信息。 选择&#x200B;**添加**。

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

选中&#x200B;**分析响应**&#x200B;的框。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion56.png)

选择&#x200B;**运行一次**。

![WF Fusion](./images/wffusion57.png)

您的屏幕应如下所示。

![WF Fusion](./images/wffusion58.png)

选择&#x200B;**？第四个节点HTTP上的**&#x200B;图标以查看响应。 您应该会在响应中看到图像文件。

![WF Fusion](./images/wffusion59.png)

复制图像URL并在浏览器窗口中将其打开。 屏幕应如下所示：

![WF Fusion](./images/wffusion60.png)

右键单击&#x200B;**HTTP**&#x200B;并将它重命名为&#x200B;**Firefly T2I**。

![WF Fusion](./images/wffusion62.png)

选择&#x200B;**保存**&#x200B;以保存更改。

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2将Photoshop API与Workfront Fusion一起使用

在节点&#x200B;**设置持有者令牌**&#x200B;和&#x200B;**Firefly T2I**&#x200B;之间选择&#x200B;**扳手**。 选择&#x200B;**添加路由器**。

![WF Fusion](./images/wffusion63.png)

右键单击&#x200B;**FireflyT2I**&#x200B;对象并选择&#x200B;**克隆**。

![WF Fusion](./images/wffusion64.png)

将克隆的对象拖放到&#x200B;**路由器**&#x200B;对象附近，该对象会自动连接到&#x200B;**路由器**。 屏幕应如下所示：

![WF Fusion](./images/wffusion65.png)

您现在拥有基于&#x200B;**Firefly T2I** HTTP请求的相同副本。 **Firefly T2I** HTTP请求的某些设置类似于与&#x200B;**Photoshop API**&#x200B;交互所需的设置，后者是一个省时工具。 现在，您只需更改不相同的变量即可，例如请求URL和有效负载。

将&#x200B;**URL**&#x200B;更改为`https://image.adobe.io/pie/psdService/text`。

![WF Fusion](./images/wffusion66.png)

使用以下有效负载替换&#x200B;**请求内容**：

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
          "name": "2048x2048-button-text",
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
        "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
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

返回第一个节点，选择&#x200B;**初始化常量**，然后为每个变量选择&#x200B;**添加项**。

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

您的屏幕应如下所示。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion68.png)

接下来，返回克隆的HTTP请求以更新&#x200B;**请求内容**。 请注意&#x200B;**请求内容**&#x200B;中的黑色变量，它们是从Postman复制的变量。 您需要更改为您刚刚在Workfront Fusion中定义的变量。 通过删除黑色文本并用正确的变量替换它，逐一替换每个变量。

![WF Fusion](./images/wffusion70.png)

在&#x200B;**输入**&#x200B;部分中进行这3项更改。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion71.png)

在&#x200B;**输出**&#x200B;节中进行这3项更改。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion72.png)

右键单击克隆的节点，然后选择&#x200B;**重命名**。 将名称更改为&#x200B;**Photoshop更改文本**。

![WF Fusion](./images/wffusion73.png)

屏幕应如下所示：

![WF Fusion](./images/wffusion74.png)

选择&#x200B;**运行一次**。

![WF Fusion](./images/wffusion75.png)

选择&#x200B;**Photoshop更改文本**&#x200B;节点上的&#x200B;**搜索**&#x200B;图标以查看响应。 您应该具有类似于这样的响应，其中包含指向状态文件的链接。

![WF Fusion](./images/wffusion76.png)

在继续Photoshop API交互之前，请禁用到&#x200B;**Firefly T2I**&#x200B;节点的路由，以免向该API端点发送不需要的API调用。 选择&#x200B;**扳手**&#x200B;图标，然后选择&#x200B;**禁用路由**。

![WF Fusion](./images/wffusion77.png)

屏幕应如下所示：

![WF Fusion](./images/wffusion78.png)

接下来，添加另一个&#x200B;**设置多个变量**&#x200B;节点。

![WF Fusion](./images/wffusion79.png)

将其放置在&#x200B;**Photoshop更改文本**&#x200B;节点之后。

![WF Fusion](./images/wffusion80.png)

选择&#x200B;**设置多个变量**&#x200B;节点，选择&#x200B;**添加项**。 从上一个请求的响应中选择变量值。

| 变量名称 | 变量值 |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

选择&#x200B;**添加**。

![WF Fusion](./images/wffusion81.png)

选择&#x200B;**确定**。

![WF Fusion](./images/wffusion82.png)

右键单击&#x200B;**Photoshop更改文本**&#x200B;节点，然后选择&#x200B;**克隆**。

![WF Fusion](./images/wffusion83.png)

将克隆的HTTP请求拖到刚刚创建的&#x200B;**设置多个变量**&#x200B;节点之后。

![WF Fusion](./images/wffusion83.png)

右键单击克隆的HTTP请求，选择&#x200B;**重命名**&#x200B;并将名称更改为&#x200B;**Photoshop检查状态**。

![WF Fusion](./images/wffusion84.png)

选择以打开HTTP请求。 更改URL以使其引用您在上一步中创建的变量，并将&#x200B;**方法**&#x200B;设置为&#x200B;**GET**。

![WF Fusion](./images/wffusion85.png)

通过选择空选项删除&#x200B;**正文**。

![WF Fusion](./images/wffusion86.png)

选择&#x200B;**确定**。

![WF Fusion](./images/wffusion87.png)

选择&#x200B;**运行一次**。

![WF Fusion](./images/wffusion88.png)

出现包含字段&#x200B;**status**，且状态设置为&#x200B;**正在运行**&#x200B;的响应。 Photoshop需要几秒钟才能完成此过程。

![WF Fusion](./images/wffusion89.png)

现在您知道该响应还需要一段时间才能完成，因此最好在此HTTP请求前面添加计时器，以便它不会立即运行。

选择&#x200B;**工具**&#x200B;节点，然后选择&#x200B;**休眠**。

![WF Fusion](./images/wffusion90.png)

将&#x200B;**休眠**&#x200B;节点放置在&#x200B;**设置多个变量**&#x200B;和&#x200B;**Photoshop检查状态**&#x200B;之间。 将&#x200B;**延迟**&#x200B;设置为&#x200B;**5**&#x200B;秒。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion91.png)

您的屏幕应如下所示。 以下配置的挑战是，等待5秒可能足够了，但可能还不够。 实际上，最好有一个更智能的解决方案，如do...while循环，每5秒检查一次状态，直到状态等于&#x200B;**succeeded**。 因此，您可以在后续步骤中实施此类策略。

![WF Fusion](./images/wffusion92.png)

选择介于&#x200B;**设置多个变量**&#x200B;和&#x200B;**睡眠**&#x200B;之间的&#x200B;**扳手**&#x200B;图标。 选择&#x200B;**添加模块**。

![WF Fusion](./images/wffusion93.png)

搜索`flow`，然后选择&#x200B;**流量控制**。

![WF Fusion](./images/wffusion94.png)

选择&#x200B;**中继器**。

![WF Fusion](./images/wffusion95.png)

将&#x200B;**重复**&#x200B;设置为&#x200B;**20**。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion96.png)

接下来，在&#x200B;**Photoshop检查状态**&#x200B;上选择&#x200B;**+**&#x200B;以添加另一个模块。

![WF Fusion](./images/wffusion97.png)

搜索&#x200B;**流**&#x200B;并选择&#x200B;**流控制**。

![WF Fusion](./images/wffusion98.png)

选择&#x200B;**数组汇总**。

![WF Fusion](./images/wffusion99.png)

将&#x200B;**Source模块**&#x200B;设置为&#x200B;**中继器**。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion100.png)

屏幕应如下所示：

![WF Fusion](./images/wffusion101.png)

选择&#x200B;**扳手**&#x200B;图标并选择&#x200B;**添加模块**。

![WF Fusion](./images/wffusion102.png)

搜索&#x200B;**工具**&#x200B;并选择&#x200B;**工具**。

![WF Fusion](./images/wffusion103.png)

选择&#x200B;**获取多个变量**。

![WF Fusion](./images/wffusion104.png)

选择&#x200B;**+添加项**&#x200B;并将&#x200B;**变量名称**&#x200B;设置为`done`。

![WF Fusion](./images/wffusion105.png)

选择&#x200B;**确定**。

![WF Fusion](./images/wffusion106.png)

选择您之前配置的&#x200B;**设置多个变量**&#x200B;节点。 为了初始化变量&#x200B;**done**，您需要在此处将其设置为`false`。 选择&#x200B;**+添加项**。

![WF Fusion](./images/wffusion107.png)

将`done`用于&#x200B;**变量名称**

要设置状态，需要一个布尔值。 要查找布尔值，请选择&#x200B;**齿轮**，然后选择`false`。 选择&#x200B;**添加**。

![WF Fusion](./images/wffusion108.png)

选择&#x200B;**确定**。

![WF Fusion](./images/wffusion109.png)

接下来，在您配置的&#x200B;**获取多个变量**&#x200B;节点之后选择&#x200B;**扳手**&#x200B;图标。

![WF Fusion](./images/wffusion110.png)

选择&#x200B;**设置筛选器**。 您现在需要检查变量&#x200B;**done**&#x200B;的值。 如果该值设置为&#x200B;**false**，则必须执行循环的下一部分。 如果值设置为&#x200B;**true**，则表示进程已成功完成，因此无需继续循环的下一部分。

![WF Fusion](./images/wffusion111.png)

对于标签，请使用&#x200B;**我们完成了吗？**&#x200B;的问题。使用现有变量&#x200B;**done**&#x200B;设置&#x200B;**Condition**，运算符应设置为&#x200B;**等于**，值应为布尔变量`false`。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion112.png)

接下来，在节点&#x200B;**Photoshop检查状态**&#x200B;和&#x200B;**数组聚合器**&#x200B;之间腾出一些空间。 然后，选择&#x200B;**扳手**&#x200B;图标并选择&#x200B;**添加路由器**。 您这样做是因为在检查Photoshop文件的状态后，应该有2条路径。 如果状态为`succeeded`，则&#x200B;**done**&#x200B;的变量应设置为`true`。 如果状态不等于`succeeded`，则循环应继续。 路由器将可以检查并设置此项。

![WF Fusion](./images/wffusion113.png)

添加路由器后，选择&#x200B;**扳手**&#x200B;图标，然后选择&#x200B;**设置过滤器**。

![WF Fusion](./images/wffusion114.png)

对于标签，请使用&#x200B;**我们已完成**。 通过选择响应字段&#x200B;**data.outputs[].status**&#x200B;来使用&#x200B;**Photoshop检查状态**&#x200B;节点的响应设置&#x200B;**条件**，运算符应设置为&#x200B;**等于**，值应为`succeeded`。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion115.png)

接下来，选择带有问号的空节点并搜索&#x200B;**工具**。 然后选择&#x200B;**工具**。

![WF Fusion](./images/wffusion116.png)

选择&#x200B;**设置多个变量**。

![WF Fusion](./images/wffusion117.png)

使用路由器的此分支时，表示Photoshop文件创建的状态已成功完成。 这意味着do...while循环不再需要继续检查Photoshop中的状态，因此应将变量`done`设置为`true`。

对于&#x200B;**变量名称**，请使用`done`。

对于&#x200B;**变量值**，应使用布尔值`true`。 选择&#x200B;**齿轮**&#x200B;图标，然后选择`true`。 选择&#x200B;**添加**。

![WF Fusion](./images/wffusion118.png)

选择&#x200B;**确定**。

![WF Fusion](./images/wffusion119.png)

接下来，右键单击刚刚创建的&#x200B;**设置多个变量**&#x200B;节点，然后选择&#x200B;**克隆**。

![WF Fusion](./images/wffusion120.png)

拖动克隆的节点，使其与&#x200B;**数组聚合器**&#x200B;连接。 然后，右键单击该节点并选择&#x200B;**重命名**，然后将其名称更改为`Placeholder End`。

![WF Fusion](./images/wffusion122.png)

删除现有变量并选择&#x200B;**+添加项**。 对于&#x200B;**变量名称**，请使用`placeholder`；对于&#x200B;**变量值**，请使用`end`。 选择&#x200B;**添加**，然后选择&#x200B;**确定**。

![WF Fusion](./images/wffusion123.png)

选择&#x200B;**保存**&#x200B;以保存您的方案。 接下来，选择   **运行一次**。

![WF Fusion](./images/wffusion124.png)

随后将执行场景，并成功完成。 请注意，您配置的do...while循环工作正常。 在下面的运行中，您可以看到根据&#x200B;**工具>获取多个变量**&#x200B;节点上的气泡，**中继器**&#x200B;运行了20次。 在该节点之后，您配置了一个用于检查状态的过滤器，并且仅当状态不等于&#x200B;**succeeded**&#x200B;时，才会执行后续节点。 在此运行中，筛选器之后的部分仅运行一次，因为在第一次运行中状态已经是&#x200B;**成功**。

![WF Fusion](./images/wffusion125.png)

您可以通过单击&#x200B;**Photoshop检查状态** HTTP请求上的气泡并细化到&#x200B;**状态**&#x200B;字段，来验证新Photoshop文件创建状态。

![WF Fusion](./images/wffusion126.png)

您现在已配置可重复方案的基本版本，可自动执行一些步骤。 在下一个练习中，您将通过增加复杂性来迭代这一点。

## 后续步骤

转到[使用Workfront Fusion实现流程自动化](./ex3.md){target="_blank"}

返回到[用Workfront Fusion实现Creative Workflow Automation](./automation.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
