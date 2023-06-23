---
title: 创建沙盒
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 创建沙盒
description: 在本课程中，您将创建一个开发环境沙盒，并用于本教程的其余部分。
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 创建沙盒

<!--25min-->

在本课程中，您将创建一个开发环境沙盒，并用于本教程的其余部分。

沙盒提供了独立的环境，您可以在其中试用功能而无需将资源和数据与生产环境混合。 欲知更多详情，请参见 [沙盒文档](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=zh-Hans).

**数据架构师** 和 **数据工程师** 将需要在本教程之外创建沙箱。

在开始练习之前，请观看此简短视频，了解有关沙箱的更多信息：
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## 所需的权限

在 [配置权限](configure-permissions.md) 在本课程中，您将设置完成本课程所需的所有访问控制。

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
1. 选择 **[!UICONTROL 创建沙盒]** 右上角
   ![选择创建沙盒](assets/sandbox-createSandbox.png)

1. 选择 **[!UICONTROL 开发]** 作为 **[!UICONTROL 类型]**
1. 为您的沙盒命名 `luma-tutorial` （考虑在结尾处添加您的姓名）
1. 为教程添加标题 `Luma Tutorial` （考虑在结尾处添加您的姓名）
1. 选择 **[!UICONTROL 创建]** 按钮
   ![创建沙盒](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >虽然您可以对沙盒名称和标题使用任意值，但建议坚持使用建议的值，因为在本教程中，我们将参考这些标签。 如果您的组织中有多个人员正在完成本教程，请考虑在沙盒标题和名称的末尾添加您的名称，例如luma-tutorial-ignatiusjreilly。

创建沙盒大约需要30秒，在此期间“[!UICONTROL 正在创建]“ ”状态随即显示。 完全创建沙盒后，它显示为“[!UICONTROL 活动]“：
![活动状态](assets/sandbox-active.png)

等到您的沙盒为“[!UICONTROL 活动]”之后再继续下一个练习。

## 将新沙盒添加到产品配置文件

一旦沙盒处于活动状态，您就必须将其包含在您的角色中才能使用它。 要将其添加到您的角色（需要系统管理员或产品管理员权限），请执行以下操作：

1. 转到 [!UICONTROL 权限] screen
1. 打开 `Luma Tutorial Platform` 角色
1. _移除_ 此 `Prod` 角色中的沙盒
1. 添加 `Luma Tutorial` 沙盒
1. 选择 **[!UICONTROL 保存]**
1. 在 [!UICONTROL 沙盒] 行，选择 **[!UICONTROL 编辑]**

   ![添加Luma教程](assets/sandbox-addLumaTutorial.png)

1. 重新加载（或按住Shift键重新加载）页面，此时您应位于 `Luma Tutorial` 沙盒，或者它应显示在沙盒下拉列表中
1. 切换到 `Luma Tutorial` 沙盒（如果您尚未在此沙盒中）

   ![确认沙盒](assets/sandbox-confirmDropdown.png)

太棒了，您已创建沙盒并准备好 [设置开发人员控制台和Postman](set-up-developer-console-and-postman.md)！
