---
title: 概述
description: 概述
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# 概述

收集有关用户浏览器中发生的事件的数据是营销策略的基本原则。 Adobe提供了多种工具来帮助您管理这些数据。 虽然您可以单独了解这些工具中的每一个，但本教程旨在更广泛地了解每个工具的功能以及它们如何协作以实现共同目标。

在本教程中，我们将讨论以下方面的一种策略：(1)在Adobe Experience Platform中构建并保留您的数据，(2)在浏览器中管理您的数据并传达已发生某些事件，以及(3)通过将相关数据发送到Adobe Experience Platform来响应此类事件。

虽然本教程使用Adobe客户端数据层、Adobe Experience Platform Web SDK和标记功能来实现更具规范性的无缝实施，但您也可以将这些工具与第三方或内部工具混合搭配使用，以实现最大的灵活性。

## 示例场景

在本教程中，我们假定您正在电子商务网站上为一个简单的产品页面实施数据收集。 产品页面即会加载到浏览器中。 在此，您将跟踪用户是否查看过该产品。 用户决定购买该产品，因此他们单击按钮将该产品添加到购物车。 在此，您将通过向Adobe Experience Platform发送体验事件来跟踪用户是否已打开新购物车并将产品添加到购物车。 最后，用户单击 _下载应用程序_ 链接，因为他们对您的移动应用程序感兴趣。 您将跟踪用户是否已单击链接。
