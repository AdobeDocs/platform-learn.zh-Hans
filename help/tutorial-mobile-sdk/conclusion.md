---
title: 结论和后续步骤
description: 完成教程后，接下来要做什么
recommendations: display,noCatalog
exl-id: 69db6cf3-0d5d-4864-aac2-e5e1aea4c02e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 4%

---

# 结论和后续步骤

恭喜！您已完成“在移动设备应用程序中实施Adobe Experience Cloud”教程！

让我们快速回顾一下您完成的所有工作。 您已：

* 使用标准和自定义字段组创建了架构。
* 设置数据流。
* 配置了移动标记属性。
* 在应用程序中安装和配置了标记扩展。
* 在应用程序中实施了以下功能：
   * 同意
   * 生命周期数据
   * 事件跟踪
   * 标识
   * 配置文件
* 正确将Experience Cloud参数传递到Web视图。
* 已使用Adobe Experience Platform Assurance验证实施。
* 已将实施连接到以下Experience Cloud应用程序：
   * Adobe Analytics
   * Experience Platform
   * Journey Optimizer

您已准备好开始历程的下一个阶段 — 在您自己的移动设备应用程序中实施Adobe Experience Cloud!

而且要学的总是更多！ 以下是一些关于其他内容的建议，这些建议将在您的实施基础上构建：

* **启用事件转发**. 可以在您的数据流中轻松启用事件转发。 以下是 [配置事件转发的实践课程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html) 的SDK教程中。 只需使用为您的移动设备实施创建的资源，然后选择您在应用程序中实施的XDM字段即可。
* **在Journey Optimizer中触发旅程**. 您在Luma应用程序中实施的事件可用于触发历程。 在中了解详情 [视频教程](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/create-journeys/use-case-transactional-journey.html).
* **连接Customer Journey Analytics**. 如果您创建了 [平台数据集](platform.md)，则可以将数据集连接到Customer Journey Analytics。 在中了解详情 [视频教程](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/connecting-customer-journey-analytics-to-data-sources-in-platform.html)
* **启用Audience Manager** 在数据流中启用Audience Manager，以发送XDM体验事件，并开始根据移动应用程序参与度构建区段。
* **实施Adobe Target**. 链接到移动资产的数据流配置尚不支持Target，但可以使用 [Adobe Target扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target).
* **在平台中构建区段**. 如果您启用了 [实时客户资料的架构和数据集](platform.md)，您可以根据移动设备应用程序事件构建区段，将其与其他来源的数据合并，然后将这些区段发送到Real-time Customer Data Platform中的目标。 在此处了解有关区段生成器的更多信息 [视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html).
* **实施平台Web SDK**. 现在您已掌握一个SDK，学习另一个SDK! Adobe Experience Platform Web SDK是JavaScript SDK，用于支持网站上的Experience Cloud和第三方服务。 类似的 [Web SDK动手教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans). 完成这两项操作，并查看跨设备合并的配置文件！
* **进一步了解Experience Platform**. 进一步了解如何从其他源摄取数据，并将其与Mobile SDK数据结合使用(位于 [面向数据架构师和数据工程师的Adobe Experience Platform快速入门](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)


>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)