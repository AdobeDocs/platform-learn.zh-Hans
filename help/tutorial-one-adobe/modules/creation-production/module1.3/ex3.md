---
title: GenStudio for Performance Marketing Campaign对元数据的激活
description: GenStudio for Performance Marketing Campaign对元数据的激活
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2c7ef715-b8af-4a5b-8873-5409b43d7cb0
source-git-commit: b8f7b370a5aba82a0dcd6e7f4f0222fe209976f7
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 1.3.3 Campaign对元数据的激活

>[!IMPORTANT]
>
>要完成本练习，您需要有权访问启用了AEM Content Hub的有效AEM Assets CS创作环境。 如果您按照练习[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}，您将有权访问此类环境。

>[!IMPORTANT]
>
>如果您之前已使用Author和AEM Assets环境配置了AEM Assets CS项目，则可能是您的AEM CS沙盒已休眠。 鉴于解除此类沙盒的休眠需要10-15分钟，最好现在就启动解除休眠过程，这样以后就不必等待它。

## 1.3.3.1创建营销活动

在&#x200B;**GenStudio for Performance Marketing**&#x200B;中，转到左侧菜单中的&#x200B;**促销活动**。 单击&#x200B;**+添加营销活动**。

![GSPeM](./images/gscampaign1.png)

然后，您应该会看到空的活动概述。

![GSPeM](./images/gscampaign2.png)

对于字段名称，请使用`--aepUserLdap-- - CitiSignal Fiber Launch Campaign`。

对于字段&#x200B;**Description**，请使用以下文本。

```
The CitiSignal Fiber Launch campaign introduces CitiSignal’s flagship fiber internet service—CitiSignal Fiber Max—to key residential markets. This campaign is designed to build awareness, drive sign-ups, and establish CitiSignal as the go-to provider for ultra-fast, reliable, and future-ready internet. The campaign will highlight the product’s benefits for remote professionals, online gamers, and smart home families, using persona-driven messaging across digital and physical channels.
```

对于字段&#x200B;**目标**，请使用以下文本。

```
Generate brand awareness in target regions
Drive early sign-ups and pre-orders for CitiSignal Fiber Max
Position CitiSignal as a premium, customer-first fiber internet provider
Educate consumers on the benefits of fiber over cable or DSL
```

对于字段&#x200B;**关键消息**，请使用以下文本。

```
Supporting Points:
Symmetrical speeds up to 2 Gbps
Whole-home Wi-Fi 6E coverage
99.99% uptime guarantee
24/7 concierge support
No data caps or throttling
 Channels:
Digital Advertising: Google Display, YouTube pre-roll, Meta (Facebook/Instagram), TikTok (for gamers)
Email Marketing: Persona-segmented drip campaigns
Social Media: Organic and paid posts with testimonials, speed demos, and influencer partnerships
Out-of-Home (OOH): Billboards, transit ads in suburban commuter corridors
Local Events: Pop-up booths at tech expos, family festivals, and gaming tournaments
Direct Mail: Personalized flyers with QR codes for early sign-up discounts
 
Target Regions:
Primary Launch Markets:
Denver Metro Area, CO
Austin, TX
Raleigh-Durham, NC
Salt Lake City, UT
Demographic Focus:
Suburban neighborhoods with high remote work density
Areas with high smart home adoption
Zip codes with underserved or dissatisfied cable customers
```

然后，您应该拥有以下权限：

![GSPeM](./images/gscampaign3.png)

向下滚动查看更多字段：

![GSPeM](./images/gscampaign4.png)

对于字段&#x200B;**开始**，将其设置为今天的日期。

对于字段&#x200B;**End**，将其设置为自即日起1个月的日期。

对于字段&#x200B;**状态**，将其设置为&#x200B;**活动**。

对于字段&#x200B;**渠道**，请将其设置为&#x200B;**Meta**，**电子邮件**，**付费媒体**，**显示**。

对于字段&#x200B;**Regions**，请选择所选区域。

对于字段&#x200B;**References** > **Products**&#x200B;的字段：选择产品`--aepUserLdap-- - CitiSignal Fiber Max`。

**引用** > **角色**：选择角色`--aepUserLdap-- - Remote Professionals`、`--aepUserLdap-- - Online Gamers`、`--aepUserLdap-- - Smart Home Families`

您应该会看到以下内容：

![GSPeM](./images/gscampaign5.png)

您的营销活动现已准备就绪。 单击&#x200B;**箭头**&#x200B;以返回。

![GSPeM](./images/gscampaign6.png)

然后，您将在列表中看到营销活动。 单击日历视图图标以将视图更改为营销活动日历。

![GSPeM](./images/gscampaign7.png)

