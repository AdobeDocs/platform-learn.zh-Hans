---
title: 创建沙盒
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建沙盒
description: 在本课程中，您将创建一个开发环境沙盒，以供在教程的其余部分使用。
role: Data Architect, Data Engineer
feature: Sandboxes
kt: 4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 创建沙盒

<!--25min-->

在本课程中，您将创建一个开发环境沙盒，在本教程的其余部分中将使用该沙盒。

沙盒提供了独立的环境，您无需将资源和数据与生产环境混合即可在其中试用功能。 有关更多详细信息，请参阅 [沙盒文档](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=zh-Hans).

**数据架构师** 和 **数据工程师** 将需要在本教程之外创建沙箱。

在开始练习之前，请观看此简短视频，进一步了解沙箱：
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## 所需权限

在 [配置权限](configure-permissions.md) 课程中，您将设置完成本课程所需的所有访问控制。

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## 创建沙盒

让我们创建一个沙盒：

1. 登录 [Adobe Experience Platform](https://experience.adobe.com/platform) 界面
1. 转到 **[!UICONTROL 沙箱]** 在左侧导航中
1. 选择 **[!UICONTROL 创建沙盒]** 在右上方
   ![选择创建沙盒](assets/sandbox-createSandbox.png)

1. 选择 **[!UICONTROL 开发]** 作为 **[!UICONTROL 类型]**
1. 命名沙盒 `luma-tutorial` （请考虑将您的名称添加到结尾）
1. 标题教程 `Luma Tutorial` （请考虑将您的名称添加到结尾）
1. 选择 **[!UICONTROL 创建]** 按钮
   ![创建沙盒](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >虽然您可以对沙盒名称和标题使用任何任意值，但建议遵循建议的值，因为我们将在整个教程中引用这些标签。 如果贵组织有多个人员在完成本教程，请考虑在沙盒标题和名称的末尾添加您的名称，例如luma-tutorial-ignatiusjreilly。

沙盒大约需要30秒才能创建，在此期间，将“[!UICONTROL 创建]“ ”状态。 完全创建沙盒后，将显示为“[!UICONTROL 活动]&quot;:
![活动状态](assets/sandbox-active.png)

等待沙盒为“[!UICONTROL 活动]”，然后继续下一个练习。

## 将新沙盒添加到产品用户档案

沙盒激活后，必须将其包含在产品用户档案中才能使用。 要将其添加到您的产品用户档案，请执行以下操作：

1. 在单独的浏览器选项卡中，登录 [Admin Console](https://adminconsole.adobe.com)
1. 转到 **[!UICONTROL 产品>Adobe Experience Platform]**
1. 打开 `Luma Tutorial Platform` 个人资料

   ![选择产品配置文件](assets/sandbox-selectProfile.png)

1. 转到 **[!UICONTROL 权限]** 选项卡

1. 在 [!UICONTROL 沙箱] 行，选择 **[!UICONTROL 编辑]**

   ![选择编辑](assets/sandbox-selectSandboxes.png)

1. _删除_ the **[!UICONTROL 生产]** 最初分配给用户档案的沙盒
1. 选择 **[!UICONTROL +]** 图标以添加新 `Luma Tutorial` 沙盒到右侧列
1. 选择 **[!UICONTROL 保存]** 保存更新的权限

   ![将沙盒移到另一列](assets/sandbox-addLumaTutorial.png)

1. 返回浏览器选项卡并显示Experience Platform
1. 重新加载（或按Shift键重新加载）页面，此时您应该位于 `Luma Tutorial` 或者，它应该显示在沙盒下拉列表中
1. 切换到 `Luma Tutorial` 沙盒（如果您尚未加入）

   ![确认沙盒](assets/sandbox-confirmDropdown.png)

太好了，您已创建了沙盒，并准备好 [设置开发人员控制台和Postman](set-up-developer-console-and-postman.md)!
