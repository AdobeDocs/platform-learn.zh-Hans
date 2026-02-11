---
title: Real-time CDP — 目标SDK
description: Real-time CDP — 目标SDK
kt: 5342
doc-type: tutorial
exl-id: c18acbf5-92f5-4cd2-a5aa-a5e9debb98c9
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 4%

---

# 2.3.6目标SDK

## 设置您的Adobe I/O项目

在本练习中，您将再次使用Adobe I/O来查询Adobe Experience Platform的API。如果尚未配置Adobe I/O项目，请返回模块2.1[中的](../rtcdpb2c-1/ex3.md)练习3，然后按照其中的说明操作。

>[!IMPORTANT]
>
>如果您是Adobe员工，请按照此处的说明使用[PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md)。

## 对Adobe I/O的身份验证

在本练习中，您将再次使用Postman来查询Adobe Experience Platform的API。如果尚未配置Postman应用程序，请返回模块2.1[中的](../rtcdpb2c-1/ex3.md)练习3，然后按照其中的说明操作。

>[!IMPORTANT]
>
>如果您是Adobe员工，请按照此处的说明使用[PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md)。

## 定义端点和格式

在本练习中，您将需要端点来配置，以便在受众符合条件时，资格事件可以流式传输到该端点。 在本练习中，您将使用[https://pipedream.com/requestbin](https://pipedream.com/requestbin)的示例终结点。 转到[https://pipedream.com/requestbin](https://pipedream.com/requestbin)，创建一个帐户，然后创建一个工作区。 创建工作区后，您将看到类似以下的内容。

单击&#x200B;**复制**&#x200B;复制URL。 您需要在下一个练习中指定此URL。 此示例中的URL是`https://eodts05snjmjz67.m.pipedream.net`。

![数据获取](./images/webhook1.png)

至于格式，我们将使用标准模板，该模板将流传输受众资格或取消资格与客户标识符等元数据。 可以自定义模板以满足特定端点的期望，但在本练习中，我们将重用标准模板，这将产生类似于这样的有效负荷，并将其流式传输到端点。

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## 创建服务器和模板配置

在Adobe Experience Platform中创建自己的目标的第一步是使用Postman创建服务器和模板配置。

为此，请打开您的Postman应用程序并转到&#x200B;**目标创作API**、**目标服务器和模板**，然后单击以打开请求&#x200B;**POST — 创建目标服务器配置**。

>[!NOTE]
>
>如果您没有该Postman收藏集，请返回模块2.1[中的](../rtcdpb2c-1/ex3.md)练习3，并按照其中的说明设置Postman和提供的Postman收藏集。

你会看到这个。 在&#x200B;**Headers**&#x200B;下，您需要手动更新键&#x200B;**x-sandbox-name**&#x200B;的值并将其设置为`--aepSandboxName--`。 选择值&#x200B;**{{SANDBOX_NAME}}**。

![数据获取](./images/sdkpm1.png)

用`--aepSandboxName--`替换它。

![数据获取](./images/sdkpm2.png)

接下来，转到&#x200B;**正文**。 选择占位符&#x200B;**{{body}}**。

![数据获取](./images/sdkpm3.png)

您现在需要使用以下代码替换占位符&#x200B;**{{body}}**：

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

粘贴上述代码后，您需要手动更新字段&#x200B;**urlBasedDestination.url.value**，并且需要将其设置为您在上一步中创建的webhook的URL，在本例中为`https://eodts05snjmjz67.m.pipedream.net`。

![数据获取](./images/sdkpm4.png)

更新字段&#x200B;**urlBasedDestination.url.value**&#x200B;后，它应该如下所示。 单击&#x200B;**发送**。

![数据获取](./images/sdkpm5.png)

>[!NOTE]
>
>请不要忘记，在向Adobe I/O发送请求之前，您需要具有有效的`access_token`。 要获得有效的`access_token`，请运行请求&#x200B;**Adobe IO - OAuth**&#x200B;集合中的&#x200B;**POST — 获取访问令牌**。

单击&#x200B;**发送**&#x200B;后，将创建您的服务器模板，作为响应的一部分，您将看到名为&#x200B;**instanceId**&#x200B;的字段。 请记下它，因为您将在下一步中需要它。 在此示例中，**instanceId**为
`52482c90-8a1e-42fc-b729-7f0252e5cebd`。

![数据获取](./images/sdkpm6.png)

## 创建目标配置

在Postman中的&#x200B;**目标创作API**&#x200B;下，转到&#x200B;**目标配置**&#x200B;并单击以打开请求&#x200B;**POST — 创建目标配置**。 你会看到这个。 在&#x200B;**Headers**&#x200B;下，您需要手动更新键&#x200B;**x-sandbox-name**&#x200B;的值并将其设置为`--aepSandboxName--`。 选择值&#x200B;**{{SANDBOX_NAME}}**&#x200B;并将其替换为`--aepSandboxName--`。

![数据获取](./images/sdkpm7.png)

接下来，转到&#x200B;**正文**。 选择占位符&#x200B;**{{body}}**。

![数据获取](./images/sdkpm9.png)

您现在需要使用以下代码替换占位符&#x200B;**{{body}}**：

```json
{
    "name": "--aepUserLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![数据获取](./images/sdkpm11.png)

粘贴上述代码后，您需要手动更新&#x200B;**destinationDelivery字段。 destinationServerId**，并且需要将其设置为在上一步中创建的目标服务器模板的&#x200B;**instanceId**，在本例中为`52482c90-8a1e-42fc-b729-7f0252e5cebd`。 接下来，单击&#x200B;**发送**。

![数据获取](./images/sdkpm10.png)

您随后将看到此响应。

![数据获取](./images/sdkpm12.png)

现在，您的目标已在Adobe Experience Platform中创建。 我们到那里去检查一下。

转到[Adobe Experience Platform](https://experience.adobe.com/platform)。 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择适当的[!UICONTROL 沙盒]后，您将看到屏幕更改，现在您已经进入专用的[!UICONTROL 沙盒]。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

在左侧菜单中，转到&#x200B;**目标**，单击&#x200B;**目录**，然后向下滚动到类别&#x200B;**流**。 您现在将看到您的目标在那里可用。

![数据获取](./images/destsdk1.png)

## 将受众链接到目标

在&#x200B;**目标** > **目录**&#x200B;中，单击目标上的&#x200B;**设置**&#x200B;以开始将受众添加到新目标。

![数据获取](./images/destsdk2.png)

为&#x200B;**持有者令牌**&#x200B;输入一个随机值，如&#x200B;**1234**。 单击&#x200B;**连接到目标**。

![数据获取](./images/destsdk3.png)

你会看到这个。 作为目标的名称，请使用`--aepUserLdap-- - Webhook`。 选择所选的端点，在此示例中为&#x200B;**EU**。 单击&#x200B;**下一步**。

![数据获取](./images/destsdk4.png)

您可以选择数据治理策略。 单击&#x200B;**下一步**。

![数据获取](./images/destsdk5.png)

选择您之前创建的名为`--aepUserLdap-- - Interest in Galaxy S24`的受众。 单击&#x200B;**下一步**。

![数据获取](./images/destsdk6.png)

你会看到这个。 确保将&#x200B;**SOURCE FIELD** `--aepTenantId--.identification.core.ecid`映射到字段`Identity: ecid`。 单击&#x200B;**下一步**。

![数据获取](./images/destsdk7.png)

单击&#x200B;**完成**。

![数据获取](./images/destsdk8.png)

您的目标现已上线，新的受众资格将立即流式传输到您的自定义webhook。

![数据获取](./images/destsdk9.png)

## 测试受众激活

转到[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登录后，您将看到此内容。 单击网站项目上的3个点&#x200B;**...**，然后单击&#x200B;**运行**&#x200B;以将其打开。

![DSN](./../../datacollection/dc1.1/images/web8.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../../../getting-started/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](../../../getting-started/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../../../getting-started/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../../../getting-started/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个练习，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](../../../getting-started/gettingstarted/images/web7.png)

在本例中，您希望对查看特定产品的特定客户做出响应。
从**Citi Signal**&#x200B;主页，转到&#x200B;**手机和设备**，然后单击产品&#x200B;**Galaxy S24**。

![数据获取](./images/homegalaxy.png)

Galaxy S24的产品页面现已查看，因此您的受众将在随后几分钟内符合您的个人资料的资格。

![数据获取](./images/homegalaxy1.png)

当您打开配置文件查看器并转到&#x200B;**受众**&#x200B;时，您将看到受众符合条件。

![数据获取](./images/homegalaxydsdk.png)

现在，返回到[https://eodts05snjmjz67.m.pipedream.net](https://eodts05snjmjz67.m.pipedream.net)上打开的webhook，您应会看到一个新的传入请求，该请求源自Adobe Experience Platform并且包含受众资格事件。

![数据获取](./images/destsdk10.png)

## 后续步骤

返回[Real-time CDP — 构建受众并执行操作](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
