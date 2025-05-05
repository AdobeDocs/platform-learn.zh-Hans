---
title: 订阅数据摄取事件
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 订阅数据摄取事件
description: 在本课程中，您将通过使用Adobe Developer Console和在线webhook开发工具设置webhook来订阅数据摄取事件。 在后续课程中，您将使用这些事件监测数据摄取作业的状态。
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 订阅数据摄取事件

<!--25min-->

在本课程中，您将通过使用Adobe Developer Console和在线webhook开发工具设置webhook来订阅数据摄取事件。 在后续课程中，您将使用这些事件监测数据摄取作业的状态。

**数据工程师**&#x200B;将希望在本教程之外订阅数据摄取事件。
**数据架构师** _可以跳过本课程_&#x200B;并转到[批量摄取课程](ingest-batch-data.md)。

## 所需的权限

在[配置权限](configure-permissions.md)课程中，您已设置完成本课程所需的所有访问控制，特别是：

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> 数据摄取事件触发的这些通知将应用于&#x200B;_您的所有沙盒_，而不仅仅是您的`Luma Tutorial`。 您还可能在帐户中看到源自其他数据摄取事件的通知。


## 设置webhook

在本练习中，我们将使用名为webhook.site的在线工具创建一个webhook（请随意替换您喜欢使用的任何其他webhook开发工具）：

1. 在另一个浏览器选项卡中，打开网站[https://webhook.site/](https://webhook.site/)
1. 您会获得一个唯一的URL，当您稍后在数据摄取课程中返回该URL时，您应该将该URL加入书签：

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. 在顶部导航中选择&#x200B;**编辑**&#x200B;按钮
1. 作为响应正文，输入`$request.query.challenge$`。 我们在本课程稍后设置的Adobe I/O事件通知向webhook发送挑战，并要求将其包含在响应正文中。
1. 选择&#x200B;**保存**&#x200B;按钮

   ![编辑响应](assets/ioevents-webhook-editResponse.png)

## 设置

1. 在另一个浏览器选项卡中，打开[Adobe Developer Console](https://console.adobe.io/)
1. 打开您的`Luma Tutorial API Project`
1. 选择&#x200B;**[!UICONTROL 添加到项目]**&#x200B;按钮，然后选择&#x200B;**[!UICONTROL 事件]**

   ![添加事件](assets/ioevents-addEvents.png)
1. 通过选择&#x200B;**[!UICONTROL Experience Platform]**&#x200B;筛选列表
1. 选择&#x200B;**[!UICONTROL 平台通知]**
1. 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;按钮
   ![添加通知](assets/ioevents-addNotifications.png)
1. 选择所有事件
1. 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;按钮
   ![选择订阅](assets/ioevents-addSubscriptions.png)
1. 在配置凭据的下一个屏幕上，再次选择&#x200B;**[!UICONTROL 下一步]**&#x200B;按钮
   ![跳过凭据屏幕](assets/ioevents-clickNext.png)
1. 作为&#x200B;**[!UICONTROL 事件注册名称]**，请输入`Platform notifications`
1. 向下滚动并选择以打开&#x200B;**[!UICONTROL Webhook]**&#x200B;部分
1. 作为&#x200B;**[!UICONTROL Webhook URL]**，粘贴来自webhook.site的&#x200B;**您的唯一URL**&#x200B;字段的值
1. 选择&#x200B;**[!UICONTROL 保存配置的事件]**&#x200B;按钮
   ![保存事件](assets/ioevents-addWebhook.png)
1. 等待配置保存，您应该会看到`Platform notifications`事件处于活动状态，并且webhook详细信息未显示错误消息
   ![配置已保存](assets/ioevents-webhookConfigured.png)
1. 切换回webhook.site选项卡，您应该会看到对webhook的第一个请求，该请求是验证Developer Console配置的结果：
   ![webhook.site中的第一个请求](assets/ioevents-webhook-firstRequest.png)

目前为止，您将在下一课程中摄取数据时了解有关这些通知的更多信息。

## 其他资源

* [Webhook.site](https://webhook.site/)
* [数据摄取通知文档](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html?lang=zh-Hans)
* [Adobe I/O事件快速入门文档](https://www.adobe.io/apis/experienceplatform/events/docs.html)

好，让我们最终开始[摄取数据](ingest-batch-data.md)！
