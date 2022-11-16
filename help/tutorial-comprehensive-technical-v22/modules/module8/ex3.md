---
title: Adobe Journey Optimizer — 外部天气API、短信操作等 — 定义自定义操作
description: Adobe Journey Optimizer — 外部天气API、短信操作等 — 定义自定义操作
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7ee5aee9-3740-4eee-9f53-a44fdb564a00
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 8.3定义自定义操作

在本练习中，您将结合使用Adobe Journey Optimizer来创建两个自定义操作。

通过转到Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

您将被重定向到 **主页**  查看Journey Optimizer。 首先，确保您使用的是正确的沙盒。 要使用的沙盒称为 `--aepSandboxId--`. 要从一个沙盒更改为另一个沙盒，请单击 **生产产品(VA7)** 并从列表中选择沙盒。 在此示例中，沙盒名为 **2022财年AEP启用**. 然后你会在 **主页** 沙盒视图 `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

在左侧菜单中，向下滚动并单击 **配置**. 接下来，单击 **管理** 按钮 **操作**.

![演示](./images/menuactions.png)

然后您将看到 **操作** 列表。

![演示](./images/acthome.png)

您将定义一个向Slack渠道发送文本的操作。

## 8.3.1操作：将文本发送到Slack渠道

您现在将使用现有Slack渠道并向该Slack渠道发送消息。 Slack具有易于使用的API，我们将使用Adobe Journey Optimizer触发其API。

![演示](./images/slack.png)

单击 **创建操作** 以开始添加新操作。

![演示](./images/adda.png)

您将看到一个空的“操作”弹出窗口。

![演示](./images/emptyact.png)

作为操作的名称，请使用 `--demoProfileLdap--TextSlack`. 在此示例中，操作名称为 `vangeluwTextSlack`.

将描述设置为： `Send Text to Slack`.

![演示](./images/slackname.png)

对于 **URL配置**，使用以下代码：

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- 方法： **POST**

>[!NOTE]
>
>上述URL引用AWS Lambda函数，该函数随后会将您的请求转发到上述Slack渠道。 这样做是为了保护对Adobe拥有的Slack渠道的访问。 如果您有自己的Slack渠道，则应通过 [https://api.slack.com/](https://api.slack.com/)，则需要在该Slack应用程序中创建传入Webhook，然后使用传入Webhook URL替换上述URL。

您无需更改标题字段。

![演示](./images/slackurl.png)

**身份验证** 应设置为 **无身份验证**.

![演示](./images/slackauth.png)

对于 **操作参数**，您需要定义应将哪些字段发送到Slack。 从逻辑上讲，我们希望Adobe Journey Optimizer和Adobe Experience Platform是个性化的大脑，因此要发送到Slack的文本应由Adobe Journey Optimizer定义，然后发送到Slack以执行。

因此，对于 **操作参数**，请单击 **编辑负载** 图标。

![演示](./images/slackmsgp.png)

然后，您将看到一个空的弹出窗口。

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

答：通过指定以下字段，这些字段将可从您的客户历程访问，并且您将能够从历程动态填充它们：

**&quot;toBeMapped&quot;:真的，**

**&quot;dataType&quot;:&quot;string&quot;,**

**&quot;label&quot;:&quot;textToSlack&quot;**

然后您将看到：

![演示](./images/slackmsgpopup1.png)

单击&#x200B;**保存**。

![演示](./images/twiliomsgpopup2.png)

向上滚动并单击 **保存** 再次保存自定义操作。

![演示](./images/slackmsgpopup3.png)

现在，您的自定义操作是 **操作** 列表。

![演示](./images/slackdone.png)

您定义了事件、外部数据源和操作。 现在，让我们将所有这些整合到一个历程中。

下一步： [8.4创建历程和消息](./ex4.md)

[返回模块8](journey-orchestration-external-weather-api-sms.md)

[返回到所有模块](../../overview.md)
