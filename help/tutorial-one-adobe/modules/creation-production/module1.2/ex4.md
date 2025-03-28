---
title: 使用连接器实现自动化
description: 使用连接器实现自动化
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 1%

---

# 1.2.4使用连接器实现自动化

现在，您将开始在Workfront Fusion for Photoshop中使用现成的连接器，并将Firefly Text-2-Image请求和Photoshop请求连接到一个场景中。

## 1.2.4.1复制并准备您的方案

在左侧菜单中，转到&#x200B;**方案**&#x200B;并选择您的文件夹`--aepUserLdap--`。 然后，您应该会看到之前创建的名为`--aepUSerLdap-- - Adobe I/O Authentication`的方案。

![WF Fusion](./images/wffc1.png)

单击箭头打开下拉菜单，然后选择&#x200B;**克隆**。

![WF Fusion](./images/wffc2.png)

将克隆方案的&#x200B;**Name**&#x200B;设置为`--aepUserLdap-- - Firefly + Photoshop`并选择适当的&#x200B;**目标团队**。 单击&#x200B;**添加**&#x200B;添加新的webhook。

![WF Fusion](./images/wffc3.png)

将&#x200B;**Webhook名称**&#x200B;设置为`--aepUserLdap-- - Firefly + Photoshop Webhook`。 单击&#x200B;**保存**。

![WF Fusion](./images/wffc4.png)

您应该会看到此内容。 单击&#x200B;**保存**。

![WF Fusion](./images/wffc5.png)

您应该会看到此内容。 单击&#x200B;**Webhook**&#x200B;节点。

![WF Fusion](./images/wffc6.png)

单击&#x200B;**将地址复制到剪贴板**，然后单击&#x200B;**重新确定数据结构**。

![WF Fusion](./images/wffc7.png)

打开Postman。 在您之前使用的同一文件夹中添加新请求。

![WF Fusion](./images/wffc9.png)

确保应用以下设置：

- 请求名称： `POST - Send Request to Workfront Fusion Webhook Firefly + Photoshop`
- 请求类型： `POST`
- 请求URL：粘贴您从Workfront Fusion场景的webhook复制的URL。

转到&#x200B;**正文**&#x200B;并将&#x200B;**正文类型**&#x200B;设置为&#x200B;**原始** - **JSON**。 将以下有效负载粘贴到&#x200B;**主体**&#x200B;中。

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

此新有效负载将确保从场景外部提供所有变量信息，而不是在场景中对其进行硬编码。 在企业方案中，组织需要以可重用方式定义方案，这意味着需要提供多个变量作为输入变量，而不是在方案中对其进行硬编码。

然后您应该拥有此项。 单击&#x200B;**发送**。

![WF Fusion](./images/wffc10.png)

Workfront Fusion Webhook仍在等待输入。

![WF Fusion](./images/wffc11.png)

单击&#x200B;**发送**&#x200B;后，邮件应更改tp **成功确定**。 单击&#x200B;**确定**。

![WF Fusion](./images/wffc12.png)

## 1.2.4.2更新Firefly T2I节点

单击节点&#x200B;**Firefly T2I**。 您应该会看到此内容。 此请求中的提示之前已硬编码为字段&#x200B;**中的**&#x200B;马。 您现在将移除该硬编码文本，并将其替换为来自webhook的字段。

![WF Fusion](./images/wffcfft2i1.png)

移除字段&#x200B;**中的文本**&#x200B;马，并将其替换为可在&#x200B;**Webhook**&#x200B;变量下找到的变量&#x200B;**prompt**。 单击&#x200B;**确定**&#x200B;以保存更改。

![WF Fusion](./images/wffcfft2i2.png)

## 1.2.4.2更改PSD文件的背景

您现在将更新场景，以使用开箱即用连接器使其更智能。 您还将输出从Firefly连接到Photoshop，以便PSD文件的背景图像通过使用Firefly的“生成图像”操作输出动态更改。

