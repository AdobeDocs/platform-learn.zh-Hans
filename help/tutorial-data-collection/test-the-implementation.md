---
title: 测试实施
description: 测试实施
exl-id: 66eb1d4e-32eb-45fc-8da4-8d3c04dc3c7a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---

# 测试实施

现在，您已设置网页并部署Adobe Experience Platform标记库，接下来该测试实施了。

1. 在浏览器中打开您的产品页面。 您可以通过单击 _文件_ then _打开文件……_ 或者，您可以在Web服务器上托管您的页面，并输入相应的URL。

页面加载后，您应会看到如下内容：
![网页](assets/webpage.png)

不漂亮，但它能做到。

## Inspect页面查看和产品查看事件

1. 在浏览器中打开开发人员工具，然后单击网络面板。 刷新页面。
此时，您应会看到四个请求：
* product.html — 您的网页。
* launch-###########-development.js — 您的Launch库。
* 交互 — 发送到服务器的页面查看事件。
* 交互 — 发送到服务器的产品查看事件。
Inspect每个请求的有效负载：
1. 对于第一个 `interact` 请求时，您应该能够看到 `eventType` of `web.webpagedetails.pageViews`.
   ![页面查看请求检查](assets/webpage-page-viewed-inspection.png)
1. 第二个 `interact` 请求时，您应该能够看到 `eventType` of `commerce.productViews`.
   ![产品查看请求检查](assets/webpage-product-view-inspection.png)
1. 查看其余要发送的数据，包括产品信息。

## Inspect打开的购物车和添加到购物车事件

1. 现在，单击**_添加到购物车_**按钮。

您应会看到两个其他请求，第一个请求带有 `eventType` of `commerce.productListOpens` （用于打开新购物车）和第二个 `eventType` of `commerce.productListAdds` （用于将产品添加到购物车）。

## Inspect下载应用程序链接点击事件

根据浏览器，单击使您离开当前页面的链接可能会清除您的网络面板。 由于您想要在离开页面之前检查网络请求是否发生了链接点击事件，因此需要配置浏览器以跨页面保留网络日志。

1. 通过检查 **_保留日志_** 复选框(Chrome、Safari、Edge)，或者单击齿轮图标并选中 **_保留日志_** 项目。
1. 单击 **_下载应用程序_** 链接。 你应该再看一个 `interact` 请求显示在“网络”面板中。
1. 通过 `eventType` of `web.webinteraction.linkClicks`，并查看有关所点击链接的详细信息。

## 检查数据是否到达Adobe Experience Platform数据集

现在，请求已发送，请检查数据是否安全地到达您创建的Adobe Experience Platform数据集。

1. 导航到 **[!UICONTROL 数据集]** 查看Adobe Experience Platform。
1. 选择 [数据集](configure-the-server/create-a-dataset.md) 创建的URL。
您可能需要等待几分钟，但很快您就会看到数据正在处理并插入数据集的指示。 您还应该查看处理是成功还是失败。 如果失败，您会知道失败的原因。 通常会失败，因为您发送的数据与架构不匹配，您需要相应地调整数据或架构。
   ![数据集摄取](assets/dataset-ingestion.png)

## 使用Adobe Experience Platform Debugger扩展

要深入了解您的实施在浏览器和Adobe服务器上的行为方式，请查看Adobe Experience Platform Debugger浏览器扩展！

[适用于Chrome的Adobe Experience Platform Debugger扩展](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Adobe Experience Platform Debugger Firefox扩展](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/)

[下一个： ](summary.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)