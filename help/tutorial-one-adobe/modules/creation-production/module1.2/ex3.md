---
title: Workfront Fusion的流程自动化
description: 了解如何使用Workfront Fusion处理自动化
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 1.2.3 Workfront Fusion的流程自动化

了解如何使用Workfront Fusion实现流程自动化。

## 1.2.3.1对多个值迭代

您的方案应如下所示：

![WF Fusion](./images/wffusion200.png)

到目前为止，您已按静态值更改Photoshop文件中的文本。 要缩放和自动化您的内容创建工作流，需要对值列表进行迭代，并将这些值动态插入到Photoshop文件中。 在接下来的步骤中，您将添加一个用于迭代现有方案中的值的水。

在&#x200B;**Router**&#x200B;节点和&#x200B;**Photoshop更改文本**&#x200B;节点之间，选择&#x200B;**扳手**&#x200B;图标并选择&#x200B;**添加模块**。

![WF Fusion](./images/wffusion201.png)

搜索`flow`并选择&#x200B;**流量控制**。

![WF Fusion](./images/wffusion202.png)

选择&#x200B;**迭代器**。

![WF Fusion](./images/wffusion203.png)

屏幕应如下所示：

![WF Fusion](./images/wffusion204.png)

虽然现在可以读取CSV文件等输入文件，但您需要定义文本字符串并拆分该CSV文件，从而使用该CSV文件的基本版本。

您可以通过选择&#x200B;**T**&#x200B;图标来查找&#x200B;**拆分**&#x200B;函数，您可以在其中查看所有可用于处理文本值的函数。 选择&#x200B;**拆分**&#x200B;函数，您应该会看到此内容。

![WF Fusion](./images/wffusion206.png)

split函数需要分号前有一个值数组，并需要您在分号后指定分隔符。 对于此测试，您应该使用包含2个字段的简单数组，**立即购买**&#x200B;和&#x200B;**单击此处**，要使用的分隔符为&#x200B;**，**。

通过替换当前空的&#x200B;**split**&#x200B;函数： `{{split("Buy now, Click here "; ",")}}`，在&#x200B;**数组**&#x200B;字段中输入此值。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion205.png)

选择&#x200B;**Photoshop更改文本**&#x200B;以添加某些变量，而不是为输入和输出字段添加静态值。

![WF Fusion](./images/wffusion207.png)

在&#x200B;**请求内容**&#x200B;中，是文本&#x200B;**单击此处**。 此文本需要替换为您数组中的值。

![WF Fusion](./images/wffusion208.png)

删除文本&#x200B;**单击此处**，然后通过从&#x200B;**迭代器**&#x200B;节点中选择变量&#x200B;**值**&#x200B;来替换它。 这可确保动态更新Photoshop文档中按钮上的文本。

![WF Fusion](./images/wffusion209.png)

您还需要更新用于在Azure存储帐户中写入文件的文件名。 如果文件名是静态的，则每个新小版本只覆盖上一个文件，因此会丢失自定义文件。 当前静态文件名是&#x200B;**citisignal-fibre-changed-text.psd**，您现在需要更新它。

将光标置于单词`text`之后。

![WF Fusion](./images/wffusion210.png)

首先，添加连字符`-`，然后选择值&#x200B;**捆绑订单位置**。 这可确保对于第一次迭代，Workfront Fusion将`-1`添加到文件名，对于第二次迭代`-2`等。 选择&#x200B;**确定**。

![WF Fusion](./images/wffusion211.png)

保存方案，然后选择&#x200B;**运行一次**。

![WF Fusion](./images/wffusion212.png)

运行该方案后，返回您的Azure存储资源管理器并刷新文件夹。 然后，您应该会看到2个新创建的文件。

![WF Fusion](./images/wffusion213.png)

下载并打开每个文件。 按钮上应该有各种文本。 这是文件`citisignal-fiber-changed-text-1.psd`。

![WF Fusion](./images/wffusion214.png)

这是文件`citisignal-fiber-changed-text-2.psd`。

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2使用Webhook激活您的方案

到目前为止，您已手动运行方案进行测试。 现在，让我们使用webhook更新您的场景，以便可以从外部环境激活它。

选择&#x200B;**+**，搜索&#x200B;**webhook**，然后选择&#x200B;**Webhook**。

![WF Fusion](./images/wffusion216.png)

选择&#x200B;**自定义webhook**。

拖动并连接&#x200B;**自定义webhook**&#x200B;节点，以使其连接到画布上的第一个节点，该节点称为&#x200B;**初始化常量**。

![WF Fusion](./images/wffusion217.png)

选择&#x200B;**自定义webhook**&#x200B;节点。 然后选择&#x200B;**添加**。

![WF Fusion](./images/wffusion218.png)

将&#x200B;**Webhook名称**&#x200B;设置为`--aepUserLdap-- - Tutorial 1.2`。

![WF Fusion](./images/wffusion219.png)

选中&#x200B;**获取请求标头**&#x200B;的框。 选择&#x200B;**保存**。

![WF Fusion](./images/wffusion220.png)

您的Webhook URL现在可用。 复制URL。

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
	"psdTemplate": "placeholder",
	"xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

返回Workfront Fusion，您的自定义Webhook上会显示一条消息： **已成功确定**。

![WF Fusion](./images/wffusion227.png)

选择&#x200B;**保存**，然后选择&#x200B;**运行一次**。 您的方案现在处于活动状态，但在您再次在Postman中选择&#x200B;**发送**&#x200B;之前不会运行。

![WF Fusion](./images/wffusion230.png)

在Postman中，再次选择&#x200B;**发送**。

![WF Fusion](./images/wffusion228.png)

您的方案会再次运行，并像之前一样创建2个文件。

![WF Fusion](./images/wffusion232.png)

将Postman请求的名称更改为`POST - Send Request to Workfront Fusion Webhook`。

![WF Fusion](./images/wffusion233.png)

现在需要开始使用变量&#x200B;**psdTemplate**。 您将使用Postman请求中的传入变量，而不是对输入文件在&#x200B;**Photoshop更改文本**&#x200B;节点中的位置进行硬编码。

打开&#x200B;**Photoshop更改文本**&#x200B;节点并转到&#x200B;**请求内容**。 在&#x200B;**inputs**&#x200B;下选择硬编码文件名&#x200B;**citisignal-fibre.psd**&#x200B;并将其删除。

![WF Fusion](./images/wffusion234.png)

选择变量&#x200B;**psdTemplate**。 选择&#x200B;**确定**，然后保存您的方案。

![WF Fusion](./images/wffusion235.png)

选择&#x200B;**开启**&#x200B;以打开您的方案。 您的方案现在运行的是不停机。

![WF Fusion](./images/wffusion236.png)

返回Postman，输入文件名`citisignal-fiber.psd`作为变量&#x200B;**psdTemplate**&#x200B;的值，然后再次选择&#x200B;**发送**&#x200B;以再次运行方案。

![WF Fusion](./images/wffusion237.png)

通过将PSD模板指定为外部系统提供的变量，您现在构建了一个可重复使用的方案。

现在，您已完成此练习。

## 后续步骤

使用连接器[&#128279;](./ex4.md){target="_blank"}转到1.2.4自动化

返回到[使用Workfront Fusion的Creative工作流自动化](./automation.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
