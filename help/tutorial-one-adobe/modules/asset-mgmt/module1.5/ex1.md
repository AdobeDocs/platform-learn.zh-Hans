---
title: Adobe Commerce as a Cloud Service快速入门
description: Adobe Commerce as a Cloud Service快速入门
kt: 5342
doc-type: tutorial
exl-id: 8603c8e2-c3ba-4976-9703-cef9e63924b8
source-git-commit: 7280f6b7d3579226f2d8c7f94e75ca8d3f2941cc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 1.5.1 Adobe Commerce as a Cloud Service快速入门

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 确保您处于正确的环境，该环境应名为`--aepImsOrgName--`。 单击&#x200B;**Commerce**。

![AEM Assets](./images/accs1.png)

## 1.5.1.1创建您的ACCS实例

您应该会看到此内容。 单击&#x200B;**+添加实例**。

![AEM Assets](./images/accs2.png)

填写以下字段：

- **实例名称**： `--aepUserLdap-- - ACCS`
- **环境**： `Sandbox`
- **地区**： `North America`

单击&#x200B;**添加实例**。

![AEM Assets](./images/accs3.png)

您即将创建的实例。 这可能需要5-10分钟。

![AEM Assets](./images/accs4.png)

实例准备就绪后，单击您的实例以将其打开。

![AEM Assets](./images/accs5.png)

## 1.5.1.2设置您的CitiSignal商店

您应该会看到此内容。 单击&#x200B;**使用Adobe ID登录**，然后登录。

![AEM Assets](./images/accs6.png)

登录后，您应该会看到此主页。 第一步是在Commerce建立CitiSignal商店。 单击&#x200B;**商店**。

![AEM Assets](./images/accs7.png)

单击&#x200B;**所有商店**。

![AEM Assets](./images/accs8.png)

单击&#x200B;**创建网站**。

![AEM Assets](./images/accs9.png)

填写以下字段：

- **名称**： `CitiSignal`
- **代码**： `citisignal`

单击&#x200B;**保存网站**。

![AEM Assets](./images/accs10.png)

那你就该回到这里来。 单击&#x200B;**创建存储**。

![AEM Assets](./images/accs11.png)

填写以下字段：

- **网站**： `CitiSignal`
- **名称**： `CitiSignal`
- **代码**： `citisignal`
- **根类别**： `Default Category`

单击&#x200B;**保存存储**。

![AEM Assets](./images/accs12.png)

那你就该回到这里来。 单击&#x200B;**创建商店视图**。

![AEM Assets](./images/accs13.png)

填写以下字段：

- **存储**： `CitiSignal`
- **名称**： `CitiSignal`
- **代码**： `citisignal`
- **状态**： `Enabled`

单击&#x200B;**保存商店视图**。

![AEM Assets](./images/accs14.png)

然后，您应该会看到此消息。 单击&#x200B;**确定**。

![AEM Assets](./images/accs15.png)

那你就该回到这里来。 单击&#x200B;**CitiSignal**&#x200B;网站以将其打开。

![AEM Assets](./images/accs16.png)

选中此复选框可将此网站设置为默认网站。

单击&#x200B;**保存网站**。

![AEM Assets](./images/accs16a.png)

那你就该回到这里来。

![AEM Assets](./images/accs16.png)

## 1.5.1.3配置类别和产品

转到&#x200B;**目录**，然后选择&#x200B;**类别**。

![AEM Assets](./images/accs17.png)

选择&#x200B;**默认类别**，然后单击&#x200B;**添加子类别**。

![AEM Assets](./images/accs18.png)

输入名称`Phones`，然后单击&#x200B;**保存**。

![AEM Assets](./images/accs19.png)

选择&#x200B;**默认类别**，然后再次单击&#x200B;**添加子类别**。

![AEM Assets](./images/accs20.png)

输入名称`Watches`，然后单击&#x200B;**保存**。

![AEM Assets](./images/accs21.png)