在上一个练习中，您已禁用&#x200B;**Firefly T2I**&#x200B;路由。 您现在应该撤消此操作。 单击&#x200B;**stop**&#x200B;图标以再次启用路由。

![WF Fusion](./images/wffc13.png)

然后，您会看到&#x200B;**stop**&#x200B;图标消失。 接下来，单击指向上一个练习配置的其他路由上的&#x200B;**扳手**&#x200B;图标，并选择&#x200B;**禁用路由**。

![WF Fusion](./images/wffc14.png)

您应该会看到此内容。 接下来，将鼠标悬停在&#x200B;**Firefly T2I**&#x200B;节点上并单击&#x200B;**+**&#x200B;图标。

![WF Fusion](./images/wffc15.png)

在搜索菜单中，输入`Photoshop`，然后单击&#x200B;**Adobe Photoshop**&#x200B;操作。

![WF Fusion](./images/wffc16.png)

选择&#x200B;**应用PSD编辑**。

![WF Fusion](./images/wffc17.png)

您应该会看到此内容。 单击&#x200B;**添加**&#x200B;以添加与Adobe Photoshop的新连接。

![WF Fusion](./images/wffc18.png)

按如下方式配置连接：

- 连接类型：选择&#x200B;**Adobe Photoshop （服务器到服务器）**
- 连接名称：输入`--aepUserLdap-- - Adobe IO`
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

向下滚动，直到看到&#x200B;**输入**。 现在，您需要定义需要插入到背景图层中的内容。 在这种情况下，您需要选择Firefly T2I对象的输出，其中包含动态生成的图像。

对于&#x200B;**存储**，请选择&#x200B;**外部**。 对于&#x200B;**文件位置**，从&#x200B;**Firefly T2I**&#x200B;请求的输出中搜索并查找变量`data.outputs[].image.url`。

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

## 1.2.4.3更改PSD文件的文本图层

### 行动动员文本

接下来，将鼠标悬停在&#x200B;**Adobe Photoshop — 应用PSD编辑**&#x200B;节点上，然后单击&#x200B;**+**&#x200B;图标。

![WF Fusion](./images/wffc34.png)

选择&#x200B;**Adobe Photoshop**。

![WF Fusion](./images/wffc35.png)

选择&#x200B;**编辑文本图层**。

![WF Fusion](./images/wffc36.png)

您应该会看到此内容。 首先，选择您之前已配置的Adobe Photoshop连接，该连接应名为`--aepUserLdap-- Adobe IO`。

您现在需要定义&#x200B;**输入文件**&#x200B;的位置，这是上一步的输出，在&#x200B;**图层**&#x200B;下，您需要输入要更改的文本图层的&#x200B;**名称**。

![WF Fusion](./images/wffc37.png)

对于&#x200B;**输入文件**，为&#x200B;**输入文件存储**&#x200B;选择&#x200B;**Azure**，并确保从上一个请求&#x200B;**Adobe Photoshop — 应用PSD编辑**&#x200B;中选择输出，您可以从此处获取该输出： `data[]._links.renditions[].href`

![WF Fusion](./images/wffc37a.png)

打开文件&#x200B;**citisignal-fibre.psd**。 在文件中，您会注意到包含行动号召的层名为&#x200B;**2048x2048-cta**。

![WF Fusion](./images/wffc38.png)

在对话框的&#x200B;**名称**&#x200B;下输入名称&#x200B;**2048x2048-cta**。

![WF Fusion](./images/wffc39.png)

向下滚动直到看到&#x200B;**文本** > **内容**。 从Webhook有效负载中选择变量&#x200B;**cta**。

![WF Fusion](./images/wffc40.png)

向下滚动，直到看到&#x200B;**输出**。 对于&#x200B;**存储**，请选择&#x200B;**Azure**。 对于&#x200B;**文件位置**，请输入以下位置。 请注意，在文件名中添加了变量`{{timestamp}}`，用于确保生成的每个文件都有唯一名称。 此外，将&#x200B;**Type**&#x200B;设置为&#x200B;**vnd.adobe.photoshop**。 单击&#x200B;**确定**。

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc41.png)

