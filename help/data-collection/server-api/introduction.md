---
title: API基本简介
description: 应用程序编程接口简介
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User,Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 0%

---

# API 101 - API基本简介

API代表应用程序编程接口。 它的意思就是它所说的 — 程序之间有接口，这些接口允许这些程序进行通信。 当程序员开发软件应用程序时，他们往往需要自己的软件来与其他软件或硬件进行通信。 API可定义这些通信和交互的内容、方式、时间、位置和原因。

API是用软件解决业务难题的一种方法。 在大多数企业，这是一种合作努力。 通过对关键术语、概念和步骤的共同了解，协作总是会更容易。

如果您想要单击网页中的链接，则在单击该链接时，浏览器会使用很多API。 浏览器可识别该点击，对您要访问的页面提出请求，在Internet上检索该页面，然后将其显示在您的屏幕上。 中间有许多较小的步骤，但您的浏览器是与各种API进行通信和交互的软件，只是用来向您显示网页。 在本文中，我们将重点介绍在使用或讨论API时非常重要的术语、概念和步骤。

在本文的末尾，您应该对这些基本术语、概念和步骤有清晰的了解。 API文档内容非常丰富，有关使用API解决特定用例的讨论会会非常详细。 通过清晰的基础知识和分享的了解，浏览文档并讨论API更简单、更高效。

>[!NOTE]
>
> 尽管有许多API，但这里重点介绍的将是Web API和浏览器API:基本上，当一个软件应用程序通过互联网与另一个软件应用程序进行交互时。

## API术语和概念

一个词或短语是什么意思？我如何能简单而轻松地去想它？ 在API中，“应用程序”部分是指软件应用程序或程序。 “编程接口”部分是指应用程序为特定目的与其他应用程序交互的方式和位置。 在我们的网页示例中，当您单击某个链接时，浏览器会向服务器发送网页请求。

![包含目标URL的超链接图像](../assets/api101-link-destination.png)

在此屏幕截图中，鼠标光标悬停在Adobe Experience Platform链接上。 底部是Web浏览器状态栏，显示浏览器将获得的页面的“地址”。 换言之，单击Adobe Experience Platform链接会告知浏览器“为我获取该页面，以便我可以在屏幕上看到该页面”。

单击链接后，浏览器会向服务器请求获取页面。 这是 `GET` 请求，Web API常用的请求方法之一。 浏览器需要满足以下要求之一：页面“地址” — 该页面在Web上的什么位置？

### URL的部分

![带有URL的浏览器地址栏](../assets/api101-address-bar.png)

大多数浏览器都有一个“地址栏”，用于显示网页的部分或全部“地址”。 当浏览器“获取”我们单击的链接所对应的页面时，它会在此地址栏中显示该页面的“地址”。 网页的“地址”是什么？

那个 `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html` 上面是网页的地址，称为URL或统一资源定位器。 URL可以引用此类页面或图像文件、视频或其他文件类型。

![URL的部分](../assets/api101-url-parts.jpg)

此地址(URL)具有与Web API和浏览器API非常相关的特定部分。

**方案**

的 `scheme` 上面也称为 `protocol` 使用Web API，并且通常 `http` 或 `https`. HTTP或HyperText传输协议是将诸如网页之类的资源从Web服务器传输到Web浏览器的方式。 HTTPS是安全版本，在该版本中，传输通过Internet进行，使用的是旨在防止对所传输资源的干扰的安全性。 通过HTTPS查看页面时，浏览器地址栏中通常会显示一个小锁图标。

对于Web API，这些资源的传输是通过HTTP请求进行的 — 换言之，就是通过HTTP发出请求。

**主机和域**

的 `business.adobe.com` 是所请求资源的主机。 单击示例链接后，浏览器会使用URL的这一部分来查找托管页面的服务器。 它并不总是与Web服务器完全相同，但在基本层面，我们可以将其视为浏览器将在其中获取我们请求的页面的服务器。

