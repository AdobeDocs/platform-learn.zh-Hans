---
title: API基本简介
description: 应用程序编程接口简介
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User, Data Engineer, Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '2086'
ht-degree: 0%

---

# API 101 - API的基本简介

API代表应用程序编程接口。 它只是它所说的意思 — 程序之间有接口，这些接口允许这些程序进行通信。 当程序员开发软件应用程序时，他们往往需要自己的软件来与其他软件或硬件进行通信。 API定义这些通信和交互的内容、方式、时间、地点和原因。

API是解决软件业务挑战的一种方法。 在大多数企业中，这是一种协作努力。 通过共享对关键术语、概念和步骤的理解，协作始终会更加轻松。

如果您考虑单击网页中的链接，那么当您单击该链接时，浏览器会使用许多API。 浏览器会识别点击，为您要访问的页面发出请求，通过Internet检索该页面，然后将其显示在屏幕上。 中间有许多较小的步骤，但您的浏览器是一种软件，它与各种API进行通信和交互，只是为了向您显示网页。 在本文中，我们将重点介绍使用或讨论API时的重要术语、概念和步骤。

在阅读本文之前，您应该对这些基本术语、概念和步骤有清楚的了解。 API文档非常详细，关于使用API解决特定用例的讨论可能非常详细。 通过清晰的基础知识和共同理解，浏览文档和讨论API会更轻松、更高效地工作。

>[!NOTE]
>
> 虽然有许多API，但重点将放在Web和浏览器API上：基本上，当一个软件应用程序通过Internet与另一个软件应用程序交互时。

## API术语和概念

一个词或短语是什么意思？我如何简单而轻松地思考它？ 在API中，“应用程序”部分是指软件应用程序或程序。 “编程接口”部分是指应用程序出于特定目的如何以及在何处与另一个应用程序交互。 在我们的网页示例中，当您单击某个链接时，浏览器会向服务器发送有关该网页的请求。

![带有目标URL的超链接图像](../assets/api101-link-destination.png)

在此屏幕快照中，鼠标光标悬停在Adobe Experience Platform链接上。 底部是Web浏览器状态栏，其中显示了浏览器将获取的页面的“地址”。 换言之，单击Adobe Experience Platform链接可告知浏览器“为我获取该页面，以便我能够在屏幕上看到它”。

单击链接时，浏览器会向服务器发出获取页面的请求。 这是`GET`请求，通常用于Web API的请求方法之一。 浏览器需要满足一个请求的是页面“地址” — 它在Web上的什么位置？

### URL的各个部分

![带有URL的浏览器地址栏](../assets/api101-address-bar.png)

大多数浏览器都有一个“地址栏”，显示某个网页的部分或全部“地址”。 当浏览器“获取”我们单击的链接的页面时，它会在地址栏中显示该页面的“地址”。 那么，网页的“地址”是什么呢？

上面的`https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`是Web上某个页面的地址，它称为URL或统一资源定位器。 URL可以引用此类页面、图像文件、视频或其他文件类型。

URL的![部分](../assets/api101-url-parts.jpg)

此地址（即URL）包含与Web和浏览器API非常相关的特定部分。

**方案**

上述`scheme`也称为具有Web API的`protocol`，它通常为`http`或`https`。 HTTP或HyperText传输协议是将网页等资源从Web服务器传输到Web浏览器的方式。 HTTPS是安全版本，其中传输在Internet上进行，使用旨在防止对正在传输的资源造成干扰的安全版本。 通过HTTPS查看页面时，经常会在浏览器地址栏中看到一个小锁图标。

对于Web API，这些资源的传输通过HTTP请求进行，换句话说，就是通过HTTP请求。

**主机和域**

`business.adobe.com`是所请求资源的主机。 单击我们的示例链接时，浏览器将使用URL的此部分来查找托管页面的服务器。 它并不总是与Web服务器完全相同，但在基本层面上，我们可以将其视为浏览器将获取我们请求的页面的服务器。

