---
title: 将开发人员添加到基于Adobe Experience Platform的应用程序
description: 了解如何将开发人员添加到基于Adobe Experience Platform的应用程序并授予API凭据的权限
feature: Access Control
role: Admin, Developer
level: Beginner
jira: KT-14689
last-substantial-update: 2023-12-15T00:00:00Z
exl-id: 4bd28867-b664-4a45-8892-91af821cbbcc
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 添加开发人员并授予API凭据权限

了解如何将开发人员添加到基于Adobe Experience Platform的应用程序，如Real-Time Customer Data Platform和Journey Optimizer。 开发人员首先添加在Admin Console中。 在Developer Console中创建了Platform项目后，将在Platform或Journey Optimizer界面中为其API凭据分配权限。 有关详细信息，请访问[访问控制文档](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hans)。

>[!VIDEO](https://video.tv.adobe.com/v/3426407?learn=on&enablevpops)

>[!ADMIN]
>
>只有系统管理员可以添加开发人员并为API凭据分配权限。 产品管理员无法完成这些任务。

>[!TIP]
>
>我们建议您也将该开发人员作为&#x200B;**用户**&#x200B;添加到Admin Console中的`AEP-Default-All-Users`产品配置文件，然后将其添加到Platform界面中与API凭据相同的角色。 这允许他们在需要时使用界面。 有关详细信息，请参阅[添加用户](add-users.md)。
