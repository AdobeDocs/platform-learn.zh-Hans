---
title: 使用连接器实现自动化
description: 使用连接器实现自动化
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 0b20ba91-28d4-4f4d-8abe-074f802c389e
source-git-commit: c9807ef0787f4390d12bc7285cfe71260aa3eabf
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 1%

---

# 1.2.4使用连接器实现自动化

现在，您将开始在Workfront Fusion for Photoshop中使用现成的连接器，并将Firefly Text-2-Image请求和Photoshop请求连接到一个场景中。

## 1.2.4.1更新变量

在继续连接器设置之前，需要将以下变量添加到&#x200B;**初始化常量**&#x200B;模块。

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

## 1.2.4.2使用webhook激活您的场景

到目前为止，您已手动运行场景进行测试。 现在，让我们使用webhook更新您的场景，以便可以从外部环境激活它。

选择&#x200B;**+**，搜索&#x200B;**webhook**，然后选择&#x200B;**Webhook**。

![WF Fusion](./images/wffusion216.png)

选择&#x200B;**自定义webhook**。

![WF Fusion](./images/wffusion217.png)

将&#x200B;**自定义webhook**&#x200B;模块拖动到方案的开头。 接下来，选择&#x200B;**clock**&#x200B;图标并将其拖动到&#x200B;**自定义webhook**&#x200B;模块。

![WF Fusion](./images/wffusion217a.png)

您应该会看到此内容。 接下来，将第一个模块上的红点朝第二个模块上的紫点拖动。

![WF Fusion](./images/wffusion217b.png)

您应该会看到此内容。 新建，单击&#x200B;**自定义webhook**&#x200B;模块。

![WF Fusion](./images/wffusion217c.png)

单击&#x200B;**添加**。

![WF Fusion](./images/wffusion218.png)

将&#x200B;**Webhook名称**&#x200B;设置为`--aepUserLdap-- - Firefly + Photoshop Webhook`。 单击&#x200B;**保存**。

![WF Fusion](./images/wffusion219.png)

您的webhook URL现已可用。 单击&#x200B;**将地址复制到剪贴板**&#x200B;以复制URL。

![WF Fusion](./images/wffusion221.png)

打开Postman，并在集合&#x200B;**FF - Firefly Services技术内部人士**&#x200B;中添加新文件夹。

![WF Fusion](./images/wffusion222.png)

命名您的文件夹`--aepUserLdap-- - Workfront Fusion`。

![WF Fusion](./images/wffusion223.png)

在刚刚创建的文件夹中，选择3个圆点&#x200B;**...**，然后选择&#x200B;**添加请求**。

![WF Fusion](./images/wffusion224.png)

将&#x200B;**方法类型**&#x200B;设置为&#x200B;**POST**，并将webhook的URL粘贴到地址栏中。

![WF Fusion](./images/wffusion225.png)

您需要发送自定义主体，以便可以将外部源中的变量元素提供给Workfront Fusion方案。

转到&#x200B;**正文**&#x200B;并选择&#x200B;**原始**。

![WF Fusion](./images/wffusion226.png)

将以下文本粘贴到请求正文中。 选择&#x200B;**发送**。

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

![WF Fusion](./images/wffusion229.png)

返回到Workfront Fusion后，您的自定义webhook上会显示一条消息，显示：**已成功确定**。

![WF Fusion](./images/wffusion227.png)

## 1.2.4.3 Adobe Firefly连接器

单击&#x200B;**+**&#x200B;图标以添加新模块。

![WF Fusion](./images/wffcff2.png)

输入搜索词`Adobe Firefly`，然后选择&#x200B;**Adobe Firefly**。

![WF Fusion](./images/wffcff2a.png)

选择&#x200B;**生成图像**。

![WF Fusion](./images/wffcff3.png)

单击&#x200B;**Adobe Firefly**&#x200B;模块以将其打开，然后单击&#x200B;**添加**&#x200B;以创建新连接。

![WF Fusion](./images/wffcff5.png)

填写以下字段：

- **连接名称**：使用`--aepUserLdap-- - Firefly connection`。
- **环境**：使用&#x200B;**生产**。
- **类型**：使用&#x200B;**个人帐户**。
- **客户端ID**：从名为&#x200B;**的Adobe I/O项目中复制**&#x200B;客户端ID`--aepUserLdap-- - One Adobe tutorial`。
- **客户端密钥**：从名为&#x200B;**的Adobe I/O项目中复制**&#x200B;客户端密钥`--aepUserLdap-- - One Adobe tutorial`。

您可以在&#x200B;**此处**&#x200B;找到Adobe I/O项目的&#x200B;**客户端ID**&#x200B;和[客户端密钥](https://developer.adobe.com/console/projects.){target="_blank"}。

