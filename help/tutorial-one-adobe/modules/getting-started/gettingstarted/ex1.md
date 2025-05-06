---
title: 快速入门 — 为Experience League文档安装Chrome扩展
description: 快速入门 — 为Experience League文档安装Chrome扩展
kt: 5342
doc-type: tutorial
exl-id: 3618dacb-2203-4d19-ae51-f78415a693fd
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# 安装适用于Experience League文档的Chrome扩展

## 关于Chrome扩展

本教程已变得通用，任何人都可以使用任何Adobe Experience Cloud实例轻松重复使用。

为了使文档可重用，在教程中引入了&#x200B;**环境变量**，这意味着您将在文档中找到以下&#x200B;**占位符**。 每个占位符都是适用于特定环境的特定变量，Chrome扩展会更改该变量，以便您轻松地从教程页面复制代码和文本，并将其粘贴到教程中使用的各种用户界面中。

此类值的示例如下所示。 目前，这些值尚无法使用，但一旦您安装和激活Chrome扩展，就会看到这些变量变为可供复制和重用的普通文本。

| 名称 | 键 | 示例 |
|:-------------:| :---------------:| :---------------:|
| IMS 组织 ID | `--aepImsOrgId--` | `907075E95BF479EC0A495C73@AdobeOrg` |
| IMS组织名称 | `--aepImsOrgName--` | `Experience Platform International` |
| AEP租户ID | `--aepTenantId--` | `_experienceplatform` |
| AEP沙盒名称 | `--aepSandboxName--` | `one-adobe` |
| 学习者配置文件LDAP | `--aepUserLdap--` | `vangeluw` |

例如，在以下屏幕截图中，您可以看到对`aepSandboxName`的引用。

![DSN](./images/mod7before.png)

安装扩展后，该文本将自动更改以反映实例特定的值。

![DSN](./images/mod7.png)

## 安装Chrome扩展

要安装该Chrome扩展，请打开Chrome浏览器，然后转到： [https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi](https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi){target="_blank"}。 你会看到这个。

单击&#x200B;**添加到Chrome**。

![DSN](./images/c2.png)

你会看到这个。 单击&#x200B;**添加扩展**。

![DSN](./images/c3.png)

随后将安装扩展，您会看到一条类似通知。

![DSN](./images/c4.png)

在&#x200B;**扩展**&#x200B;菜单中，单击&#x200B;**拼图块**&#x200B;图标，并将&#x200B;**Platform Learn - Configuration**&#x200B;扩展固定到扩展菜单。

![DSN](./images/c6.png)

## 配置Chrome扩展

转到[https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview){target="_blank"}，然后单击扩展图标以将其打开。

![DSN](./images/tuthome.png)

然后您会看到此弹出窗口。 单击&#x200B;**+**&#x200B;图标。

![DSN](./images/c7.png)

输入如下所示的值，这些值都与您的Adobe Experience Platform实例相关。

![DSN](./images/c8.png)

如果您不确定要为这些字段输入什么值，请遵循以下指南。

**AEP IMS组织名称**

当您在[https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"}上登录到Adobe Experience Platform实例时，您将在屏幕的右上角找到实例的名称。

![DSN](./images/aepname.png)

**AEP IMS组织ID**

IMS组织ID是Adobe Experience Cloud实例的唯一标识符，在本教程中的多个位置引用了该标识符。

可以通过多种方式查找IMS组织ID。 如果您不确定，请咨询您实例的其中一位系统管理员来查找该ID。

您可以通过转到[Admin Console](https://adminconsole.adobe.com/){target="_blank"}找到它，您可以在其中将它作为URL的一部分找到。

![DSN](./images/aepid1.png)

您还可以通过转到AEP菜单中的&#x200B;**数据管理>查询**&#x200B;找到它，您可以在&#x200B;**用户名**&#x200B;下找到它。

![DSN](./images/aepid2.png)

请确保复制并粘贴&#x200B;**@AdobeOrg**&#x200B;部分以及ID。

**AEP租户ID**

您的租户ID是组织AEP实例的唯一标识符。 当您在[https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"}上登录到Adobe Experience Platform实例时，您将在URL中找到租户ID。

![DSN](./images/aeptenantid.png)

当您在Chrome扩展中输入它时，应确保添加下划线作为前缀，因此在此示例中&#x200B;**experienceplatform**&#x200B;变为&#x200B;**_experienceplatform**。

**AEP沙盒名称**

您的沙盒名称是您将在AEP实例中使用的环境的名称。 当您在[https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"}上登录到Adobe Experience Platform实例时，您将在URL中找到租户ID。

在从URL获取沙盒名称之前，您应确保位于应用于本教程的沙盒中。 您可以通过单击屏幕右上角的沙盒切换器菜单切换到右沙盒。

![DSN](./images/aepsandboxsw.png)

在此示例中，AEP沙盒名称为&#x200B;**one-adobe**。

![DSN](./images/aepsname.png)

**您的LDAP**

该用户名将在本教程中使用。 在此示例中，LDAP基于此用户的电子邮件地址。 电子邮件地址为&#x200B;**vangeluw@adobe.com**，因此LDAP将变为&#x200B;**vangeluw**。

LDAP用于确保您即将执行的配置将链接到您，并且不会与您正在使用的同一实例和沙盒的其他用户发生冲突。

您的值应当类似于以下内容。
最后，单击&#x200B;**新建**。

![DSN](./images/c8a.png)

在扩展的左侧菜单中，您现在将看到一个包含环境缩写的新图标。 单击它。 然后，您将看到&#x200B;**环境变量**&#x200B;与您的特定Adobe Experience Platform实例值之间的映射。 单击&#x200B;**激活配置**。

![DSN](./images/c9.png)

激活配置后，您将在环境的首字母缩写旁看到一个绿色圆点。 这意味着您的环境现在处于活动状态。

![DSN](./images/c10.png)

## 验证教程内容

作为测试，请转到[此页面](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-one-adobe/activation/dc/dc13/ex2){target="_blank"}。

您现在应该会看到，根据Chrome扩展中激活的环境，此页面上的所有&#x200B;**环境变量**&#x200B;都已替换为其真值。

您现在应具有类似于下面的视图，其中环境变量`aepSandboxName`已被您的实际AEP沙盒名称（在本例中为&#x200B;**one-adobe**）替换。

![DSN](./images/mod7.png)

## 后续步骤

转到[使用演示系统下一步以设置您的Adobe Experience Platform数据收集客户端属性](./ex2.md){target="_blank"}

返回[开始使用](./getting-started.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
