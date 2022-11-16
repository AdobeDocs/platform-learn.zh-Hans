---
title: 区段激活到Microsoft Azure事件中心 — 创建流区段
description: 区段激活到Microsoft Azure事件中心 — 创建流区段
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: de3824bd-553c-4281-8edf-29abcc28a8e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 13.3创建区段

## 13.3.1导言

您将创建一个简单的区段：

- **设备权益** 客户用户档案在访问时将符合其条件 **设备** Luma演示网站的页面。

### 很高兴知道

当您符合某个区段的资格条件（该区段是该目标激活列表的一部分）时，Real-time CDP将触发对该目标的激活。 在这种情况下，将发送到该目标的区段鉴别有效负载将包含 **您的用户档案符合其条件的所有区段**.

本模块的目标是显示客户用户档案的区段资格已发送至 **您的** 实时事件中心目标。

### 区段状态

在Adobe Experience Platform中，区段资格始终具有 **状态**-property ，可以是以下任一类型：

- **实现**:这表示新的区段资格
- **现有**:这表示现有区段资格
- **退出**:这表示用户档案不再符合区段资格

## 13.3.2构建区段

构建区段在 [模块6](../module6/real-time-cdp-build-a-segment-take-action.md).

### 创建区段

通过转到以下URL登录Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登录后，您将登陆Adobe Experience Platform的主页。

![数据获取](../module2/images/home.png)

在继续之前，您需要选择 **沙盒**. 要选择的沙盒已命名 ``--aepSandboxId--``. 您可以通过单击 **[!UICONTROL 生产产品]** 的蓝线。 选择相应的沙盒后，您将看到屏幕发生更改，现在您就位于专用沙盒中。

![数据获取](../module2/images/sb1.png)

转到 **区段**. 单击 **+创建区段** 按钮。

![数据获取](./images/seg.png)

命名区段 `--demoProfileLdap-- - Interest in Equipment` 和添加页面名称体验事件：

单击 **事件**，拖放 **XDM ExperienceEvent > Web >网页详细信息>名称**. 输入 **设备** 作为值：

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

拖放 **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. 输入 `--demoProfileLdap--` 作为值，将comparison参数设置为 **包含** 单击 **保存**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL定义

区段的PQL如下所示：

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

下一步： [13.4激活区段](./ex4.md)

[返回到模块13](./segment-activation-microsoft-azure-eventhub.md)

[返回到所有模块](./../../overview.md)
