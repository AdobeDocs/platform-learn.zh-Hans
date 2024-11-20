---
title: 区段激活到Microsoft Azure事件中心 — 创建流区段
description: 区段激活到Microsoft Azure事件中心 — 创建流区段
kt: 5342
doc-type: tutorial
exl-id: 86bc3afa-16a9-4834-9119-ce02445cd524
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 1%

---

# 2.4.3创建区段

## 2.4.3.1导言

您将创建一个简单的区段：

- **客户在访问Luma演示网站的**&#x200B;设备&#x200B;**页面时，对客户配置文件将符合条件的设备**&#x200B;感兴趣。

### 很高兴知道

当您符合某个区段的条件（该区段属于某个目标的激活列表）时，Real-time CDP将触发对该目标的激活。 在这种情况下，将发送到该目标的区段资格有效负载将包含&#x200B;**您的配置文件符合条件的所有区段**。

此模块的目标是显示客户个人资料的区段资格已实时发送到&#x200B;**您的**&#x200B;事件中心目标。

### 区段状态

Adobe Experience Platform中的区段资格始终具有&#x200B;**状态** — 属性，可以是以下任一属性：

- **已实现**：这表示有新的区段鉴别
- **existing**：这表示存在区段资格
- **已退出**：这表示配置文件不再符合该区段的条件

## 2.4.3.2构建区段

在[模块2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)中详细说明了如何构建区段。

### 创建区段

通过转到以下URL登录Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登录后，您将登录到Adobe Experience Platform的主页。

![数据获取](./../../../modules/datacollection/module1.2/images/home.png)

在继续之前，您需要选择一个&#x200B;**沙盒**。 要选择的沙盒名为``--aepSandboxName--``。 选择相应的沙盒后，您将看到屏幕变化，现在您位于专用沙盒中。

![数据获取](./../../../modules/datacollection/module1.2/images/sb1.png)

转到&#x200B;**区段**。 单击&#x200B;**+创建区段**&#x200B;按钮。

![数据获取](./images/seg.png)

命名您的区段`--aepUserLdap-- - Interest in Equipment`并添加页面名称体验事件：

单击&#x200B;**事件**，然后拖放&#x200B;**XDM ExperienceEvent > Web >网页详细信息>名称**。 输入&#x200B;**设备**&#x200B;作为值：

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

拖放&#x200B;**XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**。 输入`--aepUserLdap--`作为值，将比较参数设置为&#x200B;**包含**，然后单击&#x200B;**保存**：

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL定义

区段的PQL如下所示：

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--aepUserLdap--", false))])
```

下一步： [2.4.4激活区段](./ex4.md)

[返回模块2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模块](./../../../overview.md)
