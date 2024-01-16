---
title: 创建身份
description: 了解如何在XDM中创建身份并使用身份映射数据元素捕获用户ID。 本课程是“使用Web SDK实施Adobe Experience Cloud”教程的一部分。
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# 创建身份

了解如何使用Experience PlatformWeb SDK捕获身份。 在上捕获未经身份验证和经过身份验证的身份数据 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html). 了解如何使用您之前创建的数据元素，通过名为身份映射的Platform Web SDK数据元素类型收集经过身份验证的数据。

Platform Web SDK标记扩展引入了四种新数据元素类型：

1. 事件合并Id
1. 标识映射
1. Variable
1. XDM对象

本课程重点介绍Identity映射数据元素。 您可以将包含经过身份验证的用户ID和身份验证状态的数据元素映射到XDM。

## 学习目标

在本课程结束时，您能够：

* 了解Experience CloudID (ECID)和第一方设备ID之间的区别
* 了解未经身份验证与经过身份验证的ID之间的区别
* 创建身份映射数据元素

## 先决条件

您已了解数据层是什么，对 [Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 数据层，并了解如何引用标记中的数据元素。 您必须在教程中完成以下先前步骤：

* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)

>[!IMPORTANT]
>
>此 [Experience CloudID服务扩展](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 在实施Adobe Experience Platform Web SDK时不需要使用，因为ID服务功能已内置到Platform Web SDK中。

## Experience Cloud ID

此 [Experience CloudID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) 是跨Adobe Experience Platform和Adobe Experience Cloud应用程序使用的共享身份命名空间。 ECID为客户身份奠定了基础，是数字资产的默认身份。 这使ECID成为跟踪未经身份验证的用户行为的理想标识符，因为它始终存在。


<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

详细了解如何 [使用Platform Web SDK跟踪ECID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en).

ECID是使用第一方Cookie和Platform Edge Network的组合设置的。 默认情况下，第一方Cookie由Web SDK设置。 要说明浏览器对Cookie有效期的限制，您可以选择设置和管理自己的第一方Cookie。 这些称为第一方设备ID (FPID)。

## 第一方设备ID (FPID)

FPID是第一方Cookie _您使用自己的Web服务器进行设置_ ，然后该Adobe会使用来设置ECID，而不是使用Web SDK设置的第一方Cookie。 当使用利用DNS A记录（对于IPv4）或AAAA记录（对于IPv6）而不是DNS CNAME或JavaScript代码的服务器设置第一方Cookie时，它们最有效。

设置FPID Cookie后，在收集事件数据时，可以获取其值并将其发送到Adobe。 收集的FPID将用作种子，以在Platform Edge Network上生成ECID，这仍将是Adobe Experience Cloud应用程序中的默认标识符。

详细了解 [Platform Web SDK中的第一方设备ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=zh-Hans)

>[!CAUTION]
>
> FPID是使用Web服务器设置的Cookie生成ECID的替代方法。 它不用于标识经过身份验证的用户。

## 经过身份验证的Id

如上所述，在使用Platform Web SDK时，您数字资产的所有访客都会Adobe分配一个ECID。 这会使ECID成为跟踪未经身份验证的数字行为的默认身份。

您还可以发送经过身份验证的用户ID，以便平台可以创建 [身份图](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs.html?lang=zh-Hans)，Target可以设置其第三方。 这是通过使用 [!UICONTROL 标识映射] 数据元素类型。

要创建 [!UICONTROL 标识映射] 数据元素：

1. 转到 **[!UICONTROL 数据元素]** 并选择 **[!UICONTROL 添加数据元素]**

1. **[!UICONTROL 名称]** 数据元素 `identityMap.loginID`

1. 作为 **[!UICONTROL 扩展名]**，选择 `Adobe Experience Platform Web SDK`

1. 作为 **[!UICONTROL 数据元素类型]**，选择 `Identity map`

1. 这会提示右侧的 **[!UICONTROL 数据收集界面]** 用于配置标识：

   ![数据收集界面](assets/identity-identityMap-setup.png)

1. 作为  **[!UICONTROL 命名空间]**，选择 `lumaCrmId` 您之前在中创建的命名空间 [配置身份](configure-identities.md) 上课。

   >[!NOTE]
   >
   >    如果您没有看到 `lumaCrmId` 命名空间，请确认您还在默认的生产沙盒中创建了该命名空间。 目前，仅在默认生产沙盒中创建的命名空间才会显示在命名空间下拉列表中。

1. 在 **[!UICONTROL 命名空间]** ，则必须设置ID。 选择 `user.profile.attributes.username` 之前在中创建的数据元素 [创建数据元素](create-data-elements.md#create-data-elements-to-capture-the-data-layer) 课程，用于在用户登录Luma网站时捕获ID。

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. 作为 **[!UICONTROL 已验证状态]**，选择 **[!UICONTROL 已验证]**
1. 选择 **[!UICONTROL 主要]**

1. 选择 **[!UICONTROL 保存]**

   ![数据收集界面](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe建议发送代表个人的身份，例如 `Luma CRM Id`，作为 [!UICONTROL 主要] 身份。
>
> 如果身份映射包含人员标识符(例如， `Luma CRM Id`)，则人员标识符将变为 [!UICONTROL 主要] 身份。 否则， `ECID` 变为 [!UICONTROL 主要] 身份。




<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

在这些步骤结束时，您应该创建以下数据元素：

| 核心扩展数据元素 | Platform Web SDK数据元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.variable.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

设置这些数据元素后，您即可在标记中创建规则，开始通过XDM对象向Platform Edge Network发送数据。

[下一步： ](create-tag-rule.md)

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此共享它们 [Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
