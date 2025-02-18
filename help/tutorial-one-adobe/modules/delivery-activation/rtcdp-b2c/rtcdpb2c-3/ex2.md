---
title: Real-time CDP — 构建受众并采取行动 — 配置Advertising目标，如Google DV360
description: Real-time CDP — 构建受众并采取行动 — 配置Advertising目标，如Google DV360
kt: 5342
doc-type: tutorial
exl-id: 2498c80f-8ba8-4563-ac37-52f461f706f4
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 2.3.2配置Advertising目标，如Google DV360

>[!IMPORTANT]
>
>以下内容仅供参考 — 如果您的实例中已存在此类目标，则&#x200B;**不**&#x200B;必须配置DV360的新目标。 在该情况下已创建目标，您可以在下一个练习中使用它。

转到[Adobe Experience Platform](https://experience.adobe.com/platform)。 登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择适当的[!UICONTROL 沙盒]后，您将看到屏幕更改，现在您已经进入专用的[!UICONTROL 沙盒]。

![数据获取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

在左侧菜单中，转到&#x200B;**目标**，然后转到&#x200B;**目录**。 您随后将看到&#x200B;**目标目录**。

![RTCDP](./images/rtcdp.png)

在&#x200B;**目标**&#x200B;中，单击&#x200B;**Google显示和视频360**，然后单击&#x200B;**+设置**。

![RTCDP](./images/rtcdpgoogle.png)

你会看到这个。 单击&#x200B;**连接到目标**。

![RTCDP](./images/rtcdpgooglecreate1.png)

在下一个屏幕中，您可以配置目标到Google DV360。

![RTCDP](./images/rtcdpgooglecreatedest.png)

在&#x200B;**Name**&#x200B;和&#x200B;**Description**&#x200B;字段中输入值。

字段&#x200B;**帐户ID**&#x200B;是DV360帐户的&#x200B;**广告商ID**。 您可以在此处找到该内容：

![RTCDP](./images/rtcdpgoogledv360advid.png)

**帐户类型**&#x200B;应设置为&#x200B;**邀请广告商**。

现在你有了这个。 单击&#x200B;**下一步**。

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google需要将Adobe列入允许列表，以便Adobe Experience Platform将数据发送到Google DV360。 请联系您的Google客户经理以启用此数据流。

创建目标后，您将看到此内容。 您可以选择数据治理策略。 接下来，单击&#x200B;**保存并退出**。

![RTCDP](./images/rtcdpcreatedest1.png)

然后，您将看到可用目标的列表。
在下一个练习中，您会将在上一个练习中构建的受众连接到Google DV360目标。

## 后续步骤

转到[2.3.3执行操作：将您的受众发送到DV360](./ex3.md){target="_blank"}

返回[Real-time CDP — 构建受众并执行操作](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
