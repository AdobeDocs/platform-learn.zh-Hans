---
title: Offer Decisioning — 配置优惠和决策ID
description: Offer Decisioning — 配置优惠和决策ID
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 12%

---

# 3.7.2配置优惠和决策

## 3.7.2.1创建您的个性化优惠

在本练习中，您将创建四个&#x200B;**个性化优惠**。 以下是创建这些优惠时要考虑的详细信息：

| 名称 | Date Range | 电子邮件的图像链接 | Web的图像链接 | 文本 | 优先级 | 资格 | 语言 | 上限频率 | 图像名称 |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | 今天 — 1个月后 | https://bit.ly/4a9RJ5d | 从Assets Library中选择 | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | 全部 — 女性客户 | 英语（美国） | 3 | Apple AirPods Max- Female.jpg |
| `--aepUserLdap-- - Galaxy S24` | 今天 — 1个月后 | https://bit.ly/3W8yuDv | 从Assets Library中选择 | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | 全部 — 女性客户 | 英语（美国） | 3 | Galaxy S24 - Female.jpg |
| `--aepUserLdap-- - Apple Watch` | 今天 — 1个月后 | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | 全部 — 男性客户 | 英语（美国） | 3 | Apple Watch - Male.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | 今天 — 1个月后 | https://bit.ly/4gTrkeo | 从Assets Library中选择 | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | 全部 — 男性客户 | 英语（美国） | 3 | Galaxy Watch7 - Male.jpg |

{style="table-layout:auto"}

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 然后，您将进入沙盒&#x200B;**的**&#x200B;主页`--aepSandboxName--`视图。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 后续步骤

转到[3.7.3适用于Experience Decisioning的Web SDK设置](./ex3.md){target="_blank"}

返回至[Experience Decisioning](ajo-decisioning.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
