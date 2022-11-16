---
title: 配置标记属性
description: 了解如何在 [!UICONTROL 数据收集] 界面。
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 10%

---

# 配置标记属性

了解如何在 [!UICONTROL 数据收集] 界面。

Adobe Experience Platform 中的标记是 Adobe 推出的新一代标记管理功能。标记为客户提供了一种简单的方式，让客户可以部署和管理所有用来加强相关客户体验的分析、营销和广告标记。详细了解 [标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans) （在产品文档中）。

## 先决条件

要完成本课程，您必须拥有创建标记属性的权限。 了解标记的基线也会有所帮助。

>[!NOTE]
>
> platform launch（客户端）现在为 [标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans)

## 学习目标

在本课程中，您将：

* 安装和配置移动标记扩展。
* 生成SDK安装说明。

## 初始设置

1. 创建新的移动设备标记属性：
   1. 在 [数据收集界面](https://experience.adobe.com/data-collection?lang=zh-Hans/){target=&quot;_blank&quot;}，选择 **[!UICONTROL 标记]** 在左侧导航中
   1. 选择 **[!UICONTROL 新建资产]**

      ![创建标记属性](assets/mobile-tags-new-property.png).
   1. 对于 **[!UICONTROL 名称]**，输入 `Mobile SDK Course`.
   1. 对于 **[!UICONTROL 平台]**，选择 **[!UICONTROL 移动设备]**.
   1. 选择&#x200B;**[!UICONTROL 保存]**。

      ![配置标记属性](assets/mobile-tags-property-config.png)

      >[!NOTE]
      >
      > 基于边缘的Mobile Sdk实施（例如，您在本教程中执行的实施）的默认同意设置来自 [!UICONTROL 同意扩展] 而不是 [!UICONTROL 隐私] 设置。 您将在本课程的后面部分添加和配置同意扩展。 有关更多信息，请参阅 [文档](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).


1. 打开新资产
1. 创建库:

   1. 转到 **[!UICONTROL 发布流程]** 中。
   1. 选择 **[!UICONTROL 添加库]**.

      ![选择添加库](assets/mobile-tags-create-library.png)

   1. 对于 **[!UICONTROL 名称]**，输入 `Initial Build`.
   1. 对于 **[!UICONTROL 环境]**，选择 **[!UICONTROL 开发]**.
   1. 选择  **[!UICONTROL Add All Changed Resources]**.
   1. 选择 **[!UICONTROL 保存并构建到开发环境]**.

      ![构建库](assets/mobile-tags-save-library.png)

   1. 最后，将其设置为 **[!UICONTROL 工作库]**.
      ![选择作为工作库](assets/mobile-tags-working-library.png)
1. 选择 **[!UICONTROL 扩展]**.

   移动核心扩展和配置文件扩展应已预安装。

1. 选择 **[!UICONTROL 目录]**.

   ![初始设置](assets/mobile-tags-starting.png)

1. 使用 [!UICONTROL 搜索] 功能来查找并安装以下扩展。 这些扩展都不需要任何配置：
   * 标识
   * AEP保证

## 扩展配置

1. 安装 **同意** 扩展。

   为本教程的目的，请选择 **[!UICONTROL 待定]**. 进一步了解 [文档](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network).

   ![同意设置](assets/mobile-tags-extension-consent.png)

1. 安装 **Adobe Experience Platform边缘网络** 扩展。

   在 **[!UICONTROL 边缘配置]** 下拉菜单，选择您在 [上一步](create-datastream.md).

1. 选择 **[!UICONTROL 保存到库并构建]**.

   ![边缘网络设置](assets/mobile-tags-extension-edge.png)


## 生成SDK安装说明

1. 选择 **[!UICONTROL 环境]**.

1. 选择 **[!UICONTROL 开发]** 安装图标。

   ![环境主屏幕](assets/mobile-tags-environments.png)

1. 选择 **[!UICONTROL iOS]**.

1. 选择 **[!UICONTROL Swift]**.

   ![安装说明](assets/mobile-tags-install-instructions.png)

1. 安装说明为您提供了实施的良好起点。

   您可以找到其他信息 [此处](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk).

   * **[!UICONTROL 环境文件ID]**:此唯一ID指向您的开发环境，请注意此值。 生产/暂存/开发将具有不同的ID值。
   * **[!UICONTROL Podfile]**:CocoaPods用于管理SDK版本和下载。 要了解更多信息，请查看 [文档](https://cocoapods.org/).
   * **[!UICONTROL 初始化代码]**:此代码块显示如何导入所需的SDK并在启动时注册扩展。

>[!NOTE]
>安装说明应视为起点，而不是明确的文档。 最新的SDK版本和代码示例可在 [文档](https://aep-sdks.gitbook.io/docs/).

## 移动标记架构

如果您熟悉标记的Web版本（以前称为Launch），那么了解移动设备上的差异就非常重要。

在Web上，标记属性会呈现到JavaScript中，然后JavaScript（通常）将托管在云中。 该JS文件直接在网站中引用。

在移动设备标记属性中，规则和配置将呈现到云中托管的JSON文件中。 移动设备应用程序中的Mobile Core扩展将下载和读取JSON文件。 扩展是可协同工作的单独SDK。 如果向标记资产中添加扩展，则还必须更新应用程序。 如果更改扩展设置或创建规则，则在发布更新的标记库后，这些更改将反映在应用程序中。

下一个： **[安装SDK](install-sdks.md)**

>[!NOTE]
>
>感谢您花时间了解Adobe Experience Platform Mobile SDK。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)