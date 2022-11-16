---
title: Real-time CDP — 构建区段并采取操作 — 配置广告目标，如Google DV360
description: Real-time CDP — 构建区段并采取操作 — 配置广告目标，如Google DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 6.2配置广告目标，如Google DV360

>[!IMPORTANT]
>
>以下内容旨在作为FYI — 您可以 **NOT** 必须为DV360配置新目标。 目标已创建，您可以在下一个练习中使用它。

转到 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的 [!UICONTROL 沙盒]，您将看到屏幕更改，现在，您已加入您的专述 [!UICONTROL 沙盒].

![数据获取](../module2/images/sb1.png)

在左侧菜单中，转到 **目标**，然后转到 **目录**. 然后您将看到 **目标目录**.

![RTCDP](./images/rtcdp.png)

在 **目标**，单击 **Google显示与视频360** 然后单击 **+设置**.

![RTCDP](./images/rtcdpgoogle.png)

然后你会看到这个。 单击 **连接到目标**.

![RTCDP](./images/rtcdpgooglecreate1.png)

在下一个屏幕中，您可以配置到Google DV360的目标。

![RTCDP](./images/rtcdpgooglecreatedest.png)

在字段中输入一个值 **名称** 和 **描述**.

字段 **帐户ID** 是 **广告商ID** DV360帐户的ID。 您可以在此处找到：

![RTCDP](./images/rtcdpgoogledv360advid.png)

的 **帐户类型** 应设置为 **邀请广告商**.

现在你有了这个。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google需要允许列表Adobe，以便Adobe Experience Platform将数据发送到Google DV360。 请联系您的Google客户经理以启用此数据流。

创建目标后，您将看到此内容。 您可以选择数据管理策略。 接下来，单击 **保存并退出**.

![RTCDP](./images/rtcdpcreatedest1.png)

然后，您将看到可用目标的列表。
在下一个练习中，您将将您在上一个练习中构建的区段连接到Google DV360目标。

下一步： [6.3采取行动：将区段发送到DV360](./ex3.md)

[返回到模块6](./real-time-cdp-build-a-segment-take-action.md)

[返回到所有模块](../../overview.md)