### 按钮文本

右键单击刚刚创建的节点，然后选择&#x200B;**克隆**。 这将创建第二个类似的对象。

![WF Fusion](./images/wffc42.png)

您应该会看到此内容。 首先，选择您之前已配置的Adobe Photoshop连接，该连接应名为`--aepUserLdap-- Adobe IO`。

您现在需要定义&#x200B;**输入文件**&#x200B;的位置，这是上一步的输出，在&#x200B;**图层**&#x200B;下，您需要输入要更改的文本图层的&#x200B;**名称**。

![WF Fusion](./images/wffc43.png)

对于&#x200B;**输入文件**，为&#x200B;**输入文件存储**&#x200B;选择&#x200B;**Azure**，并确保从上一个请求&#x200B;**Adobe Photoshop — 编辑文本图层**&#x200B;中选择输出，可从此处获取该输出： `data[]._links.renditions[].href`

打开文件&#x200B;**citisignal-fibre.psd**。 在文件中，您会注意到包含行动号召的图层名为&#x200B;**2048x2048-button-text**。

![WF Fusion](./images/wffc44.png)

在对话框的&#x200B;**名称**&#x200B;下输入名称&#x200B;**2048x2048-cta**。

![WF Fusion](./images/wffc43.png)

向下滚动直到看到&#x200B;**文本** > **内容**。 从Webhook有效负载中选择变量&#x200B;**cta**。

![WF Fusion](./images/wffc45.png)

向下滚动，直到看到&#x200B;**输出**。 对于&#x200B;**存储**，请选择&#x200B;**Azure**。 对于&#x200B;**文件位置**，请输入以下位置。 请注意，在文件名中添加了变量`{{timestamp}}`，用于确保生成的每个文件都有唯一名称。 此外，将&#x200B;**Type**&#x200B;设置为&#x200B;**vnd.adobe.photoshop**。 单击&#x200B;**确定**。

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc46.png)

单击&#x200B;**保存**&#x200B;以保存更改。

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 Webhook响应

将这些更改应用于Photoshop文件后，您现在需要配置&#x200B;**Webhook响应**，该响应将发送回激活此方案的应用程序。

将鼠标悬停在节点&#x200B;**Adobe Photoshop — 编辑文本图层**&#x200B;上并单击&#x200B;**+**&#x200B;图标。

![WF Fusion](./images/wffc48.png)

搜索&#x200B;**webhook**&#x200B;并选择&#x200B;**Webhook**。

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

从上一个请求的输出中选择路径`data[]._links.renditions[].href`。 启用&#x200B;**显示高级设置**&#x200B;的复选框，然后单击&#x200B;**添加项**。

![WF Fusion](./images/wffc52.png)

在&#x200B;**键**&#x200B;字段中，输入`Content-Type`。 在&#x200B;**值**&#x200B;字段中，输入`application/json`。 单击&#x200B;**保存**。

![WF Fusion](./images/wffc52a.png)

然后您应该拥有此项。 单击&#x200B;**确定**。

![WF Fusion](./images/wffc53.png)

单击&#x200B;**自动对齐**。

![WF Fusion](./images/wffc54.png)

您应该会看到此内容。 单击&#x200B;**运行一次**。

![WF Fusion](./images/wffc55.png)

返回Postman并单击&#x200B;**发送**。 此处使用的提示是&#x200B;**雾状草根**。

![WF Fusion](./images/wffc56.png)

随后将激活该方案，一段时间后，将在Postman中显示一个响应，其中包含新创建的PSD文件的URL。

![WF Fusion](./images/wffc58.png)

提醒您：一旦场景在Workfront Fusion中运行，您就可以通过单击每个节点上方的气泡来查看有关每个节点的信息。

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

转到[Firefly Services Automation的摘要和优点](./summary.md){target="_blank"}

返回至[自动化Adobe Firefly服务](./automation.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
