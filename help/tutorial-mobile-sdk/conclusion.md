---
title: 完成Platform Mobile SDK教程后的结论和后续步骤
description: 完成本教程后的后续操作
recommendations: display,noCatalog
jira: KT-14642
exl-id: 69db6cf3-0d5d-4864-aac2-e5e1aea4c02e
source-git-commit: cb97521c7906bcb16c7352f6c2447e07abb828c7
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 3%

---

# 结论和后续步骤

恭喜！您已完成“在移动应用程序中实施Adobe Experience Cloud”教程！

让我们快速回顾一下您已完成的所有工作。 您具有：

* 使用标准和自定义字段组创建了架构。
* 设置数据流。
* 已配置移动标记属性。
* 在应用程序中安装并实施标记扩展。
* 在应用程序中实施了以下功能：
   * 同意
   * 生命周期数据
   * 事件跟踪
   * 标识
   * 配置文件
   * Places
* 已将Experience Cloud参数正确传递给Web视图。
* 已使用Adobe Experience Platform Assurance验证实施。
* 已将实施连接到以下Experience Cloud应用程序：
   * Adobe Analytics
   * Experience Platform
   * Journey Optimizer
   * Adobe Target

您已准备好开始历程的下一阶段 — 在您自己的移动应用程序中实施Adobe Experience Cloud！

而且还有更多可学习的内容！ 要在您的实施基础上进行构建，请查看以下对其他内容的一些建议：

* **启用事件转发**。 可以在数据流中轻松启用事件转发。 以下是Web SDK教程中有关配置事件转发[&#128279;](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=zh-Hans)的实践课程。 使用为您的移动实施创建的资源，并选择您在应用程序中实施的XDM字段。
* **连接Customer Journey Analytics**。 如果您创建了[Platform数据集](platform.md)，则可以将该数据集连接到Customer Journey Analytics。 在此[视频教程中了解详情](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/connections/connecting-customer-journey-analytics-to-data-sources-in-platform.html?lang=zh-Hans)
* **在数据流中启用Audience Manager**。 将您的XDM Experience事件发送到Audience Manager，并开始根据移动应用程序参与Audience Manager构建区段。
* **在Platform**&#x200B;中生成区段。 如果您为Real-time Customer Profile[&#128279;](platform.md)启用了架构和数据集，则可以根据您的移动应用程序事件构建区段，将它们与其他源中的数据相结合，然后将这些区段发送到Real-time Customer Data Platform中的目标。 在此[视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=zh-Hans)中了解有关区段生成器的更多信息。
* **实施Platform Web SDK**。 您现在已经掌握了一个SDK，请学习另一个！ Adobe Experience Platform Web SDK是一个用于为网站上的Experience Cloud和第三方服务提供支持的JavaScript SDK。 Web SDK[&#128279;](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans)有一个类似的实践教程。 完成这两个操作后，即可看到配置文件跨设备合并！
* **了解有关Experience Platform的更多信息**。 在[面向数据架构师和数据工程师的Adobe Experience Platform快速入门](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=zh-Hans)中，了解有关如何从其他源摄取数据并将这些数据与Mobile SDK数据结合在一起的更多信息


>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Mobile SDK。 如果您有疑问、希望共享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上共享它们。
