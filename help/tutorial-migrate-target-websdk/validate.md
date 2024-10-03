---
title: 使用Web SDK验证Target实施 — 将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Adobe Experience Platform Web SDK验证活动并调试Adobe Target实施。
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# 验证平台Web SDK实施

将Target实施从at.js迁移到Platform Web SDK后，请务必先验证所有内容是否正常运行，然后再将任何更改发布到生产站点。 Adobe建议采取以下措施，本页将详细介绍这些措施：

* 执行技术验证，以确保基本实施以及Platform Web SDK请求和响应看起来正确
* 确保Target活动已正确交付和呈现
* 检查报表是否正常工作
* 重新访问受众和配置文件脚本，以确保它们与Platform Web SDK兼容
* 确保与Adobe或第三方应用程序的集成正常工作

每个Target实施都因使用的站点架构和功能而异。 您可以使用下表作为起点，并添加任何特定于您的实施的项目。 本教程的[调试页面](debugging.md)显示了可用于帮助完成此验证的工具。

## 技术验证

| 验证项 | 注释 |
|---|---|
| 页面上不再存在at.js预隐藏代码片段 | Platform Web SDK不会自动删除ID为`at-body-style`的样式。 将此旧代码片段保留在页面上会导致隐藏内容，直到达到代码片段超时为止。 |
| 页面上不再存在at.js库 | 检查浏览器的开发人员工具控制台中是否没有“adobe.target”对象。 同时包含Platform Web SDK和at.js会导致意外的渲染行为 |
| `sendEvent`请求的XDM和数据对象中需要参数 | |
| 如果使用页面请求填充目录，则Recommendations目录会按预期更新 | |
| 配置文件参数已成功传递到Target | 在Debugger中查看Edge跟踪 |
| 数据流映射器中映射到XDM的参数将正确传递给Target | 使用Debugger的Edge跟踪功能和/或Assurance进行验证 |
| 目标内容在适用的`sendEvent`响应中返回 | 当`renderDecisions`选项设置为`true`或请求了范围并且用户符合特定Target活动的资格时，应当使用此选项 |
| 基于VEC的活动渲染后，`decisioning.propositionDisplay`事件触发 | 自动和按需呈现的活动应具有单独的事件调用 |
| 在基于表单的活动渲染后，`decisioning.propositionDisplay`事件触发 | 仅适用于某些实施。 需要自定义代码才能执行此调用。 |
| 将选件应用于SPA视图更改时，将触发`decisioning.propositionDisplay`事件 | 仅适用于SPA实施 |
| 当SPA组件重新渲染给定视图时，`decisioning.propositionDisplay`事件不会触发 | 仅适用于SPA实施 |
| 在活动转换之后，`decisioning.propsitionInteract`事件触发 | 从at.js `trackEvent`或`sendNotifications`迁移的“已单击元素”和自定义转化应具有单独的事件调用 |
| 响应令牌在`sendEvent`响应中返回，并且具有预期值 | 响应令牌应可在Web SDK中正常运行 |
| 使用Web SDK和at.js的页面中，ECID保持一致 | 适用于逐页迁移。 重定向选件不适用于这些类型的迁移 |


## 活动交付和呈现

| 验证项 | 注释 |
|---|---|
| 基于VEC的活动在页面加载时正确呈现 | 最好同时验证自定义代码修改和基本修改，例如重新排列元素或替换文本 |
| 基于VEC的活动在SPA视图更改时正确呈现 | 仅适用于SPA实施 |
| 基于表单的活动可正确呈现 | 仅适用于某些实施。 渲染基于表单的活动需要类似于at.js的自定义代码。 |
| 使用重定向的活动可正常工作 | 如果源页面和目标页面都使用Platform Web SDK，则支持重定向。 不支持从at.js页面重定向到Platform Web SDK页面或反之亦然。 |
| 使用远程选件的活动可正常工作 | 不常见，请检查您的Target选件库存中的远程选件 |
| 已适当缓解闪烁 | 处理闪烁是可选的，但请确保您制定的任何缓解策略均可按预期发挥最佳页面性能和用户体验 |
| QA链接按预期工作 | 如果不起作用，请确认web.webPageDetails.URL与浏览器中的URL完全匹配 |
| 所有常用的选件类型都会按预期呈现 |  |

## 报告

| 验证项 | 注释 |
|---|---|
| 访客归属于基于VEC的活动 | 最好验证报表能否在页面加载修改和SPA视图修改中按预期工作 |
| 访客归属于基于表单的活动 | 根据使用的渲染方法，您的实施可能需要自定义代码才能执行`decisioning.propositionDisplay`事件 |
| 正确捕获标准转化目标 | 适用于Target或Analytics作为报表源 |
| 正确捕获订单转化和详细信息 | 检查审计报告 |
| 正确捕获点击跟踪转化 |  |
| 正确捕获自定义转化目标 | 例如，转化目标已从at.js `trackEvent`或`sendNotifications`迁移，这些目标通常与“已查看mbox”目标一起使用 |

## 受众和配置文件脚本

| 验证项 | 注释 |
|---|---|
| 实时活动中使用的受众与Platform Web SDK兼容 | 必须更新使用“自定义”（mbox参数）组件的受众以包含XDM属性 |
| 所有配置文件脚本与Platform Web SDK兼容 | 必须更新任何使用mbox参数的配置文件脚本以包含XDM属性 |
| 针对Target受众返回的活动 | 最好对您修改为与Platform Web SDK兼容的受众执行端到端验证 |
| 配置文件脚本按预期进行计算 | 在Debugger中查看Edge跟踪 |

## 与Adobe应用程序集成

| 验证项 | 注释 |
|---|---|
| 活动会返回Experience Cloud受众 | 例如，从Adobe Analytics发布的区段 |
| 活动会返回Experience Platform受众 | 仅当您具有基于Experience Platform的应用程序（如RTCDP）的许可证时才适用 |
| 活动会返回Audience Manager受众 | 例如，基于访问特定页面的区段 |
| Target活动数据显示在Analysis Workspace中 | 适用于使用Adobe Analytics作为报表源的活动 |

## 与第三方应用程序的集成

| 验证项 | 注释 |
|---|---|
| 响应令牌数据正确传递到第三方应用程序 | 集成方法可能有所不同，但一种常见方法是使用Target响应令牌将活动和体验信息传递给Google Analytics等其他分析工具 |
| 来自第三方的信息作为XDM或用户档案数据传递 | 应将来自第三方的所有相关信息传递到`sendEvent`对Target的调用 |

执行上述验证步骤后，您可以放心，Platform Web SDK实施已准备好投入生产。

接下来，了解如何[使用Platform Web SDK](debugging.md)对Target实施进行故障排除。

>[!NOTE]
>
>我们致力于帮助您成功完成从at.js到Web SDK的Target迁移。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
