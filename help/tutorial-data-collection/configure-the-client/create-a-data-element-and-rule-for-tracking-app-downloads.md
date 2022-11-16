---
title: 创建用于跟踪应用程序下载的数据元素和规则
description: 创建用于跟踪应用程序下载的数据元素和规则
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 4%

---

# 创建用于跟踪应用程序下载的数据元素和规则

当用户单击 [!UICONTROL 下载应用程序] 链接，则会按如下方式推送到数据层：

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

您使用 `eventInfo` 键，用于告知数据层将此数据与事件一起传输，但 _not_ 在数据层中保留数据。 对于链接点击，将有关已点击链接的信息添加到数据层将没有用处，因为它不适用于页面稍后可能发生的其他事件。

对于此实施，您会向Adobe Experience Platform发送一个体验事件，其中包含(1)数据层的计算状态和(2)的内容的合并结果 `eventInfo`.

为此，您需要创建一个数据元素，以合并这两个信息块。

## 创建数据元素

要创建相应的数据元素，请执行以下操作：

1. 单击 [!UICONTROL 数据元素] 菜单。
1. 接下来，单击 [!UICONTROL 创建新数据元素] 链接。
1. 输入数据元素名称， `computedStateAndEventInfo`.
1. 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL 核心] 如果尚未选择。
1. 对于 [!UICONTROL 数据元素类型] 字段，选择 **[!UICONTROL 合并对象]**. 此数据元素允许您合并多个对象。 合并的结果由数据元素返回。
1. 添加要包含在合并中的第一个对象。 输入 `%event.fullState%` 在 [!UICONTROL 对象（必需）] 字段。 在由 [!UICONTROL 数据推送] 规则事件时，这会引用触发规则时Adobe客户端数据层的计算状态。
1. 单击  **[!UICONTROL 添加其他]** 命令。
1. 添加第二个对象。 输入 `%event.eventInfo%` 在 [!UICONTROL 对象（必需）] 字段。 在由 [!UICONTROL 数据推送] 规则事件，此引用 `eventInfo` 被推送到Adobe客户端数据层的部分。
1. 通过单击 [!UICONTROL 保存] 按钮。
   ![computedStateAndEventInfo数据元素](../assets/computed-state-and-event-info-data-element.png)

数据元素已完成。

## 创建规则

创建用于跟踪 [!UICONTROL 下载应用程序] 链接：

1. 单击 **[!UICONTROL 规则]** 菜单。
1. 单击 **[!UICONTROL Add Rule]**.
1. 输入 **_已点击下载应用程序链接_** 在 [!UICONTROL 名称] 字段。

## 添加事件

1. 单击 **[!UICONTROL 添加]** 按钮 [!UICONTROL 事件]. 您现在可以在事件视图中显示。
1. 对于 [!UICONTROL 扩展] 字段，选择 **[!UICONTROL Adobe客户端数据层]**.
1. 对于 [!UICONTROL 事件类型] 字段，选择 **[!UICONTROL 数据推送]**.
1. 单击 **[!UICONTROL Keep Changes]**.
   ![下载应用程序点击事件](../assets/download-app-clicked-event.png)
因为您只希望在 `downloadAppClicked` 事件推送到数据层，请选择 **[!UICONTROL 特定事件]** 无线电 [!UICONTROL 听] 和类型 **_downloadAppClicked_** 到 [!UICONTROL 要注册的事件/键]  显示的文本字段。

## 添加操作

现在，您又回到了规则视图：

1. 单击[!UICONTROL 操作]下的&#x200B;**[!UICONTROL 添加]**&#x200B;按钮。
1. 此时您应该处于操作视图中。 对于 [!UICONTROL 扩展] 字段，选择 **[!UICONTROL Adobe Experience Platform Web SDK]**. 对于 [!UICONTROL 操作类型] 字段，选择 **[!UICONTROL 发送事件]**.
1. 在 [!UICONTROL 类型] 字段，选择 `web.webinteraction.linkClicks`.
1. 对于 [!UICONTROL XDM数据] 字段中，单击右侧的数据元素选择器按钮并选择 **[!UICONTROL computedStateAndEventInfo]**. 这是您最近创建的数据元素。
1. 对于此规则（与您创建的其他规则不同），请检查 **[!UICONTROL 文档将卸载]** 复选框。
   ![“文档将卸载”复选框](../assets/document-will-unload.png)
1. 通过单击 **[!UICONTROL 保留更改]** 按钮。

>[!TIP]
>
>的 [!UICONTROL 文档将卸载功能] 告知SDK用户在单击链接时离开页面。 这一点很重要，因为即使用户离开页面，SDK也可以发出请求，因为请求会在后台持续运行并到达服务器。 如果未选中此复选框，则不会以此方式发出请求，因此在卸载当前文档时可能会取消该请求。
>
>你可能会问自己，“听起来不错。 那么，为什么不始终启用此选项？”
>
>嗯，这有点复杂，但是使用此功能时，SDK使用名为的浏览器方法 [`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon) 发送请求。 使用 `sendBeacon`，则浏览器不允许SDK（或其他任何内容）访问从服务器返回的任何数据。 如果SDK要对每个请求使用此功能，则SDK将永远无法从服务器接收任何数据。 因此，检查 [!UICONTROL 文档将卸载] 复选框（仅在当前文档将被卸载时），在这种情况下，仍可以丢弃响应数据。

## 保存规则

您的规则现在应该已完成。

1. 单击 **[!UICONTROL 保存]** 中。
   ![下载应用程序链接点击规则](../assets/download-app-link-clicked-rule.png)

[下一个： ](publish-the-library.md)

>[!NOTE]
>
>感谢您花时间学习数据收集。 如果您有任何疑问、想要分享一般反馈或对未来内容提出建议，请就此分享 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)