---
title: 安装和配置Kafka群集
description: 安装和配置Kafka群集
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: adffeead-9bcb-4632-9a2c-c6da1c40b7f2
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# 2.6.2安装和配置Kafka群集

## 2.6.2.1下载Apache Kafka

转到[https://kafka.apache.org/downloads](https://kafka.apache.org/downloads)并下载最新发布的版本。 选择最新的二进制版本，在本例中为&#x200B;**Scala 2.13**。

![Kafka](./images/kafka1.png)

然后你被带到镜像站点。 单击建议的链接以下载Kafka。

![Kafka](./images/kafka2.png)

在桌面上创建名为&#x200B;**Kafka_AEP**&#x200B;的文件夹，并将下载的文件放置在该目录中。

![Kafka](./images/kafka3.png)

打开&#x200B;**终端**&#x200B;窗口，方法是：右键单击您的文件夹，然后单击&#x200B;**在文件夹新建终端**。

![Kafka](./images/kafka4.png)

在“终端”窗口中运行此命令以解压缩下载的文件：

`tar -xvf kafka_2.13-3.1.0.tgz`

>[!NOTE]
>
>请验证上述命令是否与您下载的文件的版本匹配。 如果您的版本较新，则需要更新上述命令以匹配该版本。

![Kafka](./images/kafka5.png)

您随后将看到以下内容：

![Kafka](./images/kafka6.png)

解压缩该文件后，您现在拥有如下目录：

![Kafka](./images/kafka7.png)

在该目录中，您将看到以下子目录：

![Kafka](./images/kafka8.png)

返回到“终端”窗口。 输入以下命令：

`cd kafka_2.13-3.1.0`

>[!NOTE]
>
>请验证上述命令是否与您下载的文件的版本匹配。 如果您的版本较新，则需要更新上述命令以匹配该版本。

![Kafka](./images/kafka9.png)

接下来，输入命令`bin/kafka-topics.sh`。

![Kafka](./images/kafka10a.png)

然后，您应该会看到此响应。 这意味着Kafka已正确安装，并且Java工作正常。 (提醒：您需要安装Java 8 JDK或Java 11 JDK才能使此功能正常工作！。 您可以使用命令`java -version`查看已安装的Java版本。)

![Kafka](./images/kafka10.png)

## 2.6.2.2启动Kafka

要启动Kafka，您需要按此顺序启动Kafka Zookeeper和Kafka。

打开&#x200B;**终端**&#x200B;窗口，方法是右键单击您的文件夹&#x200B;**kafka_2.13-3.1.0**，然后单击&#x200B;**在文件夹新建终端**。

![Kafka](./images/kafka11.png)

输入以下命令：

`bin/zookeeper-server-start.sh config/zookeeper.properties`

![Kafka](./images/kafka12.png)

您随后将看到以下内容：

![Kafka](./images/kafka13.png)

在进行这些练习时，请保持此窗口打开！

打开另一个新&#x200B;**终端**&#x200B;窗口，方法是右键单击您的文件夹&#x200B;**kafka_2.13-3.1.0**，然后单击&#x200B;**文件夹上的新终端**。

![Kafka](./images/kafka11.png)

输入以下命令：

`bin/kafka-server-start.sh config/server.properties`

![Kafka](./images/kafka14.png)

您随后将看到以下内容：

![Kafka](./images/kafka15.png)

在进行这些练习时，请保持此窗口打开！

## 2.6.2.3创建Kafka主题

打开&#x200B;**终端**&#x200B;窗口，方法是右键单击您的文件夹&#x200B;**kafka_2.13-3.1.0**，然后单击&#x200B;**在文件夹新建终端**。

![Kafka](./images/kafka11.png)

输入此命令以创建名称为&#x200B;**aeptest**&#x200B;的新Kafka主题。 本主题将用于本练习中的测试。

`bin/kafka-topics.sh --create --topic aeptest --bootstrap-server localhost:9092`

![Kafka](./images/kafka16a.png)

随后您将看到类似的确认：

![Kafka](./images/kafka17a.png)

输入此命令以创建名称为&#x200B;**aep**&#x200B;的新Kafka主题。 您将在下一个练习中配置的Adobe Experience Platform接收器连接器将使用此主题。

`bin/kafka-topics.sh --create --topic aep --bootstrap-server localhost:9092`

![Kafka](./images/kafka16.png)

随后您将看到类似的确认：

![Kafka](./images/kafka17.png)

## 2.6.2.4生成事件

返回创建第一个Kafka主题的“终端”窗口，然后输入以下命令：

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aeptest`

![Kafka](./images/kafka18.png)

你会看到这个。 按下Enter按钮后每行新行都将导致新消息被发送到主题&#x200B;**aeptest**。

![Kafka](./images/kafka19.png)

输入`Hello AEP`并按Enter键。 您的第一个事件现已发送到本地Kafka实例中，并放入主题&#x200B;**aeptest**&#x200B;中。

![Kafka](./images/kafka20.png)

输入`Hello AEP again.`并按Enter键。

输入`AEP Data Collection is the best.`并按Enter键。

您现在已生成主题&#x200B;**aeptest**&#x200B;中的3个事件。 这些事件现在可以由可能需要该数据的应用程序使用。

![Kafka](./images/kafka21.png)

在键盘上，同时单击`Control`和`C`以关闭制作程序。

![Kafka](./images/kafka22.png)

## 2.6.2.4使用事件

在用于生成事件的同一“终端”窗口中，输入以下命令：

`bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic aeptest --from-beginning`

然后，您将看到在上一个练习中为主题&#x200B;**aeptest**&#x200B;生成的所有消息都显示在使用者中。 这是Apache Kafka的工作方式：生产者在管道中创建事件，消费者使用这些事件。

![Kafka](./images/kafka23.png)

在键盘上，同时单击`Control`和`C`以关闭制作程序。

![Kafka](./images/kafka24.png)

在本练习中，您已完成所有基础知识来设置本地Kafka聚类、创建Kafka主题、生成事件和使用事件。

此模块的目的是模拟如果实际组织已经实施Apache Kafka群集，并且希望将数据从其Kafka群集流式传输到Adobe Experience Platform中时将发生的情况。

为了便于这种实现，创建了一个Adobe Experience Platform接收器连接器，可使用Kafka Connect实现该连接器。 您可以在此处找到该Adobe Experience Platform接收器连接器的文档： [https://github.com/adobe/experience-platform-streaming-connect](https://github.com/adobe/experience-platform-streaming-connect)。

在接下来的练习中，您将从自己的本地Kafka群集中实施使用该Adobe Experience Platform接收器连接器所需的一切。

关闭终端窗口。

您已完成此练习。

下一步： [2.6.3在Adobe Experience Platform中配置HTTP API端点](./ex3.md)

[返回模块2.6](./aep-apache-kafka.md)

[返回所有模块](../../../overview.md)
