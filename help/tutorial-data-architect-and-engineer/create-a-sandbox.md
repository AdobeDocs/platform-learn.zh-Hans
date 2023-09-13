---
title: 创建沙盒
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建沙盒
description: 在本课程中，您将创建一个开发环境沙盒，您可以在本教程的其余部分使用该沙盒。
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: fdb6a49caa29d98d73524fd0887d25641ef67780
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 创建沙盒

<!--25min-->

在本课程中，您将创建一个开发环境沙盒，并在本教程的其余部分使用该沙盒。

沙盒提供了独立的环境，您可以在其中试用功能而不会将资源和数据混入到生产环境中。 欲知更多详情，请参见 [沙盒文档](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=zh-Hans).

**数据架构师** 和 **数据工程师** 将需要在本教程之外创建沙盒。

在开始练习之前，请观看此简短视频，了解更多有关沙箱的信息：
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## 所需的权限

在 [配置权限](configure-permissions.md) 课程：您已设置完成本课程所需的所有访问控制。

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## 创建沙盒

让我们创建一个沙盒：

1. 登录 [Adobe Experience Platform](https://experience.adobe.com/platform) 界面
1. 转到 **[!UICONTROL 沙盒]** 在左侧导航中
1. 选择 **[!UICONTROL 创建沙盒]** 在右上方
   ![选择创建沙盒](assets/sandbox-createSandbox.png)

1. 选择 **[!UICONTROL 开发]** 作为 **[!UICONTROL 类型]**
1. 命名您的沙盒 `luma-tutorial` （考虑在结尾处添加您的姓名）
1. 给您的教程加上标题 `Luma Tutorial` （考虑在结尾处添加您的姓名）
1. 选择 **[!UICONTROL 创建]** 按钮
   ![创建沙盒](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >虽然您可以将任意值用于沙盒名称和标题，但建议遵循建议的值，因为在本教程中，我们将参考这些标签。 如果您的组织中有多个人员正在完成本教程，请考虑在沙盒标题和名称的末尾添加您的名称，例如luma-tutorial-ignatiusjreilly。

创建沙盒大约需要30秒，在此期间，“[!UICONTROL 正在创建]”状态将显示。 完全创建沙盒后，它显示为&quot;[!UICONTROL 活动]“：
![活动状态](assets/sandbox-active.png)

等到您的沙盒为“[!UICONTROL 活动]”然后再继续进行下一个练习。

## 将新沙盒添加到角色

一旦沙盒处于活动状态，您就必须将其包含在您的角色中才能使用它。 要将其添加到您的角色（需要系统管理员或产品管理员权限），请执行以下操作：

1. 转到 [!UICONTROL 权限] screen
1. 打开 `Luma Tutorial Platform` 角色
1. （可选） _移除_ 该 `Prod` 角色中的沙盒
1. 添加 `Luma Tutorial` 沙盒
1. 选择 **[!UICONTROL 保存]**
1. 在 [!UICONTROL 沙盒] 行，选择 **[!UICONTROL 编辑]**

   ![添加Luma教程](assets/sandbox-addLumaTutorial.png)

1. 重新加载（或按住Shift键重新加载）页面，此时您应位于 `Luma Tutorial` 沙盒，或者它应该显示在沙盒下拉列表中
1. 切换到 `Luma Tutorial` 沙盒（如果您尚未在该沙盒中）

   ![确认沙盒](assets/sandbox-confirmDropdown.png)

太好了，您已创建沙盒并准备好 [设置开发人员控制台和Postman](set-up-developer-console-and-postman.md)！
