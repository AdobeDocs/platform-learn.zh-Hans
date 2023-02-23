---
title: 使用Web SDK验证Target实施 |将Target从at.js 2.x迁移到Web SDK
description: 了解如何使用Adobe Experience Platform Web SDK验证活动并调试Adobe Target实施。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# 验证平台Web SDK实施

将Target实施从at.js迁移到Platform Web SDK后，在将任何更改发布到生产网站之前，务必要验证一切工作正常。 Adobe建议执行以下操作，此页面将详细介绍以下内容：

* 执行技术验证，以确保基本实施以及Platform Web SDK请求和响应看起来正确
* 确保正确交付和渲染Target活动
* 检查报表是否正常工作
* 重新访问受众和配置文件脚本，以确保它们与Platform Web SDK兼容
* 确保与Adobe或第三方应用程序的集成正常工作

每个Target实施都会因站点架构和所使用的功能而异。 您可以将下表用作起点，并添加实施特有的任何项目。 的 [“调试”页](debugging.md) 在本教程中，您将看到可用于帮助进行此验证的工具。

## 技术验证

| 验证项 | 注释 |
|---|---|
| 页面上不再存在at.js预隐藏代码片段 | Platform Web SDK不会自动删除具有ID的样式 `at-body-style`. 将此旧代码片段保留在页面上会导致隐藏内容，直到达到代码片段超时为止。 |
| 页面上不再存在at.js库 | 检查浏览器的开发人员工具控制台中是否没有“adobe.target”对象。 同时包含Platform Web SDK和at.js会导致意外的呈现行为 |
| 预期参数位于的XDM和数据对象中 `sendEvent` 请求 |  |
| 如果使用页面请求填充目录，则Recommendations目录会按预期进行更新 |  |
| 配置文件参数已成功传递到Target | 在Debugger中查看边缘跟踪 |
| 数据流映射器中映射到XDM的参数已正确传递到Target | 使用Debugger和/或保证的“边缘跟踪”功能进行验证 |
| 目标内容在适用的 `sendEvent` 响应 | 预期时间 `renderDecisions` 选项设置为 `true` 请求或作用域，且用户符合特定Target活动的条件 |
| A `decisioning.propositionDisplay` 基于VEC的活动渲染后，会触发事件 | 自动呈现的活动和按需呈现的活动应具有单独的事件调用 |
| A `decisioning.propositionDisplay` 事件在基于表单的活动渲染后触发 | 仅适用于某些实施。 需要自定义代码才能执行此调用。 |
| A `decisioning.propositionDisplay` 对SPA视图更改应用选件时触发事件 | 仅适用于SPA实施 |
| A `decisioning.propositionDisplay` 为给定视图重新渲染SPA组件时，不会触发事件 | 仅适用于SPA实施 |
| A `decisioning.propsitionInteract` 活动转换后触发事件 | “已单击元素”和自定义转化已从at.js迁移 `trackEvent` 或 `sendNotifications` 应具有单独的事件调用 |
| 在 `sendEvent` 响应和具有预期值 | 响应令牌应在Web SDK中正常工作 |
| 使用Web SDK和at.js时，各个页面中的ECID都保持一致 | 适用于逐页迁移。 这些类型的迁移中不应使用重定向选件 |


## 活动交付和渲染

| 验证项 | 注释 |
|---|---|
| 在页面加载时，基于VEC的活动可正确呈现 | 最好验证自定义代码修改和基本修改（如重新排列元素或替换文本） |
| 基于VEC的活动在SPA视图更改时正确呈现 | 仅适用于SPA实施 |
| 基于表单的活动可正确呈现 | 仅适用于某些实施。 呈现基于表单的活动需要与at.js类似的自定义代码。 |
| 使用重定向的活动可正常工作 | 如果源页面和目标页面都使用Platform Web SDK，则支持重定向。 不支持从at.js页面重定向到平台Web SDK页面或以相反的方式重定向。 |
| 使用远程选件的活动可正常工作 | 不常见，请检查Target选件清单以查找远程选件 |
| 适当地缓解了闪烁 | 闪烁处理是可选的，但请确保您已实施的任何缓解策略均可按预期运行，以获得最佳页面性能和用户体验 |
| QA链接可按预期工作 | 如果不起作用，请确认web.webPageDetails.URL与浏览器中的URL完全匹配 |
| 您所有常用的选件类型都会按预期呈现 |  |

## 报告

| 验证项 | 注释 |
|---|---|
| 访客被归因于基于VEC的活动 | 最好验证报表在页面加载修改和SPA视图修改中是否可按预期工作 |
| 访客被归因于基于表单的活动 | 根据使用的渲染方法，您的实施可能需要自定义代码来执行 `decisioning.propositionDisplay` 事件 |
| 可正确捕获标准转化目标 | 适用于Target或Analytics作为报表源 |
| 正确捕获了订单转化和详细信息 | 检查审核报告 |
| 可正确捕获点击跟踪转化 |  |
| 正确捕获了自定义转化目标 | 例如，转化目标从at.js中迁移 `trackEvent` 或 `sendNotifications` ，通常与“已查看的mbox”目标一起使用 |

## 受众和配置文件脚本

| 验证项 | 注释 |
|---|---|
| 实时活动中使用的受众与Platform Web SDK兼容 | 必须更新使用“自定义”（mbox参数）组件的受众，以包含XDM属性 |
| 所有配置文件脚本都与Platform Web SDK兼容 | 必须更新使用mbox参数的任何配置文件脚本，以包含XDM属性 |
| 目标受众的活动返回 | 最好对您修改的受众执行端到端验证，以使其与Platform Web SDK兼容 |
| 配置文件脚本会按预期进行评估 | 在Debugger中查看边缘跟踪 |

## 与Adobe应用程序集成

| 验证项 | 注释 |
|---|---|
| Experience Cloud受众的活动返回 | 例如，从Adobe Analytics发布的区段 |
| Experience Platform受众的活动返回 | 仅当您拥有基于Experience Platform的应用程序（如RTCDP）的许可证时才适用 |
| Audience Manager受众的活动返回 | 例如，基于访问特定页面的区段 |
| Target活动数据显示在Analysis Workspace中 | 适用于使用Adobe Analytics作为报表源的活动 |

## 与第三方应用程序集成

| 验证项 | 注释 |
|---|---|
| 响应令牌数据已正确传递到第三方应用程序 | 集成方法可能有所不同，但常见的方法是使用Target响应令牌将活动和体验信息传递给其他分析工具，如Google Analytics |
| 来自第三方的信息将作为XDM或用户档案数据进行传递 | 第三方提供的所有相关信息均应传入 `sendEvent` Target调用 |

执行上述验证步骤后，您可以确信Platform Web SDK实施已准备好迁移到生产环境。

接下来，了解如何 [使用Platform Web SDK实施Target故障诊断](debugging.md).

>[!NOTE]
>
>我们致力于帮助您成功将Target从at.js迁移到Web SDK。 如果您在迁移过程中遇到障碍，或感觉本指南中缺少关键信息，请在中发布以告知我们 [此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).