域名是域名系统的一部分，更称为DNS。 大多数人会想 `adobe.com` 或 `example.com` 作为“域名”，但是有一些与API相关的部分。 `www.adobe.com` 和 `business.adobe.com` 可以称为域名，但 `www.` 和 `business.` 部件称为子域。 API通常与包含子域(如 `api.example.com` 或 `sub.www.example.com`.

很常见的是 _主机_ 请参阅包括任何子域(如 `business.adobe.com`. 通常也会看到这些术语 _域_ 或 _域名_ 指的是没有子域(如 `adobe.com`. 记住每个部分的具体术语和主机的变体在这里并不重要。 但请注意这些术语通常使用非常重要，因此您可以阐明业务和讨论的任何相关细节。

**Origin**

Origin是另一个需要注意的术语，它与URL的各个部分密切相关。 在基本层面，起源大致为 `scheme` 加 `host` 加 `domain` 点赞 `https://business.adobe.com`. 不同的值通常表示不同的源，如 `https://business.adobe.com` 和 `http://business.adobe.com` 不是同一来源，因为它们有不同的方案。 `https://www.adobe.com` 和 `https://business.adobe.com` 由于子域的不同，在许多用途中也不是相同的源。

**路径**

上面URL示例中的最后一位是 `path` 到资源 — 示例中的页面。 的 `/products/experience-platform/` part通常表示web服务器上的文件夹或目录。 就像我们的计算机上有文件夹或目录来存放文档和照片一样，我们在Web服务器上也有文件夹来整理内容。 最后， `/adobe-experience-platform.html` “零件”(part)是文件的名称，即网页。

URL的其他更详细部分将在此系列的下一部分突出显示。

### 第三方API

Web API有时称为第三方API。 就像交易中的当事人一样。 在我们的链接示例中，您（更具体地说，您的浏览器）是页面请求的第一方。 Web服务器是第二方。 那么第三个呢？

网页通常包含来自其他主机或来源的内容或资源。 在这些情况下，当您的浏览器开始显示页面时，会向托管这些资源的其他主机（或“第三方”）发出另一组请求。 这非常常见，尤其是对于视频或图像等媒体内容，也非常常见，因为在查看或使用时需要更新的数据。 获取一天中的当前时间、当前天气或特定人员的个性化欢迎消息都是示例，第三方API可以在适当的时间提供适当的资源。 来自这些第三方API的这些请求很常见。

## Web API的常见用法

除了一天中的某个时间、天气或个性化内容之外，Web API还有许多用途。 twitter、TikTok、Facebook、LinkedIn、Snapchat、Pinterest等社交媒体平台拥有各种各样的API，程序员可以在其应用程序中使用这些API。 当然，Adobe也 [各种各样的API](https://developer.adobe.com/apis) 程序员使用这些工具，以便其软件能够与Adobe产品和服务进行交互。 软件产品和服务可通过这些API访问其他软件产品和服务。

## 示例API

浏览器API允许程序员直接与浏览器的功能进行交互。 电池API允许软件检查设备的电池状态，以便在需要时提醒您。 剪贴板API允许软件复制或粘贴设备的剪贴板。 全屏API允许软件提供将视图扩展到设备全屏的选项，如YouTube。

Adobe Experience Platform数据访问API是一个Web API，它允许程序员从Adobe Experience Platform访问和下载数据集文件，以便他们在自己的程序中使用客户配置文件数据。 像这样的API很常见，它是软件自动化过程的一部分，在该过程中，软件被编程以使用多个API组合执行一系列步骤。 与手动执行这些相同步骤相比，这通常可以显着节省成本。

## API端点

当程序员在其程序中“使用”浏览器或Web API时，他们通常会请求发送或接收资源，例如我们请求网页的示例浏览器。 API文档通常列出这些请求的“端点”，例如： `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. 这是程序员用于获取数据集文件的Platform Data Access API的特定模式或“端点”。

的 `{dataSetFileId}` 由这些大括号括起来表示程序员在请求中需要发送的值。 因此，实际API请求中的URL将类似于 `https://platform.adobe.io/data/foundation/export/files/xyz123brb` 其中 `xyz123brb` 必须是程序员要接收的数据集文件的有效ID。

换言之，就像浏览器在特定URL上获取页面一样，API请求也会从特定端点（如此数据集示例）获取资源，或将资源发送到特定端点。

## HTTP请求方法

此时，应该清楚的是，Web API会请求网页或数据集等资源。 与大多数软件概念一样，这些HTTP请求遵循可重复模式。 从软件应用程序向另一个软件应用程序发送请求，该软件应用程序会评估该请求，然后做出响应：浏览器从web服务器请求页面，并随页面内容做出响应。

从请求到响应的整个过程涉及许多较小且非常详细的步骤，但请求方法很简单。 请求方法定义要请求的操作。

**`GET`**

的 `GET` 请求提供资源的响应时，会使用请求方法，例如我们的网页和数据集示例。 当我们单击浏览器中的链接或点按移动设备上的链接时，我们会创建 `GET` 请求。

**`POST`**

的 `POST` 方法会随请求发送数据。 “请求”发送数据听起来可能有些奇怪，但提出API请求的想法是要求端点（即接收软件）接受该请求，如果是 `POST`，以接受正在发送的数据。 发送的数据通常写入数据存储（如数据库或文件），以便保存。

**`PUT`**

的 `PUT` 请求方法类似于 `POST` 由于它发送数据，但如果发送的数据在端点已存在，则 `PUT` 将通过替换现有数据来更新现有数据。 A `POST` 不更新，只是发送，因此多个 `POST` 请求可以为发送的数据创建多个记录，而不是更新任何现有记录。

**`PATCH`**

的 `PATCH` request方法用于发送更新部分现有记录的数据，例如，当我们通过更新帐户配置文件来更改地址时。 使用 `POST` 请求可以创建其他用户档案，并且 `PUT`，则可以替换现有用户档案，但使用 `PATCH` 方法我们只需更新现有记录的相关部分，如我们的地址。

**`DELETE`**

的 `DELETE` request方法会删除请求中指定的资源，例如，我们单击链接以完全删除我们的帐户配置文件。

还有其他几种方法，但这里列出了使用API时最常用的方法。

### 请求示例

现在，您已了解API涉及的基本术语、概念和步骤，接下来我们可以在实际中查看API请求示例。

浏览器示例中的页面的URL为 `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`. 单击Adobe Experience Platform链接后，浏览器会 `GET` 请求此页面。 由于我们有浏览器来为我们完成工作，因此我们只需单击，但如果程序员希望在软件应用程序中发生该请求，则他们必须提供API请求所需的所有详细信息才能成功完成。

下面显示了代码中的显示方式：

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

在上面的代码中，您可以看到 `URL` 浏览器正在请求，位于底部附近的是 `method: "GET"` 请求方法。 其他代码行也是请求的一部分，但不在本文的范围之内。


*[API]:应用程序编程接口*[URL]:统一资源定位器*[HTTP]:超文本传输协议*[DNS]:域名系统
