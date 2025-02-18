---
title: 客户人工智能 — 评分仪表板和分段（预测并采取行动）
description: 客户人工智能 — 评分仪表板和分段（预测并采取行动）
kt: 5342
doc-type: tutorial
exl-id: a6df3ff1-f907-4185-8189-f0b39c67c943
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 2.2.3客户人工智能 — 评分仪表板和分段（预测并采取行动）

一旦您的客户人工智能实例完成模型运行，您将能够可视化经过评估的倾向分数，以预测客户在未来30天内执行购买。

![AI](./images/caiinstancesummary1.png)

>[!NOTE]
>
>只有状态为&#x200B;**成功**&#x200B;的客户人工智能实例才允许您预览服务的见解。

## 倾向预测

现在，我们来回顾一下客户人工智能实例模型生成的预测倾向。 单击实例名称可查看仪表板。

![AI](./images/caimodels1.png)

客户人工智能仪表板显示有关得分、人口分布和模型要评估的影响因素的摘要。

![AI描述](./images/caidescription.png)

将鼠标悬停在影响因素上，以查看数据分布的进一步细分。

![影响因素](./images/caiinfluencefactors.png)

## 业务操作

### 划分客户

Customer AI仪表板允许通过单击定义区段。 单击倾向卡上的&#x200B;**创建区段**&#x200B;按钮。

![创建区段](./images/caiinfluencefactors1.png)

您将看到区段定义是自动创建的。

![区段规则](./images/caicreatesegment.png)

按照以下命名约定为您的区段提供一个名称： `--aepUserLdap-- - Customer AI High Propensity`。 单击&#x200B;**发布**。

![区段规则](./images/caicreatesegment1.png)

您现在可以使用此区段通过如Real-time CDP、Journey Optimizer和Adobe Target进行定位。

## 清除

为了确保您的环境中不会保留不需要的演示数据，请确保在成功完成此练习后删除数据集`--aepUserLdap-- - Demo System - Customer Experience Event Dataset`。 如果不删除演示数据，则会对AEP实例造成成本影响。

![轮廓](./images/cleanup.png)

## 后续步骤

转到[摘要和优点](./summary.md){target="_blank"}

返回[智能服务](./intelligent-services.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
