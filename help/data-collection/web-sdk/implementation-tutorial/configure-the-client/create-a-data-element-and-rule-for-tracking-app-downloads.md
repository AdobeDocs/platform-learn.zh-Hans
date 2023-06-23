---
title: 创建用于跟踪应用程序下载的数据元素和规则
description: 创建用于跟踪应用程序下载的数据元素和规则
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# 创建用于跟踪应用程序下载的数据元素和规则

提醒一下，当用户单击 [!UICONTROL 下载应用程序] 链接时，您按如下方式推送到Data Layer：

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

您已使用 `eventInfo` key，它告知数据层将数据与事件进行通信，但 _非_ 将数据保留在数据层中。 对于链接点击，将有关已点击链接的信息添加到数据层没有用处，因为它不适用于稍后页面上可能出现的其他事件。

对于此实施，您将向Adobe Experience Platform发送一个体验事件，其中包含由(1)数据层的计算状态和(2)内容合并而成的结果。 `eventInfo`.

要实现此目的，您首先需要创建一个数据元素，以合并这两块信息。

## 创建数据元素

要创建适当的数据元素，请单击 [!UICONTROL 数据元素] 在左侧菜单中。 接下来，单击 [!UICONTROL 添加数据元素] 链接。

对于数据元素名称，输入 `computedStateAndEventInfo`. 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL 核心] 如果尚未选择，则为。 对于 [!UICONTROL 数据元素类型] 字段，选择 [!UICONTROL 合并的对象]. 此数据元素允许您深度合并多个对象。 合并的结果由数据元素返回。

对于要包含在合并中的第一个对象，输入 `%event.fullState%`. 在由触发的规则中使用 [!UICONTROL 推送的数据] 规则事件，这将引用Adobe客户端数据层在触发规则时的计算状态。

单击 [!UICONTROL 添加其他].

对于第二个对象，输入 `%event.eventInfo%`. 在由触发的规则中使用 [!UICONTROL 推送的数据] 规则事件，这会引用 `eventInfo` 推送到Adobe客户端数据层的部分。

![computedStateAndEventInfo数据元素](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

数据元素已完成。 通过单击 [!UICONTROL 保存] 按钮。

## 创建规则

要创建规则以跟踪对 [!UICONTROL 下载应用程序] 链接，首次点击 [!UICONTROL 规则] 在左侧菜单中。

单击 [!UICONTROL Add Rule].

对于规则名称，输入 _已单击下载应用程序链接_.

## 添加事件

单击 [!UICONTROL 添加] 按钮位于 [!UICONTROL 事件]. 您现在显示在事件视图中。 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL Adobe客户端数据层]. 对于 [!UICONTROL 事件类型] 字段，选择 [!UICONTROL 推送的数据].

因为您只希望此规则在 `downloadAppClicked` 事件被推送到数据层，选择 [!UICONTROL 特定事件] 下的无线电 [!UICONTROL 收听] 和类型 _downloadAppClick_ 到 [!UICONTROL 要注册的事件/密钥]  显示的文本字段。

![下载应用程序点击事件](../../../assets/implementation-strategy/download-app-clicked-event.png)

单击 [!UICONTROL Keep Changes].

## 添加操作

现在，您已返回规则视图，请单击 [!UICONTROL 添加] 按钮位于 [!UICONTROL 操作]. 现在，您应位于操作视图中。 对于 [!UICONTROL 扩展] 字段，选择 [!UICONTROL Adobe Experience Platform Web SDK]. 对于 [!UICONTROL 操作类型] 字段，选择 [!UICONTROL 发送事件].

在屏幕的右侧，找到 [!UICONTROL 类型] 字段并选择 `web.webinteraction.linkClicks`.

对于 [!UICONTROL XDM数据] 字段中，单击数据元素选择器按钮并选择 [!UICONTROL computedStateAndEventInfo]. 这是您刚刚创建的数据元素。

对于此规则（与您创建的其他规则不同），您将检查 [!UICONTROL 文档将卸载] 复选框。 这基本上告知SDK，当用户单击链接时，用户将离开页面。 这一点非常重要，因为它允许SDK发出请求，以便即使用户离开页面，请求仍将继续在后台运行并到达服务器。 如果未选中此复选框，则不会以这种方式发出请求，因此当当前文档卸载时，可能会取消请求。

你可能会问自己，“听起来不错。 为什么没有始终启用此选项？”

嗯，这有点复杂，但使用此功能时，SDK会使用名为的浏览器方法 [`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon) 以发送请求。 使用发送请求时 `sendBeacon`，浏览器不允许SDK（或其他任何内容）访问从服务器返回的任何数据。 如果SDK要针对每个请求使用此功能，则SDK将永远无法从服务器接收任何数据。 因此，请务必检查 [!UICONTROL 文档将卸载] 仅当当前文档将卸载时才会选中此复选框，在这种情况下，仍可以丢弃响应数据。

![“文档将卸载”复选框](../../../assets/implementation-strategy/document-will-unload.png)

单击 [!UICONTROL 保留更改] 按钮。

## 保存规则

您的规则现在应已完成。

![下载应用程序链接点击规则](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

通过单击保存规则 [!UICONTROL 保存].