![WF Fusion](./images/wffc20.png)

填写完所有字段后，单击&#x200B;**继续**。 然后，将自动验证您的连接。

![WF Fusion](./images/wffcff6.png)

接下来，选择传入的&#x200B;**自定义webhook**&#x200B;提供给方案的变量&#x200B;**prompt**。

![WF Fusion](./images/wffcff7.png)

将&#x200B;**模型版本** **提示符**&#x200B;设置为&#x200B;**image4 standard**。 单击&#x200B;**确定**。

![WF Fusion](./images/wffcff7b.png)

单击&#x200B;**保存**&#x200B;以保存更改，然后单击&#x200B;**运行一次**&#x200B;以测试配置。

![WF Fusion](./images/wffcff8.png)

转到Postman，验证请求中的提示，然后单击&#x200B;**发送**。

![WF Fusion](./images/wffcff8a.png)

单击“发送”后，请返回Workfront Fusion并单击&#x200B;**Adobe Firefly**&#x200B;模块上的气泡图标以验证详细信息。

![WF Fusion](./images/wffcff9.png)

进入&#x200B;**OUTPUT** - **详细信息** > **URL**&#x200B;以查找由&#x200B;**Adobe Firefly**&#x200B;生成的图像的URL。

![WF Fusion](./images/wffcff10.png)

复制URL并将其粘贴到浏览器中。 现在，您应该会看到一个图像，该图像表示您从Postman请求发送的提示，在本例中为&#x200B;**雾状草原**。

![WF Fusion](./images/wffcff11.png)

## 1.2.4.2更改PSD文件的背景

您现在将更新场景，以使用更多开箱即用连接器使其更智能。 您还将输出从Firefly连接到Photoshop，以便PSD文件的背景图像通过使用Firefly的“生成图像”操作输出动态更改。

您应该会看到此内容。 接下来，将鼠标悬停在&#x200B;**Adobe Firefly**&#x200B;模块上，然后单击&#x200B;**+**&#x200B;图标。

![WF Fusion](./images/wffc15.png)

在搜索菜单中，输入`Photoshop`，然后单击&#x200B;**Adobe Photoshop**&#x200B;操作。

![WF Fusion](./images/wffc16.png)

选择&#x200B;**应用PSD编辑**。

![WF Fusion](./images/wffc17.png)

您应该会看到此内容。 单击&#x200B;**添加**&#x200B;以添加与Adobe Photoshop的新连接。

![WF Fusion](./images/wffc18.png)

按如下方式配置连接：

- 连接类型：选择&#x200B;**Adobe Photoshop （服务器到服务器）**
- 连接名称：输入`--aepUserLdap-- - Adobe I/O`
- 客户端ID：粘贴您的客户端ID
- 客户端密码：粘贴您的客户端密码

单击&#x200B;**继续**。

![WF Fusion](./images/wffc19.png)

要查找您的&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**，请转到[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}并打开名为`--aepUserLdap-- One Adobe tutorial`的Adobe I/O项目。 转到&#x200B;**OAuth服务器到服务器**&#x200B;以查找您的客户端ID和客户端密钥。 复制这些值，并将其粘贴到Workfront Fusion的连接设置中。

![WF Fusion](./images/wffc20.png)

单击&#x200B;**继续**&#x200B;后，在验证您的凭据时，将会短暂显示一个弹出窗口。 完成后，您应该会看到此内容。

![WF Fusion](./images/wffc21.png)

现在，您需要输入希望Fusion使用的PSD文件的文件位置。 对于&#x200B;**存储**，选择&#x200B;**Azure**，对于&#x200B;**文件位置**，输入`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/{{1.AZURE_STORAGE_SAS_READ}}`。 将光标放在第二个`/`旁边。 然后，查看可用变量并向下滚动以查找变量&#x200B;**psdTemplate**。 单击变量&#x200B;**psdTemplate**&#x200B;以将其选定。

![WF Fusion](./images/wffc22.png)

您应该会看到此内容。

![WF Fusion](./images/wffc23.png)

一直向下滚动直到看到&#x200B;**图层**。 单击&#x200B;**添加项**。

![WF Fusion](./images/wffc24.png)

您应该会看到此内容。 现在，您需要在Photoshop PSD模板中输入用于文件背景的图层的名称。

![WF Fusion](./images/wffc25.png)

在文件&#x200B;**citisignal-fibre.psd**&#x200B;中，您将找到用于背景的图层。 在此示例中，该图层名为&#x200B;**2048x2048-background**。

![WF Fusion](./images/wffc26.png)

在Workfront Fusion对话框中粘贴名称&#x200B;**2048x2048-background**。

![WF Fusion](./images/wffc27.png)