域名是域名系统（通常称为DNS）的一部分。 大多数人将`adobe.com`或`example.com`视为“域名”，但存在与API相关的部分。 `www.adobe.com`和`business.adobe.com`可以称为域名，但`www.`和`business.`部分称为子域。 API经常与包含子域（如`api.example.com`或`sub.www.example.com`）的URL交互。

经常会看到术语&#x200B;_主机_&#x200B;是指包括任何子域（如`business.adobe.com`）的完整域名。 在引用不带子域（如`adobe.com`）的主机时，经常会看到术语&#x200B;_域_&#x200B;或&#x200B;_域名_。 记住主机的每个部分和变体的特定术语在此处并不重要。 但是，了解这些术语的常用之处很重要，这样您就可以阐明业务和讨论的任何相关细节。

**Origin**

Origin是另一个要注意的术语，它与URL的部分密切相关。 在基本级别上，原点大致为`scheme`加`host`加`domain`，如`https://business.adobe.com`。 不同的值通常表示不同的源，如`https://business.adobe.com`和`http://business.adobe.com`不是同一源，因为它们具有不同的方案。 由于不同的子域，`https://www.adobe.com`和`https://business.adobe.com`在许多使用中也不是同一来源。

**路径**

上述URL示例中的最后一位是资源的`path`，即我们示例中的页面。 `/products/experience-platform/`部分通常表示Web服务器上的文件夹或目录。 就像我们在计算机上为文档和照片提供了文件夹或目录一样，我们在Web服务器上也提供了用于整理内容的文件夹。 最后，`/adobe-experience-platform.html`部分是文件的名称 — 网页。

URL还有其他更详细的部分，将在本系列的下一部分重点介绍。

### 第三方API

Web API有时称为第三方API。 这就像交易中的当事人一样。 在我们的链接示例中，您（或者更具体地说，您的浏览器）是页面请求中的第一方。 Web服务器是第二方。 那么第三个呢？

网页通常包含来自其他主机或来源的内容或资源。 在这些情况下，当您的浏览器开始显示页面时，它会向托管这些资源的其他主机或“第三方”发出另一组请求。 这非常常见，尤其是对于视频或图像等媒体内容，以及在查看或使用数据时需要更新的数据。 获取当天的当前时间、当前天气或特定人员的个性化欢迎消息都是第三方API可以在正确时间提供正确资源的示例。 这些请求通常来自这些第三方API。

## Web API的常见用法

