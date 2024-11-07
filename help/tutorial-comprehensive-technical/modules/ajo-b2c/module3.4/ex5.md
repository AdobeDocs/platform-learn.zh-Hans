---
title: Adobe Journey Optimizer — 商业活动
description: 本节介绍如何使用业务事件功能来执行“有现货的商品”用例
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 1%

---

# 3.4.5创建业务事件历程

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 若要从一个沙盒更改到另一个沙盒，请单击&#x200B;**PRODUCTION Prod (VA7)**，然后从列表中选择该沙盒。 在此示例中，沙盒名为&#x200B;**AEP Enablement FY22**。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.5.1创建业务事件

在左侧菜单中，单击&#x200B;**配置**。 单击&#x200B;**事件**&#x200B;信息卡中的&#x200B;**管理**&#x200B;按钮。

![Journey Optimizer](./images/be1.png)

业务事件是您可以在Journey Optimizer中创建的一种新类型事件。 与您在以前的模块中创建的&#x200B;**单一**&#x200B;事件不同，业务事件不是由客户触发的，而是由组织触发的。 您现在将创建您的商业活动。

单击&#x200B;**创建事件**。

![Journey Optimizer](./images/be2.png)

在“事件创建”窗体中输入以下值：

- **名称**： `--aepUserLdap--ItemBackInStock`。 例如： **vangeluwItemBackInStock**
- **描述**：当产品重新上架时，将触发此事件
- **类型**：在下拉列表中选择&#x200B;**业务**

![Journey Optimizer](./images/evde.png)

对于架构，选择&#x200B;**Demo System - JO业务事件(Global v1.1) v.1**&#x200B;的事件架构。 您现在需要在架构中选择用例所需的字段。

![Journey Optimizer](./images/evdes.png)

执行以下步骤：

单击字段上的&#x200B;**铅笔**&#x200B;图标，其中显示&#x200B;**1字段已选定**。

![Journey Optimizer](./images/23.8-4.png)

选择架构中所有可用的字段，然后单击&#x200B;**确定**。

![Journey Optimizer](./images/23.8-5.png)

对于条件：您需要指定此架构中的哪些记录将触发业务事件。

执行以下步骤：

单击显示&#x200B;**添加条件**&#x200B;的字段上的&#x200B;**铅笔**&#x200B;图标。

![Journey Optimizer](./images/23.8-6.png)

在左侧，展开`--aepTenantId--`对象，展开对象&#x200B;**joBusinessEvents**，并将字段&#x200B;**eventName**&#x200B;拖放到画布上。

![Journey Optimizer](./images/23.8-7.png)

对于字段&#x200B;**eventName**，输入以下值： `--aepUserLdap--ItemBackInStock`。 例如：vangeluwItemBackInStock。
单击**确定**。

![Journey Optimizer](./images/23.8-8.png)

单击&#x200B;**确定**。

![Journey Optimizer](./images/23.8-9.png)

最后，事件创建表单应如下所示。 单击&#x200B;**保存**&#x200B;以保存您的业务事件。

![Journey Optimizer](./images/23.8-10.png)

## 3.4.5.2创建业务事件历程

您现在可以利用此业务活动和历程中的消息。 转到&#x200B;**历程**。 单击&#x200B;**创建历程**。

![Journey Optimizer](./images/bej10.png)

在右侧，您将看到一个表单，其中您需要指定历程名称和描述。 输入以下值：

- **名称**： `--aepUserLdap-- - Item back in stock journey`。 例如：vangeluw — 物料返回库存历程
- **描述**：当某个项目重新上架时，此历程会向感兴趣的访客发送短信。

单击&#x200B;**确定**。

![Journey Optimizer](./images/bej11.png)

在左侧菜单的&#x200B;**事件**&#x200B;下，搜索您的LDAP。 您会找到之前创建的业务事件`--aepUserLdap--ItemBackInStock`。 将此事件拖放到画布上，因为这将是历程的起点。

![Journey Optimizer](./images/bej12.png)

如您所见，**读取区段**&#x200B;活动已自动添加到画布中。 这是因为业务事件仅发送触发程序让历程读取特定区段，然后该历程检索用户档案列表。

单击&#x200B;**读取区段**活动。
**读取区段**&#x200B;配置要求您选择要通知刚刚发生的业务事件的区段。 单击&#x200B;**选择区段**&#x200B;字段。

![Journey Optimizer](./images/bej13.png)

在&#x200B;**选择区段**&#x200B;弹出窗口中，搜索您的LDAP并选择您在[模块2.3 - Real-time CDP — 生成区段并执行名为`--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`的操作](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)中创建的区段。 例如： vangeluw — 关注PROTEUS FITNESS JACKSHIRT。 单击&#x200B;**保存**。

![Journey Optimizer](./images/bej14.png)

接下来，单击&#x200B;**确定**。

![Journey Optimizer](./images/bej15.png)

下一步是拖放我们要在此历程中执行的操作。 选择操作&#x200B;**短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/jop9.png)