然后，您应该会看到营销活动日历，该日历可让您更直观地了解哪些营销活动在哪个时刻处于活动状态。

![GSPeM](./images/gscampaign8.png)

## 1.3.3.2设置与元的连接

>[!IMPORTANT]
>
>要设置与Meta的连接，您需要具有可用的Meta用户帐户，并且需要将该用户帐户添加到Meta Business帐户。

要设置到Meta的连接，请单击3个点&#x200B;**...**，然后选择&#x200B;**设置**。

![GSPeM](./images/gsconnection1.png)

单击&#x200B;**元广告**&#x200B;的&#x200B;**连接**。

![GSPeM](./images/gsconnection2.png)

使用您的元帐户登录。 单击&#x200B;**继续**。

![GSPeM](./images/gsconnection3.png)

如果您的帐户关联到Meta Business帐户，您将能够选择已在Meta中配置的业务组合。

![GSPeM](./images/gsconnection5.png)

成功建立连接后，单击显示&#x200B;**X已连接帐户**&#x200B;的行。

![GSPeM](./images/gsconnection4.png)

然后，您应该会看到连接到GenStudio for Performance Marketing的元业务帐户的详细信息。

![GSPeM](./images/gsconnection6.png)

## 1.3.3.3创建新资源

转到[https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}。 输入提示`a neon rabbit running very fast through space`并单击&#x200B;**生成**。

![GSPeM](./images/gsasset1.png)

然后，您将看到正在生成的多个图像。 选择您最喜欢的图像，单击图像上的&#x200B;**共享**&#x200B;图标，然后选择&#x200B;**在Adobe Express中打开**。

![GSPeM](./images/gsasset2.png)

然后，您将看到刚刚生成的图像在Adobe Express中可用于编辑。 您现在需要在图像上添加CitiSignal徽标。 为此，请转到&#x200B;**品牌**。

![GSPeM](./images/gsasset3.png)

然后，您应该会看到在GenStudio for Performance Marketing中创建的CitiSignal品牌模板出现在Adobe Express中。 单击以选择应命名为`--aepUserLdap-- - CitiSignal`的品牌模板。

![GSPeM](./images/gsasset4.png)

转到&#x200B;**徽标**&#x200B;并单击&#x200B;**白色** Citisignal徽标将其放到图像上。

![GSPeM](./images/gsasset5.png)

将CitiSignal徽标放在左上角。

![GSPeM](./images/gsasset6.png)

接下来，单击&#x200B;**共享**。

![GSPeM](./images/gsasset7.png)

选择&#x200B;**AEM Assets**。

![GSPeM](./images/gsasset8.png)

单击&#x200B;**选择文件夹**。

![GSPeM](./images/gsasset9.png)

选择您的AEM Assets CS存储库（应命名为`--aepUserLdap-- - CitiSignal`），然后选择文件夹`--aepUserLdap-- - CitiSignal Fiber Campaign`。 单击&#x200B;**选择**。

![GSPeM](./images/gsasset11.png)

您应该会看到此内容。 单击&#x200B;**上传1项资源**。 您的图像现在将上传到AEM Assets CS。

![GSPeM](./images/gsasset12.png)

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 打开&#x200B;**Experience Manager Assets**。

![GSPeM](./images/gsasset13.png)

选择您的AEM Assets CS环境，应将其命名为`--aepUserLdap-- - CitiSignal dev`。

![GSPeM](./images/gsasset14.png)

转到&#x200B;**Assets**，然后双击文件夹`--aepUserLdap-- - CitiSignal Fiber Campaign`。

![GSPeM](./images/gsasset15.png)

然后，您应该会看到类似以下的内容。 双击图像`--aepUserLdap-- - neon rabbit`。

![GSPeM](./images/gsasset16.png)

随后将显示图像`--aepUserLdap-- - neon rabbit`。 将&#x200B;**状态**&#x200B;更改为&#x200B;**已批准**，然后单击&#x200B;**保存**

>[!IMPORTANT]
>
>如果图像的状态未设置为&#x200B;**已批准**，则图像在GenStudio for Performance Marketing中将不可见。 在GenStudio for Performance Marketing中，只能访问已批准的资源。

![GSPeM](./images/gsasset17.png)

切换回GenStudio for Performance Marketing。 在左侧菜单中，转到&#x200B;**Assets**&#x200B;并选择您的AEM Assets CS存储库，该存储库应名为`--aepUserLdap-- - CitiSignal`。 然后，您将看到之前创建并批准的图像在GenStudio for Performance Marketing中可用。

![GSPeM](./images/gsasset18.png)

## 1.3.3.4创建和批准元广告

## 1.3.3.5将广告发布到元

## 后续步骤

转到[摘要和优点](./summary.md){target="_blank"}

返回[GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
