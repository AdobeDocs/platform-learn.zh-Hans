---
title: 安装和配置Kafka Connect和Adobe Experience Platform接收器连接器
description: 安装和配置Kafka Connect和Adobe Experience Platform接收器连接器
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# 2.6.4安装和配置Kafka Connect和Adobe Experience Platform接收器连接器

## 2.6.4.1下载Adobe Experience Platform接收器连接器

转到[https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases)并下载Adobe Experience Platform接收器连接器的最新正式版本。

![Kafka](./images/kc1.png)

将下载文件&#x200B;**streaming-connect-sink-0.0.14-java-11.jar**&#x200B;放在桌面上。

![Kafka](./images/kc2.png)

## 2.6.4.2配置Kafka Connect

转到桌面上名为&#x200B;**Kafka_AEP**&#x200B;的文件夹，然后导航到文件夹`kafka_2.13-3.1.0/config`。
在该文件夹中，使用任意文本编辑器打开文件**connect-distributed.properties**。

![Kafka](./images/kc3a.png)

在文本编辑器中，转到第34和35行并确保将字段`key.converter.schemas.enable`和`value.converter.schemas.enable`设置为`false`

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

保存对此文件所做的更改。

![Kafka](./images/kc3.png)

接下来，返回文件夹`kafka_2.13-3.1.0`并手动创建新文件夹并将其命名为`connectors`。

![Kafka](./images/kc4.png)

右键单击该文件夹，然后单击&#x200B;**在文件夹**&#x200B;新建终端。

![Kafka](./images/kc5.png)

你会看到这个。 输入命令`pwd`以检索该文件夹的完整路径。 选择完整路径并将其复制到剪贴板。

![Kafka](./images/kc6.png)

