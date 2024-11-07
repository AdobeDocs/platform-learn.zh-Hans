---
title: offer decisioning — 配置优惠和决策ID
description: offer decisioning — 配置优惠和决策ID
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 2%

---

# 3.3.2配置优惠和决策

## 3.3.2.1创建个性化优惠

在本练习中，您将创建四个&#x200B;**个性化优惠**。 以下是创建这些优惠时要考虑的详细信息：

| 名称 | Date Range | 电子邮件的图像链接 | Web的图像链接 | 文本 | 优先级 | 资格 | 语言 |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|
| `--aepUserLdap-- - Nadia Elements Shell` | 今天 — 1个月后 | https://bit.ly/3nPiwdZ | https://bit.ly/2INwXjt | `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell` | 25 | 全部 — 女性客户 | 英语（美国） |
| `--aepUserLdap-- - Radiant Tee` | 今天 — 1个月后 | https://bit.ly/2HfA17v | https://bit.ly/3pEIdzn | `{{ profile.person.name.firstName }}, 5% discount on Radiant Tee` | 15 | 全部 — 女性客户 | 英语（美国） |
| `--aepUserLdap-- - Zeppelin Yoga Pant` | 今天 — 1个月后 | https://bit.ly/2IOaItW | https://bit.ly/2INZHZd | `{{ profile.person.name.firstName }}, 10% discount on Zeppelin Yoga Pant` | 25 | 全部 — 男性客户 | 英语（美国） |
| `--aepUserLdap-- - Proteus Fitness Jackshirt` | 今天 — 1个月后 | https://bit.ly/330a43n | https://bit.ly/36USaQW | `{{ profile.person.name.firstName }}, 5% discount on Proteus Fitness Jackshirt` | 15 | 全部 — 男性客户 | 英语（美国） |

{style="table-layout:auto"}

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 若要从一个沙盒更改到另一个沙盒，请单击&#x200B;**PRODUCTION Prod (VA7)**，然后从列表中选择该沙盒。 在此示例中，沙盒名为&#x200B;**AEP Enablement FY22**。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

在左侧菜单中，单击&#x200B;**选件**，然后转到&#x200B;**选件**。 单击&#x200B;**+创建选件**。

![决策规则](./images/offers1.png)

然后您会看到此弹出窗口。 选择&#x200B;**个性化优惠**，然后单击&#x200B;**下一步**。

![决策规则](./images/offers2.png)

您现在位于&#x200B;**详细信息**&#x200B;视图中。

![决策规则](./images/offers3.png)

在这种情况下，您需要配置选件`--aepUserLdap-- - Nadia Elements Shell`。 使用上表中的信息填写字段。 在此示例中，个性化优惠的名称为&#x200B;**vangeluw - Nadia Elements Shell**。 此外，将&#x200B;**开始日期和时间**&#x200B;设置为昨天，并将&#x200B;**结束日期和时间**&#x200B;设置为从现在起一个月后的某个日期。

完成后，您应该拥有此项。 单击&#x200B;**下一步**。

![决策规则](./images/offers4.png)

您现在需要创建&#x200B;**呈现**。 表示是&#x200B;**版面**&#x200B;和实际资源的组合。

对于&#x200B;**呈现1**，请选择：

- 渠道：Web
- 版面：Web — 图像
- 内容： URL
- 公共位置：从上表中列&#x200B;**Web**&#x200B;的图像链接复制URL

![决策规则](./images/addcontent1.png)

或者，您也可以为内容选择&#x200B;**资源库**，然后单击&#x200B;**浏览**。

![决策规则](./images/addcontent2.png)

随后您将看到Assets库的弹出窗口，转到文件夹&#x200B;**enablement-assets**&#x200B;并选择图像文件&#x200B;**nadia-web.png**。 然后，单击&#x200B;**选择**。

![决策规则](./images/addcontent3.png)

您随后将看到以下内容：

![决策规则](./images/addcontentrep20.png)

单击&#x200B;**+添加呈现**。

![决策规则](./images/addrep.png)

对于&#x200B;**呈现2**，请选择：

- 渠道：电子邮件
- 版面：电子邮件 — 图像
- 内容： URL
- 公共位置：复制上表中电子邮件&#x200B;**的列**&#x200B;图像链接中的URL

![决策规则](./images/addcontentrep21.png)

或者，您也可以为内容选择&#x200B;**资源库**，然后单击&#x200B;**浏览**。

![决策规则](./images/addcontent2b.png)

随后您将看到Assets库的弹出窗口，转到文件夹&#x200B;**enablement-assets**&#x200B;并选择图像文件&#x200B;**nadia-email.png**。 然后，单击&#x200B;**选择**。

![决策规则](./images/addcontent3b.png)

您随后将看到以下内容：

![决策规则](./images/addcontentrep20b.png)