然后，您应该创建2个类别。

![AEM Assets](./images/accs22.png)

接下来，转到&#x200B;**目录**，然后选择&#x200B;**产品**。

![AEM Assets](./images/accs23.png)

您应该会看到此内容。 单击&#x200B;**添加产品**。

![AEM Assets](./images/accs24.png)

配置您的产品，如下所示：

- **产品名称**： `iPhone Air`
- **SKU**： `iPhone-Air`
- **价格**： `999`
- **数量**： `10000`
- **类别**：选择`Phones`

单击&#x200B;**保存**。

![AEM Assets](./images/accs25.png)

向下滚动到&#x200B;**配置**&#x200B;并单击&#x200B;**创建配置**。

![AEM Assets](./images/accs26.png)

您应该会看到此内容。 单击&#x200B;**新建属性**。

![AEM Assets](./images/accs27.png)

将&#x200B;**默认标签**&#x200B;设置为`Storage`，然后单击&#x200B;**管理选项**&#x200B;下的&#x200B;**添加选项**。

![AEM Assets](./images/accs28.png)

在所有3列中使用名称`256GB`配置第一个选项，然后再次单击&#x200B;**添加选项**。

![AEM Assets](./images/accs29.png)

在所有3列中使用名称`512GB`配置第二个选项，然后再次单击&#x200B;**添加选项**。

![AEM Assets](./images/accs30.png)

在所有3列中使用名称`1TB`配置第三个选项。

![AEM Assets](./images/accs31.png)

向下滚动到&#x200B;**店面属性**。 将以下选项设置为&#x200B;**是**：

- **在搜索中使用**
- **允许Storefront上的HTML标签**
- **在店面的目录页面上可见**
- **在产品列表中使用**

![AEM Assets](./images/accs32.png)

向上滚动并单击&#x200B;**保存属性**。

![AEM Assets](./images/accs33.png)

您应该会看到此内容。 选择&#x200B;**颜色**&#x200B;和&#x200B;**存储**&#x200B;的两个属性，然后单击&#x200B;**下一步**。

![AEM Assets](./images/accs34.png)

您应该会看到此内容。 您现在需要添加可用的颜色选项。 为此，请单击&#x200B;**创建新值**。

![AEM Assets](./images/accs35.png)

输入值`Sky-Blue`并单击&#x200B;**创建新值**。

![AEM Assets](./images/accs36.png)

输入值`Light-Gold`并单击&#x200B;**创建新值**。

![AEM Assets](./images/accs37.png)

输入值`Cloud-White`并单击&#x200B;**创建新值**。

![AEM Assets](./images/accs38.png)

输入值`Space-Black`。 单击&#x200B;**全选**

![AEM Assets](./images/accs39.png)

选择&#x200B;**存储**&#x200B;下的全部3个选项，然后单击&#x200B;**下一步**。

![AEM Assets](./images/accs40.png)

保留默认设置，然后单击&#x200B;**下一步**。

![AEM Assets](./images/accs41.png)

您应该会看到此内容。 单击&#x200B;**生成产品**。

![AEM Assets](./images/accs42.png)

将每个产品的&#x200B;**数量**&#x200B;设置为`10000`。 单击&#x200B;**保存**。

![AEM Assets](./images/accs43.png)

向下滚动到Websites **中的**&#x200B;产品，并选中&#x200B;**CitiSignal**&#x200B;的复选框。

单击&#x200B;**保存**。

![AEM Assets](./images/accs44.png)

单击&#x200B;**确认**。

![AEM Assets](./images/accs45.png)

您应该会看到此内容。 单击&#x200B;**上一步**。

![AEM Assets](./images/accs46.png)

您现在可以在产品目录中看到产品&#x200B;**iPhone Air**&#x200B;及其变体。

![AEM Assets](./images/accs47.png)

下一步：[将ACCS连接到AEM Sites CS/EDS店面](./ex2.md){target="_blank"}

返回[Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