返回文本编辑器，转到文件&#x200B;**connect-distributed.properties**，然后向下滚动到最后一行（屏幕快照中的第86行）。 您应该取消注释以`# plugin.path=`开头的行，并且应该将完整路径粘贴到名为`connectors`的文件夹。 结果应类似于下面这样：

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.1.0/connectors`

保存对文件&#x200B;**connect-distributed.properties**&#x200B;所做的更改并关闭文本编辑器。

![Kafka](./images/kc7.png)

接下来，将下载到名为`connectors`的文件夹中的Adobe Experience Platform接收器连接器的最新正式版本复制。 您之前下载的文件名为&#x200B;**streaming-connect-sink-0.0.14-java-11.jar**，只需将其移到`connectors`文件夹中即可。

![Kafka](./images/kc8.png)

接下来，在&#x200B;**kafka_2.13-3.1.0**&#x200B;文件夹级别打开一个新的“终端”窗口。 右键单击该文件夹，然后单击&#x200B;**在文件夹**&#x200B;新建终端。

在“终端”窗口中，粘贴以下命令： `bin/connect-distributed.sh config/connect-distributed.properties`并单击&#x200B;**Enter**。 此命令将启动Kafka Connect并加载Adobe Experience Platform接收器连接器的库。

![Kafka](./images/kc9.png)

几秒钟后，您将会看到如下内容：

![Kafka](./images/kc10.png)

## 2.6.4.3使用Postman创建Adobe Experience Platform接收器连接器

您现在可以使用Postman与Kafka Connect交互。 为此，请下载[此Postman收藏集](./../../../assets/postman/postman_kafka.zip)并将其解压缩到桌面上的本地计算机。 然后，您将拥有一个名为`Kafka_AEP.postman_collection.json`的文件。

![Kafka](./images/kc11a.png)

您需要在Postman中导入此文件。 为此，请打开Postman，单击&#x200B;**导入**，将文件`Kafka_AEP.postman_collection.json`拖放到弹出窗口中，然后单击&#x200B;**导入**。

![Kafka](./images/kc11b.png)

然后，您可以在Postman的左侧菜单中找到此收藏集。 单击第一个请求&#x200B;**可用Kafka Connect连接器**&#x200B;以将其打开。GET

![Kafka](./images/kc11c.png)

你会看到这个。 单击蓝色的&#x200B;**发送**&#x200B;按钮，之后您应该会看到空响应`[]`。 空响应是由于当前未定义Kafka Connect连接器。

![Kafka](./images/kc11.png)

要创建连接器，请单击以打开Kafka集合中的第二个POST **请求“创建AEP接收器连接器”**。 你会看到这个。 在第11行，上面显示“**”aep.endpoint“：”**，您需要将粘贴到练习[15.3](./ex3.md)结束时收到的HTTP API流端点URL。 HTTP API流终结点URL如下所示： `https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`。

![Kafka](./images/kc12a.png)

粘贴后，请求正文应如下所示。 单击蓝色的&#x200B;**发送**&#x200B;按钮以创建您的连接器。 您的连接器创建操作会立即得到响应。

![Kafka](./images/kc12.png)

GET单击第一个请求&#x200B;**可用Kafka Connect连接器**&#x200B;以再次打开它，然后再次单击蓝色的&#x200B;**发送**&#x200B;按钮。 您现在将看到Kafka Connect连接器已创建。

![Kafka](./images/kc13.png)

接下来，打开Kafka集合中的第三个请求，**GET检查Kafka连接连接器状态**。 单击蓝色的&#x200B;**发送**&#x200B;按钮，您将获得如下响应：连接器正在运行。

![Kafka](./images/kc14.png)

## 2.6.4.4生成体验事件

打开一个新的&#x200B;**终端**&#x200B;窗口，方法是右键单击您的文件夹&#x200B;**kafka_2.13-3.1.0**，然后单击&#x200B;**位于文件夹的新终端**。

![Kafka](./images/kafka11.png)

输入以下命令：

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

![Kafka](./images/kc15.png)

你会看到这个。 按下Enter按钮后每行新内容都将导致新消息被发送到主题&#x200B;**aep**。

![Kafka](./images/kc16.png)

您现在可以发送消息，这最终会被Adobe Experience Platform接收器连接器占用，并且会实时将其摄取到Adobe Experience Platform中。

让我们做个小演示来测试一下。

转到[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![DSN](./../../gettingstarted/gettingstarted/images/web8.png)

在&#x200B;**Screens**&#x200B;页面上，单击&#x200B;**运行**。

![DSN](./../../gettingstarted/gettingstarted/images/web2.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个演示，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

单击屏幕左上角的Adobe徽标图标以打开配置文件查看器。

![演示](./../../../modules/datacollection/module1.2/images/pv1.png)

请查看配置文件查看器面板和实时客户配置文件，将&#x200B;**Experience CloudID**&#x200B;作为当前未知客户的主要标识符。

![演示](./../../../modules/datacollection/module1.2/images/pv2.png)

转到“注册/登录”页面。 单击&#x200B;**创建帐户**。

![演示](./../../../modules/datacollection/module1.2/images/pv9.png)

填写您的详细信息，然后单击&#x200B;**注册**，之后您将被重定向到上一页。

![演示](./../../../modules/datacollection/module1.2/images/pv10.png)

打开配置文件查看器面板，然后转到Real-time Customer Profile。 在“配置文件查看器”面板上，您应该会看到所有显示的个人数据，如新添加的电子邮件和电话标识符。

![演示](./../../../modules/datacollection/module1.2/images/pv11.png)

您可能会看到基于过去活动的一些体验事件。

![Kafka](./images/kc19.png)

让我们更改此设置，并将来自Kafka的Callcenter体验活动发送到Adobe Experience Platform。

获取以下示例体验事件有效负载并将其复制到文本编辑器中。

```json
{
  "header": {
    "datasetId": "61fe23fd242870194a6d779c",
    "imsOrgId": "--aepImsOrgID--",
    "source": {
      "name": "Launch"
    },
    "schemaRef": {
      "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
      "contentType": "application/vnd.adobe.xed-full+json;version=1"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    },
    "xdmEntity": {
      "eventType": "callCenterInteractionKafka",
      "_id": "",
      "timestamp": "2022-02-23T09:54:12.232Z",
      "_experienceplatform": {
        "identification": {
          "core": {
            "phoneNumber": ""
          }
        },
        "interactionDetails": {
          "core": {
            "callCenterAgent": {
              "callID": "Support Contact - 3767767",
              "callTopic": "contract",
              "callFeeling": "negative"
            }
          }
        }
      }
    }
  }
}
```

你会看到这个。 您需要手动更新2个字段：

- **_id**：请将其设置为类似`--aepUserLdap--1234`的随机id
- **timestamp**：将时间戳更新为当前日期和时间
- **phoneNumber**：输入刚刚在演示网站上创建的帐户的phoneNumber。 您可以在“配置文件查看器”面板的&#x200B;**标识**&#x200B;下找到它。

您还需要检查并可能更新以下字段：
- **datasetId**：您需要复制数据集演示系统的数据集ID — 呼叫中心的事件数据集(Global v1.1)
- **imsOrgID**：您的IMS组织ID为`--aepImsOrgId--`

>[!NOTE]
>
>字段&#x200B;**_id**&#x200B;对于每次数据引入都必须是唯一的。 如果您生成多个事件，请确保每次将字段&#x200B;**_id**&#x200B;更新为新的唯一值。

![Kafka](./images/kc20.png)

然后，您应该具有如下内容：

![Kafka](./images/kc21.png)

接下来，将完整的体验事件复制到剪贴板。 需要去除JSON有效负载的空格，我们将使用在线工具来去除空格。 转到[http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/)以执行该操作。

![Kafka](./images/kc22.png)

将您的体验事件粘贴到编辑器中，然后单击&#x200B;**删除空格**。

![Kafka](./images/kc22a.png)

接下来，选择所有输出文本并将其复制到剪贴板。

![Kafka](./images/kc23.png)

返回到“终端”窗口。

![Kafka](./images/kc16.png)

将不带空格的新有效负载粘贴到“终端”窗口中，然后单击&#x200B;**Enter**。

![Kafka](./images/kc23a.png)

接下来，返回您的演示网站并刷新页面。 您现在应会在&#x200B;**其他事件**&#x200B;下看到个人资料中的体验事件，如下所示：

![Kafka](./images/kc24.png)

>[!NOTE]
>
>如果希望呼叫中心交互显示在“配置文件查看器”面板上，则需要在[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)上添加以下标签并在项目中过滤，方法是转到选项卡&#x200B;**配置文件查看器**。

![Kafka](./images/kc25.png)

您已完成此练习。

下一步：[摘要和优点](./summary.md)

[返回模块2.6](./aep-apache-kafka.md)

[返回所有模块](../../../overview.md)