接下来，单击&#x200B;**+添加呈现**。

![决策规则](./images/addrep.png)

对于&#x200B;**呈现3**，请选择：

- 渠道：非数字
- 版面：非数字 — 文本

接下来，您需要添加内容。 在这种情况下，这意味着添加要用作行动号召的文本。

单击&#x200B;**添加内容**。

![决策规则](./images/addcontentrep31.png)

然后您会看到此弹出窗口。

![决策规则](./images/addcontent3text.png)

选择&#x200B;**自定义文本**&#x200B;并填写以下字段：

查看上表中的&#x200B;**文本**&#x200B;字段，并在此处输入该文本，在本例中为： `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell`。

您还会注意到您可以选择任何配置文件属性，并将其作为动态字段包含在选件文本中。 在本例中，字段`{{ profile.person.name.firstName }}`将确保接收此优惠的客户的名字将包含在优惠文本中。

你会看到这个。 单击&#x200B;**保存**。

![决策规则](./images/addcontentrep3text.png)

您现在拥有了此功能。 单击&#x200B;**下一步**。

![决策规则](./images/addcontentrep3textdone.png)

您随后将看到以下内容：

![决策规则](./images/constraints.png)

选择&#x200B;**根据定义的决策规则**&#x200B;并单击&#x200B;**+**&#x200B;图标以添加规则&#x200B;**all - Female Customers**。

![决策规则](./images/constraints1.png)

你会看到这个。 如上表所示，填写&#x200B;**优先级**。 单击&#x200B;**下一步**。

![决策规则](./images/constraints2.png)

然后，您将看到新&#x200B;**个性化优惠**&#x200B;的概述。

![决策规则](./images/offeroverview.png)

最后，单击&#x200B;**保存并批准**。

![决策规则](./images/saveapprove.png)

然后，您将在选件概述中看到新创建的个性化选件变得可用：

![决策规则](./images/offeroverview1.png)

您现在应重复上述步骤，为Radiant Tee、Zeppelin Yoga Pant和Proteus Fitness Jackshirt产品创建其他三个个性化优惠。

完成后，您的&#x200B;**个性化优惠**&#x200B;的&#x200B;**优惠概述**&#x200B;屏幕应显示所有优惠。

![最终优惠](./images/finaloffers.png)

## 3.3.2.2创建您的后备优惠

创建四个个性化优惠后，您现在应配置&#x200B;**后备优惠**。

确保您处于&#x200B;**选件**&#x200B;视图中：

![最终优惠](./images/finaloffers.png)

单击&#x200B;**+创建选件**。

![决策规则](./images/createoffer.png)

然后您会看到此弹出窗口。 选择&#x200B;**后备优惠**&#x200B;并单击&#x200B;**下一步**。

![决策规则](./images/foffers2.png)

您随后将看到以下内容：

![决策规则](./images/foffers3.png)

为您的后备优惠输入此名称： `--aepUserLdap-- - Luma Fallback Offer`。 单击&#x200B;**下一步**。

![决策规则](./images/foffers4.png)

您现在需要创建&#x200B;**呈现**。 表示是&#x200B;**版面**&#x200B;和实际资源的组合。

对于&#x200B;**呈现1**，请选择：

- 渠道：Web
- 版面：Web — 图像
- 内容： URL
- 公共位置： `https://bit.ly/3nBOt9h`

![决策规则](./images/addcontent1fb.png)

或者，您也可以为内容选择&#x200B;**资源库**，然后单击&#x200B;**浏览**。

![决策规则](./images/addcontent2fb.png)

随后您将看到Assets库的弹出窗口，转到文件夹&#x200B;**enablement-assets**&#x200B;并选择图像文件&#x200B;**spriteyogastraps-web.png**。 然后，单击&#x200B;**选择**。

![决策规则](./images/addcontent3fb.png)

您随后将看到以下内容：

![决策规则](./images/addcontentrep20fb.png)

对于&#x200B;**呈现2**，请选择：

- 渠道：电子邮件
- 版面：电子邮件 — 图像
- 内容： URL
- 公共位置： `https://bit.ly/3nF4qvE`

![决策规则](./images/addcontentrep21fb.png)

或者，您也可以为内容选择&#x200B;**资源库**，然后单击&#x200B;**浏览**。

![决策规则](./images/addcontent2bfb.png)

随后您将看到Assets库的弹出窗口，转到文件夹&#x200B;**enablement-assets**&#x200B;并选择图像文件&#x200B;**spriteyogastraps-email.png**。 然后，单击&#x200B;**选择**。

![决策规则](./images/addcontent3bfb.png)

您随后将看到以下内容：

![决策规则](./images/addcontentrep20bfb.png)

接下来，单击&#x200B;**+添加呈现**。

![决策规则](./images/addrep.png)

对于&#x200B;**呈现3**，请选择：