将&#x200B;**类别**&#x200B;设置为&#x200B;**营销**&#x200B;并选择允许您发送短信的短信表面。 在这种情况下，要选择的电子邮件表面为&#x200B;**短信**。

![ACOP](./images/journeyactions1x.png)

下一步是创建消息。 为此，请单击&#x200B;**编辑内容**。

![ACOP](./images/journeyactions2x.png)

您现在可以看到消息仪表板，您可以在其中配置短信的文本。 单击&#x200B;**撰写邮件**&#x200B;区域以创建邮件。

![Journey Optimizer](./images/sms3.png)

输入以下文本： `Hi {{profile.person.name.firstName}}, the Proteus Fitness Jackshirt is back in stock at Luma.`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4.png)

单击左上角主题行文本旁边的&#x200B;**箭头**，返回消息仪表板。

![Journey Optimizer](./images/oc79xx.png)

您现在将看到已完成的短信操作。 单击&#x200B;**确定**。

![Journey Optimizer](./images/oc79xxy.png)

您的历程现已准备就绪，可供发布。 单击&#x200B;**Publish**。

![Journey Optimizer](./images/jop13.png)

再次单击&#x200B;**Publish**。

![Journey Optimizer](./images/jop14.png)

您的历程现已发布，您现在可以对其进行测试！

![Journey Optimizer](./images/jop15.png)

## 3.4.5.3测试您的业务事件历程

现在，您将通过Postman针对&#x200B;**Demo System - JO业务活动(Global v1.1) v.1**&#x200B;的事件架构引入新事件来模拟产品重新上架。

在左侧菜单中，单击&#x200B;**源**，然后单击&#x200B;**帐户**&#x200B;选项卡。

![Journey Optimizer](./images/s1.png)

在&#x200B;**帐户**&#x200B;选项卡上，您会找到名为&#x200B;**Journey Optimizer商业事件**&#x200B;的帐户。 单击以将其打开。

![Journey Optimizer](./images/s2.png)

此帐户只有一个数据流，请单击数据流名称将其选定。

![Journey Optimizer](./images/s3.png)

单击右侧菜单中的&#x200B;**复制架构有效负载**。 此选项将整个&#x200B;**curl**&#x200B;命令复制到剪贴板，以根据&#x200B;**演示系统 — JO业务事件(Global v1.1) v.1**&#x200B;的事件架构插入记录。

![Journey Optimizer](./images/s4.png)

将Curl命令粘贴到文本编辑器中

![Journey Optimizer](./images/s5.png)

让我们仔细了解一下此请求，

- POST请求将发送到DCS入口ID
- 该请求引用架构、数据集和组织ID。
- 最后，它包含xdmEntity节点，该节点表示我们要在数据集中创建的数据。

您现在需要替换以下`xdmEntity`行……

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "string",
      "eventName": "string",
      "stockEventId": "string"
    }
  },
  "_id": "/uri-reference",
  "eventType": "advertising.completes",
  "timestamp": "2018-11-12T20:20:39+00:00"
}
```

...通过此行，确保验证字段eventName，它应显示为`--aepUserLdap--ItemBackInStock`，这表示您在业务事件中指定的条件，以触发您的历程。

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "Product Proteus Fitness Jackshirt is back in stock",
      "eventName": "--aepUserLdap--ItemBackInStock",
      "stockEventId": "1"
    }
  },
  "_id": "/uri-reference",
  "eventType": "productBackInStock",
  "timestamp": "2021-04-19T15:25:39+00:00"
}
```

更新的&#x200B;**curl**&#x200B;命令应如下所示：

![Journey Optimizer](./images/s6.png)

选择所有内容并将其复制到剪贴板。

打开Postman。 单击Postman左侧的&#x200B;**导入**。

![Journey Optimizer](./images/23.8-46.png)

选择&#x200B;**原始文本**&#x200B;选项卡，并将之前复制的命令粘贴到此处。 单击&#x200B;**继续**。

![Journey Optimizer](./images/s7.png)

单击&#x200B;**导入**。

![Journey Optimizer](./images/23.8-50.png)

Postman已自动将&#x200B;**curl**&#x200B;命令转换为准备触发的REST命令，只需按&#x200B;**发送**&#x200B;按钮即可请求在数据集内创建该记录。

![Journey Optimizer](./images/23.8-51.png)

验证是否已成功收到您的请求。 在邮递员中查找&#x200B;**200 OK**&#x200B;状态。

![Journey Optimizer](./images/s8.png)

短信可能需要几分钟才能到达您的手机。 如果不包含，则您对Proteus Fitness Jackshirt **的**&#x200B;兴趣区段可能不包含具有正确手机的配置文件。 如果是这样的话，请访问Luma网站，访问&#x200B;**Proteus Fitness Jackshirt**&#x200B;产品并注册，同时确保您提供正确的手机号码。

![Journey Optimizer](./images/s9.png)

您现在已经完成了此练习。

下一步：[摘要和优点](./summary.md)

[返回模块3.4](./journeyoptimizer.md)

[返回所有模块](../../../overview.md)
