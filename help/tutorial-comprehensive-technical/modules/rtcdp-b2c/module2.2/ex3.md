---
title: 客户人工智能 — 评分仪表板和分段（预测并采取行动）
description: 客户人工智能 — 评分仪表板和分段（预测并采取行动）
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 2.2.3客户人工智能 — 评分仪表板和分段（预测并采取行动）

一旦您的客户人工智能实例完成模型运行，您将能够可视化经过评估的倾向分数，以预测客户在未来30天内执行购买。

![AI](./images/caimodels.png)

>[!NOTE]
>
>只有状态为&#x200B;**成功**&#x200B;的客户人工智能实例才允许您预览服务的见解。

## 2.2.3.1倾向预测

现在，我们来回顾一下客户人工智能实例模型生成的预测倾向。 单击实例名称可查看仪表板。

![AI](./images/caimodels1.png)

客户人工智能仪表板显示有关得分、人口分布和模型要评估的影响因素的摘要。

![AI描述](./images/caidescription.png)

![仪表板摘要](./images/caidashboard.png)

将鼠标悬停在影响因素上，以查看数据分布的进一步细分。

![影响因素](./images/caiinfluencefactors.png)

## 2.2.3.2业务操作

### 2.2.3.2.1对客户进行分段

Customer AI仪表板允许通过单击定义区段。 单击倾向卡上的&#x200B;**创建区段**&#x200B;按钮。

![创建区段](./images/caiinfluencefactors1.png)

您将看到区段定义是自动创建的。

![区段规则](./images/caicreatesegment.png)

按照以下命名约定为您的区段提供一个名称： `--aepUserLdap-- - Customer AI High Propensity`。 单击&#x200B;**保存**。

![区段规则](./images/caicreatesegment1.png)

您现在可以使用此区段通过如Real-time CDP、Journey Orchestration和Adobe Target进行定位。

### 2.2.3.2.2配置文件概述

由于客户人工智能倾向得分将成为实时客户档案的一部分，因此您可以查看单个客户的分数。

在Adobe Experience Platform中，转到左侧菜单中的&#x200B;**配置文件**，然后选择&#x200B;**浏览**。

使用您摄取的JSON文件中提供的任何标识符搜索配置文件，例如实例&#x200B;**EMAIL hbirkenshawa@businessweek.com**。 单击&#x200B;**配置文件ID**&#x200B;以打开配置文件。

![用户档案](./images/profile1.png)

您随后将看到以下内容：

![用户档案](./images/profile2.png)

转到&#x200B;**Attributes**，其中包含来自您的客户人工智能模型的输出。

![用户档案](./images/profile3.png)

向下滚动以查看由您的客户人工智能模型计算的倾向分数。

![用户档案](./images/profile4.png)

下一步：[摘要和优点](./summary.md)

[返回模块2.2](./intelligent-services.md)

[返回所有模块](./../../../overview.md)
