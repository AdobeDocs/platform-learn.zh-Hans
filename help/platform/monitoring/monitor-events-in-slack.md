---
title: 在Slack中监控事件
description: 了解如何通过与Experience Platform App Builder webhook代理集成，在Slack中接收Adobe通知。
feature: Monitoring
role: Developer, Admin
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2026-02-24T00:00:00Z
jira: KT-20339
thumbnail: KT-20339.jpeg
source-git-commit: 268df348b1151394acde869ba4814b658a27e8ff
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 0%

---


# 监控Slack中的Experience Platform事件

了解如何通过与Experience Platform App Builder webhook代理集成，在Slack中接收Adobe通知。 数据工程师和管理员可能希望在Slack中接收来自Adobe Experience Platform的主动通知，以监控其Platform实施的运行状况。 本教程概述了使用Adobe App Builder将Adobe I/O Events连接到Slack的架构和实施步骤。


>[!VIDEO](https://video.tv.adobe.com/v/3480183?learn=on)

## 为什么是webhook代理？

由于验证过程中的协议不匹配，无法将Adobe I/O Events直接连接到Slack传入Webhook。

* **挑战**：当您使用Adobe I/O Events注册webhook时，Adobe会向您的端点发送“挑战”请求（`GET`或`POST`）。 您的端点必须成功处理此质询并返回特定值以确认所有权。

* **限制**： Slack的传入Webhook仅用于摄取JSON负载进行消息传送。 它们没有逻辑来识别或响应Adobe的验证质询握手。

* **解决方案**：使用Adobe App Builder部署中间webhook代理。 此代理位于Adobe和Slack之间，用于：
   1. 截获来自Adobe的请求并响应验证挑战。
   1. 将有效负载格式化为与Slack兼容的消息，并将其转发到Slack。

* **传递方法**：运行时操作。  运行时操作随Adobe App Builder一起打包。 使用运行时操作（非Web操作）作为事件处理程序时，Adobe I/O Events会自动处理签名验证和质询响应。 推荐使用运行时操作，因为此方法需要较少的代码并提供内置安全性。

## 架构概述

### 什么是Adobe Developer Console？

Adobe Developer Console是管理Adobe项目、API和凭据的中心门户。 您可以在此处创建项目、配置身份验证和注册Webhook。

### 什么是App Builder？

Adobe App Builder是一个完整的框架，它允许企业开发人员构建云原生应用程序。

* **配置**：默认情况下不启用App Builder；必须作为功能为您的组织配置它。 确保您的组织具有&#x200B;**[!DNL App Builder]**&#x200B;权利。

* **项目模板**： App Builder项目是专门使用&#x200B;**[!UICONTROL 中的]** App Builder[!DNL Developer Console]模板创建的(来自模板[!UICONTROL  > ]App Builder[!UICONTROL 的]项目)。 模板会自动设置必要的工作区和运行时环境。

* **App Builder快速入门指南**：请参阅文档[以配置并创建您的第一个项目（从模板](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target=_blank}）。

### 什么是Adobe I/O Runtime？

Adobe I/O Runtime是支持App Builder的无服务器平台。 它允许开发人员部署响应HTTP请求运行的代码(Functions-as-a-Service)，而无需管理服务器基础架构。

在此实现中，我们使用&#x200B;**操作**。 Action是在Adobe I/O Runtime上运行的无状态函数（在Node.js中编写）。 我们的操作将用作Adobe I/O Events与之通信的公共HTTP端点。

有关详细信息，请参阅[Adobe I/O Runtime文档](https://developer.adobe.com/runtime/){target=_blank}。

## 实施指南

### 先决条件

开始之前，请确保您满足以下条件：

* **Adobe Developer Console访问权限**：您必须有权访问已启用App Builder的组织中的系统管理员或[开发人员角色](../admin/add-developers.md)。

  >[!TIP]
  > 要验证App Builder配置，请登录[Adobe Developer Console](https://developer.adobe.com/console/){target=_blank}，确保您处于所需的组织中，选择&#x200B;**[!UICONTROL 从模板创建项目]**，并验证App Builder模板是否可用。 如果不是，请查看App Builder常见问题解答部分&quot;[如何获取App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/faq#how-to-get-app-builder){target=_blank}&quot;


* **Node.js和npm**：此项目需要Node.js，其中包括NPM （节点包管理器）。 NPM用于安装Adobe CLI和管理项目依赖项。

   * [下载Node.js（建议使用LTS版本）](https://nodejs.org/){target=_blank}
   * [npm快速入门指南](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){target=_blank} — 有关如何验证安装的指南。

* **`aio CLI`**：已通过终端安装： `npm install -g @adobe/aio-cli`
* **Slack应用程序配置**：您需要在工作区中设置Slack应用程序，并激活&#x200B;**传入Webhook**。

   * [创建Slack应用程序](https://api.slack.com/apps){target=_blank}
   * [Slack传入Webhook指南](https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks/){target=_blank} — 按照本指南创建应用程序并生成Webhook URL（以`https://hooks.slack.com/`开头……）。

### 步骤1：在Adobe Developer Console中创建项目

首先，在Adobe Developer Console中使用App Builder模板创建一个项目：

1. 登录[Adobe Developer Console](https://developer.adobe.com/console)
1. 选择&#x200B;**[!UICONTROL 从模板创建项目]**
1. 选择App Builder模板
1. 输入项目标题，例如`Slack webhook integration`
1. 选择&#x200B;**[!UICONTROL 保存]**

### 步骤2：初始化运行时环境

在终端中运行以下命令以创建项目结构：

#### 登录`aio`

```
aio login
```

#### 初始化新的App Builder项目

```
aio app init slack-webhook-proxy
```

1. 选择您的组织并按&#x200B;**Enter**
1. 选择您在上一步中创建的项目（例如，`Slack webhook integration`），然后按&#x200B;**Enter**
1. 选择&#x200B;**[!UICONTROL 仅我的组织支持的模板]**&#x200B;选项
1. 按&#x200B;**Enter**&#x200B;跳过示例部分
1. 出现提示时，请确保选择了以下组件（应填充圆圈），然后按&#x200B;**Enter**：
   1. **[!UICONTROL 操作：部署运行时操作]**
   1. **[!UICONTROL 事件：发布到Adobe I/O Events]**
   1. **[!UICONTROL Web Assets：部署到托管的静态资源]**
1. 使用“向上”和“向下”箭头，导航传入列表并选择&#x200B;**[!UICONTROL Adobe Experience Platform：实时客户个人资料]**，然后按&#x200B;**Enter**
1. **[!UICONTROL 通用]**&#x200B;操作是自动生成的
1. 为UI选择&#x200B;**[!UICONTROL 纯HTML/JS]**，然后按&#x200B;**Enter**
1. 将&#x200B;**[!UICONTROL generic]**&#x200B;保留为示例操作，以展示如何访问外部API名称，并按&#x200B;**Enter**
1. 保留&#x200B;**[!UICONTROL publish-events]**&#x200B;作为示例操作名称，以使用云事件格式创建消息，然后按&#x200B;**Enter**

应完成应用程序初始化。

#### 导航到项目目录

```
cd slack-webhook-proxy
```

#### 添加Web操作

```
aio app add action
```

1. 选择&#x200B;**[!UICONTROL 仅我的组织支持的模板]**，然后按&#x200B;**Enter**
2. 在呈现的表中查看&#x200B;**[!UICONTROL publish-events]**&#x200B;操作；按&#x200B;**共享空间**&#x200B;选择该操作。 如果名称旁边的圆圈已填充（如视频教程中所示），请按&#x200B;**Enter**
3. 命名操作`webhook-proxy`

### 步骤3：代理操作代码

在IDE或文本编辑器中，使用以下代码创建/修改文件`actions/webhook-proxy/index.js`。 此实施会将事件转发到Slack。 使用运行时操作注册时，签名验证和质询处理是自动进行的。

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("webhook-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### 步骤4：配置操作

`app.config.yaml`中的操作配置是关键的。 使用Web：否，创建可在Developer Console中注册为运行时操作的非Web操作。

```yaml
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

#### 为什么`web: no?`

当您使用非Web操作并通过Developer Console中的“运行时操作”选项注册它时，Adobe I/O Events会自动执行以下操作：

* 处理质询验证（`GET`和`POST`）
* 在调用操作之前验证数字签名
* 将签名验证器操作链接到操作之前

这意味着您的代码只需要处理业务逻辑(转发到Slack)。

### 步骤5：环境变量

为了安全地管理凭据，我们使用环境变量。 在项目的根目录中创建/修改`.env`文件以添加Slack webhook URL。 如果未看到`.env`文件，请确保在系统上显示隐藏的文件：

```
# ... other .env file content ...
 
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### 步骤 6：部署

设置环境变量后，部署操作。 在终端中运行此命令时，请确保位于项目的根目录下，即`slack-webhook-proxy`。

```
aio app deploy
```

您的操作将部署到Adobe I/O Runtime，并且可在Developer Console中注册操作。

### 步骤7：最终注册(Adobe Developer Console)

现在您的操作已部署，请将其注册为Adobe事件的目标。

1. 导航到[Adobe Developer Console](https://developer.adobe.com/console){target=_blank}并打开您的App Builder项目。
1. 选择您的&#x200B;**[!UICONTROL Workspace]**
1. 选择&#x200B;**[!UICONTROL 添加服务]**&#x200B;并选择&#x200B;**[!UICONTROL 事件]**。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;作为产品。
1. 选择&#x200B;**[!UICONTROL 平台通知]**&#x200B;作为事件类型。
1. 选择您希望在Slack中收到通知的特定事件（或所有事件），然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 选择或[创建您的OAuth凭据](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/api/platform-api-authentication){target=_blank}。
1. 配置&#x200B;**[!UICONTROL 事件注册详细信息]**：
   1. **[!UICONTROL 注册名称]**：为注册提供一个描述性名称。
   1. **[!UICONTROL 注册描述]**：确保此描述是显式的，以便其他参与者能够了解其用途。
   1. 选择&#x200B;**[!UICONTROL 下一步]**
   1. **[!UICONTROL 交付方法]**：选择&#x200B;**[!UICONTROL 运行时操作]**（不是“Webhook”）。
   1. **[!UICONTROL 运行时操作]**：从下拉列表中选择`webhook-proxy`（如果未看到该页面，请刷新该页面）。
1. 选择&#x200B;**[!UICONTROL 保存配置的事件]**。


### 步骤8：使用示例事件进行验证

您可以通过单击任何已配置事件旁边的“发送示例事件”按钮，端到端地测试整个流。

示例事件通过您在创建Slack应用程序并创建webhook时配置的渠道发送；您应该看到类似以下的内容：

![Slack中的监视事件示例](../assets/slack-monitor.png)

恭喜，您已成功地将Slack与Experience Platform活动集成！

### 常见问题

以下是配置代理时可能会遇到的一些问题以及解决这些问题的一些可能方法。

* **无法查看IMS组织**：如果在运行`aio app init`时未看到您的IMS组织列表，请尝试以下操作。 在终端中运行`aio logout`，在默认Web浏览器上注销Experience Cloud，然后再次运行`aio login`。
* **操作未出现在下拉列表**&#x200B;中：确保在`web: no`中设置了`app.config.yaml`。 运行时操作下拉列表中只显示非Web操作。 部署后刷新“Developer Console”页面。
* **签名验证失败**：如果在激活日志中看到此信息，则表示Adobe的内置验证器拒绝了请求。 对于合法的Adobe事件，不应发生这种情况。 检查事件注册是否正确配置。
* **Slack未接收消息**：检查`SLACK_WEBHOOK_URL`文件中是否正确设置了`.env`，以及Slack应用是否启用了传入Webhook。
* **操作超时**：运行时操作的超时为60秒。 如果您的操作需要较长时间，请考虑改用日志记录方法。