向下滚动，直到看到&#x200B;**输入**。 现在，您需要定义需要插入到背景图层中的内容。 在这种情况下，您需要选择包含动态生成的图像的&#x200B;**Adobe Firefly**&#x200B;模块的输出。

对于&#x200B;**存储**，请选择&#x200B;**外部**。 对于&#x200B;**文件位置**，您需要从`{{XX.details[].url}}`Adobe Firefly **模块的输出复制并粘贴变量**，但您需要使用&#x200B;**Adobe Firefly**&#x200B;模块的序列号替换变量中的&#x200B;**XX**，本例中为&#x200B;**5**。

![WF Fusion](./images/wffc28.png)

接下来，向下滚动，直到看到&#x200B;**编辑**。 将&#x200B;**Edit**&#x200B;设置为&#x200B;**Yes**&#x200B;并将&#x200B;**Type**&#x200B;设置为&#x200B;**Layer**。 单击&#x200B;**添加**。

![WF Fusion](./images/wffc29.png)

您应该会看到此内容。 接下来，您需要定义操作的输出。 单击&#x200B;**输出**&#x200B;下的&#x200B;**添加项**。

![WF Fusion](./images/wffc30.png)

为&#x200B;**存储**&#x200B;选择&#x200B;**Azure**，将此`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{1.AZURE_STORAGE_SAS_WRITE}}`粘贴到&#x200B;**文件位置**&#x200B;下，并在&#x200B;**类型**&#x200B;下选择&#x200B;**vnd.adobe.photoshop**。 单击以启用&#x200B;**显示高级设置**。

![WF Fusion](./images/wffc31.png)

在&#x200B;**高级设置**&#x200B;下，选择&#x200B;**是**以覆盖同名文件。
单击**添加**。

![WF Fusion](./images/wffc32.png)

然后您应该拥有此项。 单击&#x200B;**确定**。

![WF Fusion](./images/wffc33.png)

单击&#x200B;**保存**&#x200B;以保存更改，然后单击&#x200B;**运行一次**&#x200B;以测试配置。

![WF Fusion](./images/wffc33a.png)

转到Postman，验证请求中的提示，然后单击&#x200B;**发送**。

![WF Fusion](./images/wffcff8a.png)

您应该会看到此内容。 单击&#x200B;**Adobe Photoshop — 应用PSD编辑**&#x200B;模块上的气泡。

![WF Fusion](./images/wffc33b.png)

您现在可以看到已成功生成新的PSD文件并将其存储在您的Microsoft Azure存储帐户中。

![WF Fusion](./images/wffc33c.png)

## 1.2.4.3更改PSD文件的文本图层

接下来，将鼠标悬停在&#x200B;**Adobe Photoshop — 应用PSD编辑**&#x200B;模块上，然后单击&#x200B;**+**&#x200B;图标。

![WF Fusion](./images/wffc34.png)

选择&#x200B;**Adobe Photoshop**。

![WF Fusion](./images/wffc35.png)

选择&#x200B;**编辑文本图层**。

![WF Fusion](./images/wffc36.png)

您应该会看到此内容。 首先，选择您之前已配置的Adobe Photoshop连接，该连接应名为`--aepUserLdap-- Adobe I/O`。

![WF Fusion](./images/wffc37.png)

对于&#x200B;**输入文件**，为&#x200B;**输入文件存储**&#x200B;选择&#x200B;**Azure**，并确保从上一个请求&#x200B;**Adobe Photoshop — 应用PSD编辑**&#x200B;中选择输出，您可以如下定义： ``{{XX.data[].`_links`.renditions[].href}}`` (将XX替换为上一个模块Adobe Photoshop — 应用PSD编辑的序列号)。

接下来，单击&#x200B;**图层**&#x200B;下的&#x200B;**+添加项**&#x200B;以开始添加需要更新的文本图层。

![WF Fusion](./images/wffc37a.png)

有2项需要更改，需要更新文件&#x200B;**citisignal-fibre.psd**&#x200B;中的CTA文本和按钮文本。

要查找层名称，请打开文件&#x200B;**citisignal-fibre.psd**。 在文件中，您会注意到包含call to action的层名为&#x200B;**2048x2048-cta**。

![WF Fusion](./images/wffc38.png)

在文件&#x200B;**citisignal-fibre.psd**&#x200B;中，您还会注意到包含call to action的层名为&#x200B;**2048x2048-button-text**。

![WF Fusion](./images/wffc44.png)

您首先需要配置需要对层&#x200B;**2048x2048-cta**&#x200B;进行的更改。 在对话框的&#x200B;**名称**&#x200B;下输入名称&#x200B;**2048x2048-cta**。

![WF Fusion](./images/wffc39.png)

向下滚动直到看到&#x200B;**文本** > **内容**。 从Webhook有效负载中选择变量&#x200B;**cta**。 单击&#x200B;**添加**。

