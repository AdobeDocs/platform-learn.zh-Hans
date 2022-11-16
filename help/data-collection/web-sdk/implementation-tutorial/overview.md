---
title: 概述
description: 概述
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# 概述

收集有关用户浏览器中发生的事件的数据是营销策略的基本原则。 Adobe提供了多种工具来帮助您管理此数据。 虽然您可以单独熟悉这些工具中的每个工具，但本教程会尝试提供更广泛的视图，了解每个工具的用途以及它们如何协同工作来实现共同目标。

在本教程中，我们将讨论一项策略：(1)在Adobe Experience Platform中构建并保留您的数据，(2)在浏览器中管理您的数据并告知已发生某些事件，以及(3)通过向Adobe Experience Platform发送相关数据来对此类事件做出响应。

虽然本教程使用Adobe客户端数据层、Adobe Experience Platform Web SDK和标记功能进行更规范、更无缝的实施，但您也可以将这些工具与第三方或内部工具混合使用，以实现最大灵活性。

## 示例场景

在本教程中，我们假定您正在为电子商务网站上的简单产品页面实施数据收集。 产品页面将在浏览器中加载。 在此，您将跟踪用户是否已查看产品。 用户决定购买产品，因此他们单击按钮以将产品添加到购物车。 在此，您将跟踪用户是否已打开新购物车，并通过将体验事件发送到Adobe Experience Platform将产品添加到购物车。 最后，用户单击 _下载应用程序_ 链接，因为他们对您的移动设备应用程序感兴趣。 您将跟踪用户是否已点击该链接。
