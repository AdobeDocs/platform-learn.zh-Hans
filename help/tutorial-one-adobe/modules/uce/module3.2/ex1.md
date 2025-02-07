---
title: AJO翻译服务快速入门
description: AJO翻译服务快速入门
kt: 5342
doc-type: tutorial
exl-id: ee0b8650-a59f-4888-8228-4caafe4143e4
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 3.2.1翻译提供程序

## 3.2.1.1配置Microsoft Azure Translator

转到[https://portal.azure.com/#home](https://portal.azure.com/#home)。

![翻译](./images/transl1.png)

在搜索栏中输入`translators`。 然后，单击&#x200B;**+创建**。

![翻译](./images/transl2.png)

选择&#x200B;**创建转换器**。

![翻译](./images/transl3.png)

选择您的&#x200B;**订阅ID**&#x200B;和&#x200B;**资源组**。
将**区域**&#x200B;设置为&#x200B;**全局**。
将**定价层**&#x200B;设置为&#x200B;**免费F0**。

选择&#x200B;**审阅+创建**。

![翻译](./images/transl4.png)

选择&#x200B;**创建**。

![翻译](./images/transl5.png)

选择&#x200B;**转到资源**。

![翻译](./images/transl6.png)

在左侧菜单中，转到&#x200B;**资源管理** > **密钥和终结点**。 单击以复制密钥。

![翻译](./images/transl7.png)

## 3.2.1.2语言环境词典

转到[https://experience.adobe.com/](https://experience.adobe.com/)。 单击&#x200B;**Journey Optimizer**。

![翻译](./images/ajolp1.png)

在左侧菜单中，转到&#x200B;**翻译**，然后转到&#x200B;**区域设置词典**。 如果看到此消息，请单击&#x200B;**添加默认区域设置**。

![翻译](./images/locale1.png)

您应该会看到此内容。

![翻译](./images/locale2.png)

## 3.2.1.3在AJO中配置翻译提供程序

转到[https://experience.adobe.com/](https://experience.adobe.com/)。 单击&#x200B;**Journey Optimizer**。

![翻译](./images/ajolp1.png)

在左侧菜单中，转到&#x200B;**翻译**，然后转到&#x200B;**提供程序**。 单击&#x200B;**添加提供程序**。

![翻译](./images/transl8.png)

在&#x200B;**提供程序**&#x200B;下，选择&#x200B;**Microsoft Translator**。 选中此复选框可启用翻译提供商的使用。 粘贴您从Microsoft Azure转换器复制的密钥。 然后单击&#x200B;**验证凭据**。

![翻译](./images/transl9.png)

随后，您的凭据应会被成功验证。 如果是，请向下滚动以选择要翻译的语言。

![翻译](./images/transl10.png)

确保选择`[en-US] English`、`[es] Spanish`、`[fr] French`、`[nl] Dutch`。

![翻译](./images/transl11.png)

向上滚动并单击&#x200B;**保存**。

![翻译](./images/transl12.png)

您的&#x200B;**翻译提供商**&#x200B;现已准备就绪，可供使用。

![翻译](./images/transl13.png)

## 3.2.1.4配置翻译项目

转到[https://experience.adobe.com/](https://experience.adobe.com/)。 单击&#x200B;**Journey Optimizer**。

![翻译](./images/ajolp1.png)

在左侧菜单中，转到&#x200B;**翻译**，然后转到&#x200B;**区域设置词典**。 如果看到此消息，请单击&#x200B;**创建项目**。

![翻译](./images/ajoprovider1.png)

输入名称`--aepUserLdap-- - Translations`，将&#x200B;**Source区域设置**&#x200B;设置为`[en-US] English - United States`，并选中此复选框以启用&#x200B;**自动发布已批准的翻译**。 接下来，单击&#x200B;**+添加区域设置**。

![翻译](./images/ajoprovider1a.png)

搜索`fr`，启用`[fr] French`的复选框，然后启用&#x200B;**Microsoft Translator**&#x200B;的复选框。 单击&#x200B;**+添加区域设置**。

![翻译](./images/ajoprovider2.png)

搜索`es`，启用`[es] Spanish`的复选框，然后启用&#x200B;**Microsoft Translator**&#x200B;的复选框。 单击&#x200B;**+添加区域设置**。

![翻译](./images/ajoprovider3.png)

搜索`nl`，启用`[nl] Spanish`的复选框，然后启用&#x200B;**Microsoft Translator**&#x200B;的复选框。 单击&#x200B;**+添加区域设置**。

![翻译](./images/ajoprovider6.png)

单击&#x200B;**保存**。

![翻译](./images/ajoprovider8.png)

您的&#x200B;**翻译**&#x200B;项目现已准备就绪，可供使用。

![翻译](./images/ajoprovider9.png)

您已完成此练习。

## 后续步骤

转到[3.2.2创建您的营销活动](./ex2.md)

返回[模块3.2](./ajotranslationsvcs.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}