- 渠道：非数字
- 版面：非数字 — 文本

接下来，您需要添加内容。 在这种情况下，这意味着添加图像链接。

单击&#x200B;**添加内容**。

![决策规则](./images/addcontentrep21text.png)

然后您会看到此弹出窗口。

![决策规则](./images/addcontent2text.png)

选择&#x200B;**自定义文本**&#x200B;并填写以下字段：

输入文本`{{ profile.person.name.firstName }}, discover our Sprite Yoga Straps!`并单击&#x200B;**保存**。

![决策规则](./images/faddcontent3text.png)

你会看到这个。 单击&#x200B;**下一步**。

![决策规则](./images/faddcontentrep3.png)

然后，您将看到新&#x200B;**后备优惠**&#x200B;的概述。 单击&#x200B;**完成**。

![决策规则](./images/fofferoverview.png)

最后，单击&#x200B;**保存并批准**。

![决策规则](./images/saveapprovefb.png)

在&#x200B;**选件概述**&#x200B;屏幕中，您现在将看到以下内容：

![最终优惠](./images/ffinaloffers.png)

## 3.3.2.3创建您的收藏集

收藏集用于&#x200B;**从个性化优惠列表中**&#x200B;筛选出优惠的子集，并将其用作决策的一部分，以加快决策过程。

转到&#x200B;**收藏集**。 单击&#x200B;**+创建收藏集**。

![决策规则](./images/collections.png)

然后您会看到此弹出窗口。 像这样配置您的收藏集。 单击&#x200B;**下一步**。

- 集合名称：使用`--aepUserLdap-- - Luma Collection`
- 选择&#x200B;**创建静态集合**。

![决策规则](./images/createcollectionpopup1.png)

在下一个屏幕中，选择您在上一个练习中创建的4个&#x200B;**个性化优惠**。 单击&#x200B;**保存**。

![决策规则](./images/createcollectionpopup2.png)

您现在将看到以下内容：

![决策规则](./images/colldone.png)

## 3.3.2.4创建决策

决策将投放位置、个性化优惠集合和备用优惠组合在一起，以供Offer decisioning引擎最终根据每个个性化的优惠特征（如优先级、资格限制和总/用户上限）为特定用户档案查找最佳优惠。

要配置您的&#x200B;**决策**，请转到&#x200B;**决策**。 单击&#x200B;**+创建活动**。

![决策规则](./images/activitydd.png)

您随后将看到以下内容：

![决策规则](./images/activity1.png)

填写这样的字段。 单击&#x200B;**下一步**。

- 名称： `--aepUserLdap-- - Luma Decision`
- 开始日期和时间：昨天
- 结束日期和时间：今天+ 1个月

![决策规则](./images/activity2.png)

在下一个屏幕中，您需要将投放位置添加到决策范围。 您需要为投放位置&#x200B;**Web — 图像**、**电子邮件 — 图像**&#x200B;和&#x200B;**非数字 — 文本**&#x200B;创建决策范围。

![决策规则](./images/addplacements.png)

首先，通过在下拉菜单中选择投放位置来创建&#x200B;**非数字型 — 文本**&#x200B;的决策范围。 然后，单击“**添加**”按钮以添加评估标准。

![决策规则](./images/activity3.png)

选择您的收藏集`--aepUserLdap-- - Luma Collection`并单击&#x200B;**添加**。

![决策规则](./images/activity4text.png)

你会看到这个。 单击&#x200B;**-**&#x200B;按钮以添加新决策范围。

![决策规则](./images/activity5text.png)

选择版面&#x200B;**Web — 图像**，并根据评估条件添加收藏集`--aepUserLdap-- - Luma Collection`。 然后，再次单击&#x200B;**+**&#x200B;按钮以添加新的决策范围。

![决策规则](./images/activity6text.png)

选择版面&#x200B;**电子邮件 — 图像**，并根据评估条件添加您的收藏集`--aepUserLdap-- - Luma Collection`。 然后，单击&#x200B;**下一步**。

![决策规则](./images/activity4.png)

您现在需要选择名为`--aepUserLdap-- - Luma Fallback Offer`的&#x200B;**备用选件**。 单击&#x200B;**下一步**。

![决策规则](./images/activity10.png)

查看您的决定。 单击&#x200B;**完成**。

![决策规则](./images/activity11.png)

在弹出窗口中，单击&#x200B;**保存并激活**。

![决策规则](./images/activity12.png)

最后，您将在概述中看到您的决策：

![决策规则](./images/activity13.png)

您现在已成功配置决策。 您的决策现已上线，并可用于实时为客户提供优化和个性化的优惠。

下一步： [3.3.3为Offer decisioning](./ex3.md)准备数据收集客户端属性和Web SDK设置

[返回模块3.3](./offer-decisioning.md)

[返回所有模块](./../../../overview.md)