![WF Fusion](./images/wffc40.png)

您应该会看到此内容。 单击&#x200B;**图层**&#x200B;下的&#x200B;**+添加项**&#x200B;开始添加需要更新的下一个文本图层。

![WF Fusion](./images/wffc40a.png)

在对话框的&#x200B;**名称**&#x200B;下输入名称&#x200B;**2048x2048-button-text**。

![WF Fusion](./images/wffc40b.png)

向下滚动直到看到&#x200B;**文本** > **内容**。 从Webhook有效负载中选择变量&#x200B;**按钮**。 单击&#x200B;**添加**。

![WF Fusion](./images/wffc40c.png)

您应该会看到此内容。

![WF Fusion](./images/wffc40d.png)

向下滚动，直到看到&#x200B;**输出**。 对于&#x200B;**存储**，请选择&#x200B;**Azure**。 对于&#x200B;**文件位置**，请输入以下位置。 请注意，在文件名中添加了变量`{{timestamp}}`，用于确保生成的每个文件都有唯一名称。 此外，将&#x200B;**Type**&#x200B;设置为&#x200B;**vnd.adobe.photoshop**。

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

将&#x200B;**Type**&#x200B;设置为&#x200B;**vnd.adobe.photoshop**。 单击&#x200B;**确定**。

![WF Fusion](./images/wffc41.png)

单击&#x200B;**保存**&#x200B;以保存更改。

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 Webhook响应

将这些更改应用于Photoshop文件后，您现在需要配置&#x200B;**Webhook响应**，该响应将发送回激活此方案的应用程序。

将鼠标悬停在模块&#x200B;**Adobe Photoshop — 编辑文本图层**&#x200B;上并单击&#x200B;**+**&#x200B;图标。

![WF Fusion](./images/wffc48.png)

搜索`webhooks`并选择&#x200B;**Webhook**。

![WF Fusion](./images/wffc49.png)

选择&#x200B;**Webhook响应**。

![WF Fusion](./images/wffc50.png)

您应该会看到此内容。 将以下有效负载粘贴到&#x200B;**主体**&#x200B;中。

```json
{
    "newPsdTemplate": ""
}
```

![WF Fusion](./images/wffc51.png)

复制并粘贴变量`{{XX.data[]._links.renditions[].href}}`并用最后&#x200B;**Adobe Photoshop — 编辑文本图层**&#x200B;模块的序列号替换&#x200B;**XX**，在本例中为&#x200B;**7**。

![WF Fusion](./images/wffc52.png)

启用&#x200B;**显示高级设置**&#x200B;的复选框，然后单击&#x200B;**添加项**。

![WF Fusion](./images/wffc52b.png)

在&#x200B;**键**&#x200B;字段中，输入`Content-Type`。 在&#x200B;**值**&#x200B;字段中，输入`application/json`。 单击&#x200B;**添加**。

![WF Fusion](./images/wffc52a.png)

然后您应该拥有此项。 单击&#x200B;**确定**。

![WF Fusion](./images/wffc53.png)

单击&#x200B;**自动对齐**。

![WF Fusion](./images/wffc54.png)

您应该会看到此内容。 单击&#x200B;**保存**&#x200B;以保存您的更改，然后单击&#x200B;**运行一次**&#x200B;以测试您的方案。

![WF Fusion](./images/wffc55.png)

返回Postman并单击&#x200B;**发送**。 此处使用的提示是&#x200B;**雾状草根**。

![WF Fusion](./images/wffc56.png)

随后将激活该方案，一段时间后，将在Postman中显示一个响应，其中包含新创建的PSD文件的URL。

![WF Fusion](./images/wffc58.png)

提醒您：一旦场景在Workfront Fusion中运行，您就可以通过单击每个模块上方的气泡来查看有关每个模块的信息。

![WF Fusion](./images/wffc59.png)

通过使用Azure Storage Explorer，您可以在Azure Storage Explorer中双击新创建的PSD文件来查找并打开该文件。

![WF Fusion](./images/wffc60.png)

然后，您的文件应如下所示，其背景将被&#x200B;**雾状草原**&#x200B;的背景所取代。

![WF Fusion](./images/wffc61.png)

如果您再次运行场景，然后使用其他提示从Postman发送新请求，您将看到场景变得多么容易且可重复使用。 在此示例中，使用的新提示为&#x200B;**sunny desert**。

![WF Fusion](./images/wffc62.png)

几分钟后，使用新背景生成了新的PSD文件。

![WF Fusion](./images/wffc63.png)

## 后续步骤

转到[1.2.3 Frame.io和Workfront Fusion](./ex3.md){target="_blank"}

返回到[使用Workfront Fusion的Creative工作流自动化](./automation.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
