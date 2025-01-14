---
title: 创建变量数据元素
description: 添加将根据多个规则构建的数据元素，然后将其发送到Edge Network并转发到Adobe Analytics
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16759
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 创建变量数据元素

添加将根据多个规则构建的数据元素，然后将其发送到Edge Network并转发到Adobe Analytics。

此数据元素将创建“数据”对象，该数据对象将用于将Adobe Analytics变量（prop、eVar、event等）传递回Adobe Analytics和Adobe Target。 因此，就像在Analytics的AppMeasurement实施中构建“s对象”一样，我们将构建以下类型：要跨规则访问和更新的变量对象，并且可用于将prop和eVar填充到Analytics中。

1. 在数据收集界面中，单击左侧导航栏中的&#x200B;**数据元素**。

   您将转到数据元素登录页面，在该页面中，您将看到所有预先存在的数据元素。 我们需要创建一个新的数据元素来促进迁移。 单击&#x200B;**添加数据元素**。

   ![添加数据元素](assets/add-new-data-alement.jpg)

1. 配置数据元素。
   1. 随意命名数据元素 — 这有助于您记住这是在您的页面上构建数据，并且这将会是“变量”类型。 在本教程中，我们将它称为&#x200B;**页面查看数据变量**。
   1. 从“扩展”下拉列表中选择&#x200B;**Adobe Experience Platform Web SDK**。
   1. 从&#x200B;**数据元素类型**&#x200B;下拉列表中选择&#x200B;**变量**。
   1. 在右侧面板中，选择&#x200B;**数据**&#x200B;单选按钮。
   1. 查看&#x200B;**Adobe Analytics**&#x200B;解决方案以及要迁移的其他任何解决方案，例如，此屏幕快照中显示的&#x200B;**Adobe Target**。
1. 单击&#x200B;**保存**。

   ![配置变量数据元素](assets/configure-variable-data-element.jpg)
