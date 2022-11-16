---
title: 智能服务 — Customer AI创建新实例（配置）
description: Customer AI — 创建新实例（配置）
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: d9377c97-efed-427a-a063-aa9c6bd1a78a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 3%

---

# 5.2 Customer AI — 创建新实例（配置）

Customer AI通过分析现有的消费者体验事件数据来预测客户流失率或转化倾向得分。 创建新的Customer AI实例可让营销人员定义目标和衡量标准。

## 5.2.1设置新的Customer AI实例

在Adobe Experience Platform中，单击 **服务** 中。 的 **服务** 浏览器会显示并显示您可使用的所有可用服务。 在Customer AI的卡片中，单击 **打开**.

![服务导航](./images/navigatetoservice.png)

单击 **创建实例**.

![创建新实例](./images/createnewinstance.png)

然后你会看到这个。

![创建新实例](./images/custai1.png)

输入Customer AI实例的必需详细信息：

- 名称：use `--demoProfileLdap-- Product Purchase Propensity`
- 描述：使用： **预测客户购买产品的可能性**
- 倾向类型：选择 **转化**

![设置第1页](./images/setuppage1.png)

单击&#x200B;**下一步**。

![设置第1页](./images/next.png)

然后你会看到这个。 选择您在上一个练习中创建的数据集(名为 `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. 单击&#x200B;**下一步**。

![设置第1页](./images/custai2.png)

选择 **将发生** 并定义字段 **commerce.purchases.value** 作为目标变量。

![定义CAI目标](./images/caidefinegoal.png)

单击&#x200B;**下一步**。

![设置第1页](./images/next.png)

接下来，将计划设置为运行 **每周** 并将时间设置为尽可能接近您当前的时间。 确保切换 **为用户档案启用分数** 启用。

![定义CAI高级](./images/caiadvancepage.png)

单击&#x200B;**完成**。

![设置第1页](./images/finish.png)

然后，您将看到此弹出窗口。 单击&#x200B;**确定**。

![设置第1页](./images/finish1.png)

配置实例后，您可以在Customer AI实例列表中看到该实例，并通过单击Customer AI实例行预览设置和执行详细信息的摘要。 在发现错误的情况下，摘要面板还将显示错误详细信息。

![实例设置摘要](./images/caiinstancesummary.png)

>[!NOTE]
>
>只要Customer AI实例的状态为 **等待培训** 或 **错误**

下一步： [5.3客户AI — 评分仪表板和分段（预测并采取行动）](./ex3.md)

[返回到模块5](./intelligent-services.md)

[返回到所有模块](./../../overview.md)
