---
title: 快速入门 — 为Experience League文档安装Chrome扩展
description: 快速入门 — 为Experience League文档安装Chrome扩展
kt: 5342
doc-type: tutorial
source-git-commit: bdade61b2f64a5138807a47f73d8006ce9c564fc
workflow-type: tm+mt
source-wordcount: '624'
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

例如，在以下屏幕截图中，您可以看到对`aepImsOrgName`的引用。

![DSN](./images/mod7before.png)

安装扩展后，该文本将自动更改以反映实例特定的值。

![DSN](./images/mod7.png)

## 安装Chrome扩展

要安装该Chrome扩展，请打开Chrome浏览器，然后转到： [https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi](https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi){target="_blank"}。 你会看到这个。

单击&#x200B;**添加到Chrome**。

![DSN](./images/c2.png)

你会看到这个。 Click **Add extension**.

![DSN](./images/c3.png)

The extension will then be installed, and you&#39;ll see a similar notification.

![DSN](./images/c4.png)

In the **extensions** menu, click the **puzzle piece** icon and pin the **Platform Learn - Configuration** extension to the extension menu.

![DSN](./images/c6.png)

## Configure the Chrome extension

Go to [https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview){target="_blank"} and then click the extension icon to open it.

![DSN](./images/tuthome.png)

You&#39;ll then see this popup. Click the **+** icon.

![DSN](./images/c7.png)

Enter the values as indicated below, which are all related to your Adobe Experience Platform instance.

![DSN](./images/c8.png)

**Your LDAP**

This is the username that will be used as part of the tutorial. In this example, the LDAP is based off of the email address of this user. The email address is **vangeluw@adobe.com** so the LDAP becomes **vangeluw**.

The LDAP is used to ensure that the configuration you&#39;ll be doing will be linked to you, and won&#39;t conflict with other users that may be using the same instance and sandbox that you&#39;re using.

Your values should look similar to these.
Finally, click **Create New**.

![DSN](./images/c8a.png)

In the left menu of the extension, you&#39;ll now see a new icon with the initials of your environment. Click it. 然后，您将看到&#x200B;**环境变量**&#x200B;与您的特定Adobe Experience Platform实例值之间的映射。 单击&#x200B;**激活配置**。

![DSN](./images/c9.png)

激活配置后，您将在环境的首字母缩写旁看到一个绿色圆点。 这意味着您的环境现在处于活动状态。

![DSN](./images/c10.png)

## 验证教程内容

作为测试，请转到[此页面](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-one-adobe/agents/agents1/ex1){target="_blank"}。

您现在应该会看到，根据Chrome扩展中激活的环境，此页面上的所有&#x200B;**环境变量**&#x200B;都已替换为其真值。

您现在应具有类似于下面的视图，其中环境变量`aepSandboxName`已被您的实际AEP沙盒名称（在本例中为&#x200B;**one-adobe**）替换。

![DSN](./images/mod7.png)

## 后续步骤

转到[要安装的应用程序](./ex2.md){target="_blank"}

返回[快速入门 — 代理AI](./getting-started-agentic-ai.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
