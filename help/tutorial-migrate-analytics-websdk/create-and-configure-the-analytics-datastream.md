---
title: 创建和配置数据流
description: 了解如何创建和配置新数据流，以便将您的网站数据路由到Adobe Analytics。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16757
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# 创建和配置数据流

了解如何创建和配置新数据流，以便将您的网站数据路由到Adobe Analytics。

在本课程中，您将学习如何创建和配置系统，以便您的数据从网站流到Adobe Edge，然后从那里路由到Adobe Analytics。

![架构图](assets/architecture_diagram.jpg)

## 创建新的开发数据流

1. 打开Adobe数据收集界面
   1. 在浏览器中导航到https://experience.adobe.com
   1. 确保在页面顶部选择正确的组织(例如，下图中的Adobe生产 — 技术营销演示)
   1. 单击“九个点”（即应用程序切换器），然后选择&#x200B;**数据收集**

      ![导航到数据收集](assets/navigate-to-data-collection.jpg)

1. 在左侧导航中转到&#x200B;**[!UICONTROL 数据流]**
1. 选择&#x200B;**[!UICONTROL 新数据流]**
1. 输入所需的&#x200B;**[!UICONTROL Name]**，并包括一个指示符，指示符将用于Web SDK开发环境。 例如，您可以按站点名称来命名它，如下所示。 记下该名称，因为稍后在标记属性中配置Web SDK扩展时，将引用该名称。 根据需要输入描述。

   >[!NOTE]
   >
   >如果使用用于数据收集的[数据准备](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/edge-network/data-prep)功能，您只需选择架构，在本教程中，我们将不会执行此操作。 请访问链接以了解更多信息。

1. 选择&#x200B;**[!UICONTROL 保存]**

   ![创建数据流](assets/create-new-datastream.jpg)

1. 保存数据流后，将显示一个新屏幕，告诉您尚未配置任何服务。 换言之，您的数据将发送到Edge服务器，但在我们添加服务之前，不会发送到任何应用程序。 我们现在将配置数据流以将数据发送到Adobe Analytics。 单击&#x200B;**[!UICONTROL 添加服务]**。
   ![添加服务](assets/datastream-add-service.jpg)
1. 在服务下拉菜单中，选择&#x200B;**[!UICONTROL Adobe Analytics]**。
1. 在“报表包ID”字段中，输入您在[创建验证报表包](create-a-validation-report-suite.md)活动中创建的验证报表包的ID（不是标题，而是报表包ID）。 单击&#x200B;**[!UICONTROL 保存]**。

## 暂存和生产数据流

您现在希望&#x200B;**再次执行相同的步骤**&#x200B;两次：一次用于暂存环境，另一次用于生产环境。 当您设置这两个额外的数据流时，我们将在下面添加一些注释。

### 暂存数据流

* 在命名数据流时（以及在添加描述时），您可以/应该具有相同的名称，不同之处在于添加“staging”而不是“development”。
* 像以前一样添加Adobe Analytics服务，并将报表包设置为相同的开发报表包。
* 如果您希望更干净的环境来查看Adobe Analytics报表中的暂存编号，则可以创建一个仅用于暂存的新报表包，然后确保在此数据流的Analytics服务中指向该报表包。

### 生产数据流

* 在命名数据流时（以及在添加描述时），您可以/应该具有相同的名称，不同之处在于添加“production”而不是“development”。
* 当选择要将数据映射到的报表包时，您可以将此数据流映射到AppMeasurement实现馈送的&#x200B;**当前**&#x200B;生产报表包，而不是选择开发报表包或甚至新的报表包。 这样，在完成迁移并对其进行测试并对数字感到满意后，您可以删除旧的AppMeasurement代码，将标记库发送到生产环境，并且您会将新的生产数据馈送到同一生产报表包，以便旧实施与新实施之间可以保持连续性。
