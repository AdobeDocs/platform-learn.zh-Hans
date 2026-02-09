---
title: 为Platform Web SDK创建身份
description: 了解如何在XDM中创建身份并使用身份映射数据元素捕获用户ID。 本课程是《使用 Web SDK 实施 Adobe Experience Cloud》教程的一部分。
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 3%

---

# 创建身份

了解如何使用 Adobe Experience Platform Web SDK 捕获身份标识。捕获[Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html)上未经身份验证和经过身份验证的标识数据。 了解如何使用您之前创建的数据元素，通过名为身份映射的Platform Web SDK数据元素类型收集经过身份验证的数据。

本课程将重点介绍Adobe Experience Platform Web SDK标记扩展中可用的身份映射数据元素。 您可以将包含经过身份验证的用户ID和身份验证状态的数据元素映射到XDM。


>[!WARNING]
>
> 本教程中使用的Luma网站预计将在2026年2月16日这一周内被替换。 作为本教程的一部分完成的工作可能不适用于新网站。

## 学习目标

在本课程结束时，您能够：

* 了解Experience Cloud ID (ECID)和第一方设备ID (FPID)之间的关系
* 了解未经身份验证与经过身份验证的ID之间的区别
* 创建身份映射数据元素

## 先决条件

您了解数据层是什么，熟悉[Luma演示站点](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}数据层，并了解如何在标记中引用数据元素。 您必须完成本教程中之前的课程：

* [配置XDM架构](configure-schemas.md)
* [配置身份命名空间](configure-identities.md)
* [配置数据流](configure-datastream.md)
* [Web SDK扩展安装在标记属性中](install-web-sdk.md)
* [创建数据元素](create-data-elements.md)


## Experience Cloud ID

[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/ecid)是跨Adobe Experience Platform和Adobe Experience Cloud应用程序使用的共享身份命名空间。 ECID为客户身份奠定了基础，是数字资产的默认身份。 ECID是跟踪未经身份验证的用户行为的理想标识符，因为它始终存在。

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

详细了解如何使用Platform Web SDK[跟踪](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview)ECID。

ECID是使用第一方Cookie和平台Edge Network的组合设置的。 默认情况下，第一方身份Cookie由Web SDK在客户端设置。 要说明浏览器对Cookie生命周期的限制，您可以选择改为在服务器端设置您自己的第一方身份Cookie。 这些身份Cookie称为第一方设备ID (FPID)。

>[!IMPORTANT]
>
>实施Adobe Experience Platform Web SDK时不需要[Experience Cloud ID服务扩展](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension)，因为ID服务功能已内置到Platform Web SDK中。

## 第一方设备ID (FPID)

FPID是使用您自己的Web服务器&#x200B;_设置的第一方Cookie_，Adobe随后会使用这些服务器创建ECID，而不是使用Web SDK设置的第一方Cookie。 虽然浏览器支持可能有所不同，但由利用DNS A记录（对于IPv4）或AAAA记录（对于IPv6）的服务器设置的第一方Cookie往往比由DNS CNAME或JavaScript代码设置时更持久。

设置FPID Cookie后，在收集事件数据时，可以获取其值并将其发送到Adobe。 收集的FPID将用作种子，以在Platform Edge Network上生成ECID，这仍将是Adobe Experience Cloud应用程序中的默认标识符。

虽然本教程中未使用FPID，但建议您在自己的网络SDK实施中使用FPID。 阅读有关Platform Web SDK中的[第一方设备ID的详细信息](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> FPID是使用Web服务器设置的Cookie生成ECID的替代方法。 它不用于标识经过身份验证的用户。

## 经过身份验证的Id

如上所述，在使用Platform Web SDK时，Adobe会为您数字财产的所有访客分配一个ECID。 ECID是用于跟踪未经身份验证的数字行为的默认身份。

您还可以发送经过身份验证的用户ID，以便平台可以创建[身份图](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs)，并且Target可以设置其[第三方ID](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/3rd-party-id)。 通过使用[!UICONTROL 标识映射]数据元素类型来设置经过身份验证的ID。

要创建[!UICONTROL 标识映射]数据元素：

1. 转到&#x200B;**[!UICONTROL 数据元素]**&#x200B;并选择&#x200B;**[!UICONTROL 添加数据元素]**

1. **[!UICONTROL Name]**&#x200B;数据元素`identityMap.loginID`

1. 对于&#x200B;**[!UICONTROL 扩展]**，请选择`Adobe Experience Platform Web SDK`

1. 作为&#x200B;**[!UICONTROL 数据元素类型]**，请选择`Identity map`

1. 这会在&#x200B;**[!UICONTROL 数据收集界面]**&#x200B;的右侧提示屏幕区域，以便您配置标识：

   ![数据收集接口](assets/identity-identityMap-setup.png)

1. 作为&#x200B;**[!UICONTROL 命名空间]**，请选择您之前在`lumaCrmId`配置身份[课程中创建的](configure-identities.md)命名空间。 如果下拉列表中未显示该变量，请键入该变量。

1. 选择&#x200B;**[!UICONTROL 命名空间]**&#x200B;后，必须设置ID。 选择之前在`user.profile.attributes.username`创建数据元素[课程中创建的](create-data-elements.md#create-data-elements-to-capture-the-data-layer)数据元素，该数据元素可在用户登录Luma网站时捕获ID。

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. 作为&#x200B;**[!UICONTROL Authenticated状态]**，请选择&#x200B;**[!UICONTROL Authenticated]**
1. 选择&#x200B;**[!UICONTROL 主要]**

1. 选择&#x200B;**[!UICONTROL 保存]**

   ![数据收集接口](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe建议将代表人员（如`Luma CRM Id`）的标识作为[!UICONTROL primary]标识发送。
>
> 如果身份映射包含人员标识符（例如，`Luma CRM Id`），则人员标识符将变为[!UICONTROL 主]身份。 否则，`ECID`将成为[!UICONTROL 主]标识。




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

| 核心扩展数据元素 | Platform Web SDK扩展数据元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `identityMap.loginID` |
| `cart.productInfo.purchase` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

设置这些数据元素后，您可以通过在Tags中创建规则来开始向Platform Edge Network发送数据。

>[!NOTE]
>
>感谢您投入时间学习Adobe Experience Platform Web SDK。 如果您有疑问、希望分享一般反馈或有关于未来内容的建议，请在此[Experience League社区讨论帖子](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享这些内容
