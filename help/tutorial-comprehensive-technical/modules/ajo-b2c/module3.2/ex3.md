---
title: Adobe Journey Optimizer — 外部天气API、SMS操作等 — 定义自定义操作
description: Adobe Journey Optimizer — 外部天气API、SMS操作等 — 定义自定义操作
kt: 5342
doc-type: tutorial
exl-id: d9bdc4c6-7539-4646-9b75-f397b792479f
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 3%

---

# 3.2.3定义自定义操作

在本练习中，您将创建一个自定义操作以向Slack渠道发送消息。

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

现在，您将使用现有的Slack渠道并将消息发送到该Slack渠道。 Slack具有易于使用的API，您将使用Adobe Journey Optimizer触发其API。

![演示](./images/slack.png)

在左侧菜单中，向下滚动并单击&#x200B;**配置**。 接下来，单击&#x200B;**操作**&#x200B;下的&#x200B;**管理**&#x200B;按钮。

![演示](./images/menuactions.png)

您随后将看到&#x200B;**操作**&#x200B;列表。 单击&#x200B;**创建操作**。

![演示](./images/acthome.png)

您将会看到一个空的“操作”弹出窗口。

![演示](./images/emptyact.png)

作为操作的名称，请使用`--aepUserLdap--TextSlack`。

将描述设置为： `Send Message to Slack`。

对于&#x200B;**URL配置**，请使用此：

- URL： `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- 方法： **POST**

>[!NOTE]
>
>上述URL引用AWS Lambda函数，该函数随后会将您的请求转发到上述Slack渠道。 这是为了保护对Adobe拥有的Slack渠道的访问。 如果您拥有自己的Slack渠道，则应通过[https://api.slack.com/](https://api.slack.com/)创建一个Slack应用，然后需要在该Slack应用中创建传入Webhook，然后将上述URL替换为传入Webhook URL。

![演示](./images/slackname.png)

您无需更改标题字段。

![演示](./images/slackurl.png)

**身份验证**&#x200B;应设置为&#x200B;**无身份验证**。

![演示](./images/slackauth.png)

在&#x200B;**负载**&#x200B;下，您需要定义应将哪些字段发送到Slack。 从逻辑上讲，您希望Adobe Journey Optimizer和Adobe Experience Platform成为个性化的大脑，因此要发送到Slack的文本应该由Adobe Journey Optimizer定义，然后发送到Slack以供执行。

对于&#x200B;**请求**，单击&#x200B;**编辑有效负载**&#x200B;图标。

![演示](./images/slackmsgp.png)

然后您会看到一个空的弹出窗口。

![演示](./images/slackmsgpopup.png)

复制以下文本并将其粘贴到空弹出窗口中。

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

您随后将看到以下内容：

![演示](./images/slackmsgpopup1.png)

向上滚动，再次单击&#x200B;**保存**&#x200B;以保存您的操作。

![演示](./images/slackmsgpopup3.png)

您的自定义操作现已成为&#x200B;**操作**&#x200B;列表的一部分。

![演示](./images/slackdone.png)

您已定义事件、外部数据源和操作。 现在，让我们将所有这些整合到一个历程中。

下一步： [3.2.4创建您的历程和消息](./ex4.md)

[返回模块3.2](journey-orchestration-external-weather-api-sms.md)

[返回所有模块](../../../overview.md)
