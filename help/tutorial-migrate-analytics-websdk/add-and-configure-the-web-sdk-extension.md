---
title: 添加和配置Web SDK扩展
description: 了解如何在Tags资产中添加和配置Web SDK扩展，以便在后续课程中为您提供完成迁移所需的功能。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16758
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# 添加和配置Web SDK扩展

了解如何在Tags资产中添加和配置Web SDK扩展，以便在后续课程中为您提供完成迁移所需的功能。
按照以下步骤添加和配置扩展：

1. 导航到Experience Platform数据收集。 这可以通过两种方式之一实现：
   1. 转到[Adobe Experience Platform界面](https://platform.adobe.com/)，然后选择左侧导航底部附近的&#x200B;**[!UICONTROL 标记]**。
      ![访问标记1](assets/access-tags-1.jpg)
   1. 如果您无权访问Platform，则可以使用窗口右上角的应用程序切换器（9个点）并选择数据收集(登录Experience.Adobe.com后)。
      ![访问标记2](assets/access-tags-2.jpg)
1. 查找并选择您要迁移到Web SDK的标记属性。
1. 在标记属性的左侧导航中，选择&#x200B;**[!UICONTROL 扩展]**。
1. 选择顶部附近的&#x200B;**[!UICONTROL 目录]**，查看所有可用扩展的列表。
1. 搜索并选择&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;扩展，然后单击右侧的&#x200B;**[!UICONTROL 安装]**。

   ![查找Web SDK扩展](assets/find-the-websdk-extension.jpg){style="border:1px solid lightslategray"}

1. 此时会显示扩展配置设置。 找到数据流部分，然后设置要用于此迁移的Experience Platform沙盒（所有三个环境的“环境”下拉列表）。 如果您只迁移Adobe Analytics而不向Adobe Experience Platform发送数据，请选择&#x200B;**生产**&#x200B;沙盒。 如果您要将此行为分析数据发送到Experience Platform以在那里的应用程序中使用，请选择要用于此的沙盒。 您可能首先会希望选择一个开发沙盒，直到完成迁移并添加/测试您的Platform服务为止。
1. 非常重要的是，通过选择您在上一步中为生产、暂存和开发环境创建的数据流，将标记中的此处的代码和设置连接到Edge。

   ![数据流选择](assets/choose-datastreams.jpg){style="border:1px solid lightslategray"}

1. 向下滚动并注意默认已选择&#x200B;**标识**&#x200B;设置。 保持选中这些复选框，因为它们有助于在迁移到Web SDK时正确识别网站访客。 有关更多信息，请参阅下面的文档。

1. 选择&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>现在，Tags资产已基本安装和配置了Web SDK扩展。 在本迁移教程中创建或修改数据元素和规则时，我们将使用Web SDK扩展的部分内容，但不会更改教程中的任何其他扩展配置项目。 其他配置项目可以也应该用于其他用例。 有关这些配置的详细文档，请参阅[配置Web SDK标记扩展](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration)。
