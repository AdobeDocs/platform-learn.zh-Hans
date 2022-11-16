---
title: 快速入门 — 安装适用于Experience League文档的Chrome扩展
description: 快速入门 — 安装适用于Experience League文档的Chrome扩展
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6e0a88e7-65e3-4251-8ab1-e030a397a56b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# 0.1安装适用于Experience League文档的Chrome扩展

## 0.1.1为什么我们要创建Chrome扩展？

文档已变为通用文档，以便任何人都可以使用任何Adobe Experience Platform实例轻松重复使用。
通过使文档可重复使用， **环境变量** 文档中介绍了，这意味着您将在 **键** 中。 每个键都是特定环境的特定变量，Chrome扩展将为您更改该变量，这样您就可以轻松地从教程页面复制代码和文本，并将其粘贴到将作为教程一部分使用的各种用户界面中。

此类值的示例可在下面找到。 目前，这些值还无法使用，但是，当您安装并激活Chrome扩展后，您会看到这些变量变为“正常”文本，以便您复制和重复使用。

| 名称 | 键 |
|:-------------:| :---------------:|
| AEP IMS组织ID | `--aepImsOrgId--` |
| AEP租户ID | `--aepTenantId--` |
| DCS入口ID | `--dcsInletId--` |
| 演示配置文件LDAP | `--demoProfileLdap--` |

例如，在以下屏幕截图中，您可以看到对 `--aepTenantId--`.

![DSN](./images/mod7before.png)

安装扩展后，将自动更改该相同的文本以反映特定于实例的值。

![DSN](./images/mod7.png)

该扩展还允许您：

- 注册参加教程
- 通过提交每个模块的完成情况来跟踪您的进度，如 [如何测量完成？](../../completion.md)

## 0.1.2安装Chrome扩展

要安装该Chrome扩展，请打开您的Chrome浏览器，然后转到： [https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0](https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0). 然后你会看到这个。

单击 **添加到Chrome**.

![DSN](./images/c2.png)

然后你会看到这个。 单击 **添加扩展**.

![DSN](./images/c3.png)

随后将安装该扩展，您将看到类似的通知。

![DSN](./images/c4.png)

在 **扩展** 菜单，单击 **拼图** 图标并固定 **平台学习 — 配置** 扩展。

![DSN](./images/c6.png)

## 0.1.2配置Chrome扩展

转到 [https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en) ，然后单击扩展图标以将其打开。

![DSN](./images/tuthome.png)

然后，您将看到此弹出窗口。 单击 **+** 图标。

![DSN](./images/c7.png)

输入您的名称和为Adobe Experience Platform环境创建的配置ID。 单击&#x200B;**新建**。

>[!IMPORTANT]
>
>如果您是Adobe员工：您可以在内部Github存储库(https://git.corp.adobe.com/vangeluw/platformenablement)中找到要使用的配置ID。
>
>如果您是Adobe解决方案合作伙伴，请联系您的解决方案合作伙伴联系人或发送电子邮件 **spphelp@adobe.com**.

![DSN](./images/c8.png)

在扩展的左侧菜单中，您现在将看到一个带有您姓名首字母的图标。 单击它。 然后，您将看到 **环境变量** 和您的特定Adobe Experience Platform实例值。 单击 **激活配置**.

![DSN](./images/c9.png)

激活配置后，您会在首字母旁边看到一个绿色圆点。 这表示您的配置ID现在处于活动状态。 此外，您还将看到许多其他菜单选项。

![DSN](./images/c10.png)

您现在有2个选项：

- 如果您是已启用且已设置的现有用户，请转到 **0.1.3现有用户 — 登录**
- 如果您是首次启动本教程的全新用户，请转到 **0.1.4注册** 跳过 **0.1.3现有用户 — 登录**

## 0.1.3现有用户 — 登录

>[!IMPORTANT]
>
>练习 **0.1.3现有用户 — 登录** 仅当您是之前已注册参加本教程的现有用户时，才会正常工作。

如果您是首次设置此Chrome扩展的现有用户，请单击左侧菜单中的紫色图标。 然后你会看到这个。

![DSN](./images/chromeret1.png)

根据需要填写值。

>[!IMPORTANT]
>
>的 **LDAP** 是最重要的字段：您应使用首次注册本教程时所用的相同LDAP。 这将确保成功加载进度。 如果不确定ldap是什么，请查看您的电子邮件地址。 在您的电子邮件地址中，使用@-symbol之前的文本作为LDAP。 如果您的电子邮件地址为 **vangeluw@adobe.com**，则在此处输入的LDAP应为 **万热卢**)。

![DSN](./images/chromeret2.png)

单击&#x200B;**确定**。

![DSN](./images/chromeret3.png)

30秒1分钟后，您的屏幕将发生更改，并且您将被还原为 **主页**，您将在此处看到以下内容：

![DSN](./images/chromeret4.png)

您的Chrome扩展现已配置完成，您现在可以验证一切是否正常。

## 0.1.4新用户 — 注册

>[!IMPORTANT]
>
>练习 **0.1.4新用户 — 注册** 适用于首次启动本教程的新用户。

如果您是首次注册本教程的新用户，请单击菜单中的黄色图标。 然后你会看到这个。

![DSN](./images/c11.png)

根据需要填写字段。 单击&#x200B;**保存**。

>[!IMPORTANT]
>
>的 **LDAP** 是最重要的领域。 如果不确定ldap是什么，请查看您的电子邮件地址。 在您的电子邮件地址中，使用@-symbol之前的文本作为LDAP。 如果您的电子邮件地址为 **vangeluw@adobe.com**，则在此处输入的LDAP应为 **万热卢**)。

![DSN](./images/chrome1.png)

30秒1分钟后，您的屏幕将发生更改，并且您将被还原为 **主页**，您将在此处看到以下内容：

![DSN](./images/chrome2.png)

您的Chrome扩展现已配置完成，您现在可以验证一切是否正常。

## 0.1.5验证教程内容

对于测试，请转到 [本页](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/module4/ex3.html?lang=zh-Hans).

你现在应该看到 **环境变量** 已根据chrome扩展中的配置ID被替换为其真实值。

现在，您应该具有与下面类似的视图，其中的环境变量 `--aepTenantId--` 已被您的实际租户ID替换，在本例中为 **_experienceplatform**.

![DSN](./images/c12.png)

下一步： [0.2使用“演示系统”旁边的“设置Adobe Experience Platform数据收集客户端属性”](./ex2.md)

[返回模块0](./getting-started.md)

[返回到所有模块](./../../overview.md)