除了时间、天气或个性化内容之外，Web API还有许多用途。 twitter、TikTok、Facebook、LinkedIn、Snapchat、Pinterest等社交媒体平台具有多种程序员可以在其应用程序中使用的API。 当然，Adobe还有[多种程序员使用的API](https://developer.adobe.com/apis)，以便他们的软件可以与Adobe产品和服务交互。 软件产品和服务通过这些API访问其他软件产品和服务。

## 示例API

浏览器API允许程序员直接与浏览器的功能交互。 电池API允许软件检查设备的电池状态，以便在需要时提醒您。 剪贴板API允许软件与设备的剪贴板一起复制或粘贴。 全屏API让软件可以选择将视图展开到设备的全屏，如YouTube。

Adobe Experience Platform数据访问API是一个Web API，它允许程序员从Adobe Experience Platform访问和下载数据集文件，以便他们可以在自己的程序中使用客户配置文件数据。 对于这样的API来说，作为软件自动化流程的一部分是很常见的，在软件自动化流程中，经过编程后，可使用多个API组合来执行一系列步骤。 与手动执行这些相同步骤相比，这通常可显着节省成本。

## API端点

当程序员在程序中“使用”浏览器或Web API时，他们通常会请求发送或接收资源，例如我们的示例浏览器请求网页。 API文档通常会列出这些请求的“端点”，例如： `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`。 这是程序员将用于获取数据集文件的Platform数据访问API的特定模式或“端点”。

由这些大括号括起来的`{dataSetFileId}`表示程序员在请求中需要发送的值。 因此，实际API请求中的URL类似于`https://platform.adobe.io/data/foundation/export/files/xyz123brb`，其中`xyz123brb`必须是程序员希望接收的数据集文件的有效ID。

换言之，就像浏览器通过特定URL获取页面、API请求从特定端点获取资源或向特定端点发送资源一样，此数据集示例如下。

## HTTP请求方法

此时，应当清楚的是，Web API会请求网页或数据集等资源。 与大多数软件概念一样，这些HTTP请求遵循可重复的模式。 从软件应用程序向另一个软件应用程序发送请求，该应用程序评估该请求，然后作出响应：浏览器从Web服务器请求一个页面，并使用页面内容作出响应。

从请求到响应的整个过程涉及许多更小且非常详细的步骤，但请求方法却非常简单。 请求方法定义所请求的操作。

**`GET`**

在请求提供资源的响应（如我们的网页和数据集示例）时使用`GET`请求方法。 当我们单击浏览器中的链接或点按移动设备上的链接时，我们正在后台发出`GET`请求。

**`POST`**

`POST`方法随请求发送数据。 “请求”发送数据听起来可能很奇怪，但想法是，发出API请求需要端点（接收软件）接受请求，如果是`POST`，还要接受正在发送的数据。 发送的数据通常会像数据库或文件一样写入数据存储，以便进行保存。

**`PUT`**

`PUT`请求方法类似于`POST`，因为它发送数据，但如果正在发送的数据在端点已存在，则`PUT`将通过替换现有数据来更新现有数据。 `POST`不更新，只是发送，因此多个`POST`请求可以创建已发送数据的多个记录，而不是更新任何现有记录。

**`PATCH`**

`PATCH`请求方法用于发送更新部分现有记录的数据，例如，当我们通过更新帐户配置文件来更改地址时。 通过`POST`请求可以创建其他配置文件，通过`PUT`，可以替换现有配置文件，但通过使用`PATCH`方法，我们只需更新现有记录的相关部分，如我们的地址。

**`DELETE`**

`DELETE`请求方法会删除在请求中指定的资源，例如，如果我们单击链接以完全删除帐户配置文件。

还有其他几种方法，但以下是使用API时最常用方法的列表。

### 请求示例

现在，您已了解与API相关的基本术语、概念和步骤，我们可以查看实际的API请求示例。

浏览器示例中的页面的URL为`https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`。 单击Adobe Experience Platform链接后，浏览器会对此页面发出`GET`请求。 由于我们有浏览器来为我们工作，因此我们只需单击，但如果程序员希望在软件应用程序中发生该请求，他们必须提供成功完成API请求所需的所有详细信息。

下面是代码中可能出现的形式：

```js
fetch(
  "https://business.adobe.com/products/experience-platform/adobe-experience-platform.html",
  {
    headers: {
      accept:
        "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "accept-language": "en-US,en;q=0.9",
      "sec-ch-ua":
        '" Not A;Brand";v="99", "Chromium";v="101", "Microsoft Edge";v="101"',
      "sec-fetch-dest": "document",
      "sec-fetch-mode": "navigate",
      "sec-fetch-site": "none",
      "sec-fetch-user": "?1",
      "upgrade-insecure-requests": "1",
    },
    referrerPolicy: "strict-origin-when-cross-origin",
    body: null,
    method: "GET",
    mode: "cors",
    credentials: "include",
  }
);
```

在上面的代码中，您可以看到浏览器正在请求的`URL`，在底部附近向下是`method: "GET"`请求方法。 其他几行代码也是请求的一部分，但超出了本文的范围。


*[API]：应用程序编程接口
*[URL]：统一资源定位器
*[HTTP]：超文本传输协议
*[DNS]：域名系统
