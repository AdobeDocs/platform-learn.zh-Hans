---
title: 概述
description: 概述
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---

# 使用Adobe Experience Platform数据收集

收集有关用户浏览器中发生的事件的数据是营销策略的基本原则。 Adobe提供了多种工具来帮助您管理此数据。 虽然您可以单独熟悉这些工具中的每个工具，但本教程会尝试提供更广泛的视图，了解每个工具的用途以及它们如何协同工作来实现共同目标。

在本教程中，我们将讨论以下策略：

1. 在Adobe Experience Platform中构建并保留您的数据，
1. 在浏览器中管理数据并告知已发生某些事件，以及
1. 通过向Adobe Experience Platform发送相关数据来对此类事件做出反应。

本教程使用Adobe客户端数据层、Adobe Experience Platform Web SDK和 [!DNL Tags] 功能提供了更规范、更无缝的实施，您还可以将这些工具与第三方或内部工具混合使用，以实现最终的灵活性。

## 示例场景

在本教程中，您将为电子商务网站上的简单产品页面实施数据收集：

1. 产品页面将在浏览器中加载。 在此，您可以跟踪用户是否已查看过产品。
1. 用户决定购买产品，因此他们单击按钮以将产品添加到购物车。 在此，您可以通过将体验事件发送到Adobe Experience Platform来跟踪用户是否已打开新购物车并将产品添加到购物车。
1. 最后，用户单击 _下载应用程序_ 链接，因为他们对您的移动设备应用程序感兴趣。 您跟踪用户是否已点击链接。

让我们开始吧！

[下一个： ](structuring-your-data.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
