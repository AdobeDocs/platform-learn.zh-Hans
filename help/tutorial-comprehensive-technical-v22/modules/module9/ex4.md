---
title: offer decisioning — 使用演示网站测试您的决策
description: 使用演示网站测试您的决策
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: cdb2ba7d-bfc3-43ce-b9a1-1f0866322589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---

# 9.4将Adobe Target与Offer decisioning结合使用

## 9.4.1收集演示项目的可共享链接

要在Adobe Target中加载演示网站项目，您首先需要收集一个特殊链接，以允许Adobe Target加载您的演示网站项目。

为此，请转至 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用Adobe ID登录后，您将看到此内容。 单击您的网站项目以将其打开。

![RTCDP](./images/builder1.png)

你现在会看到这个。 单击&#x200B;**共享**。

![RTCDP](./images/builder2.png)

单击 **生成链接** 然后将链接复制到剪贴板。

![RTCDP](./images/builder3.png)

转到 [https://bitly.com](https://bitly.com)，粘贴您复制的链接并单击 **缩短**. 现在，您将获得一个缩短链接，该链接如下所示： `https://bit.ly/3JxN7aG`. 在下一个练习中，您将需要该链接。

![RTCDP](./images/builder4.png)

## 9.4.2收集

现在，转到Adobe Experience Cloud主页 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 单击 **Target**.

![RTCDP](../module6/images/excl.png)

在 **Adobe Target** 主页，您将看到所有现有活动。

![RTCDP](../module6/images/exclatov.png)

单击 **+创建活动** 创建新活动。

![RTCDP](../module6/images/exclatcr.png)

选择 **体验定位**.

![RTCDP](./images/exclatcrxt.png)

现在，选择 **可视** 并将您的短链接粘贴到字段中 **输入活动URL**. 单击&#x200B;**下一步**。

![RTCDP](./images/exclatcrxt1.png)

然后，您将看到在可视化体验编辑器中加载演示网站项目。

![RTCDP](./images/vec1.png)

转到 **浏览** 模式 **允许所有** 在Cookie同意弹出窗口中。

![RTCDP](./images/vec2.png)

单击包含文本的区域 **特色类别**. 单击 **此项前插入** 然后选择 **选件决策**.

![RTCDP](./images/vec3.png)

然后，您将看到此弹出窗口。 选择沙盒 `--aepSandboxId--` 然后选择版面 **Web — 图像**.

![RTCDP](./images/vec4.png)

接下来，选择您的决策 `--demoProfileLdap-- - Luma Decision`. 单击&#x200B;**保存**。

![RTCDP](./images/vec5.png)

然后你会看到这个。 确保添加其他模板规则 **URL** **包含** **your-project-name**. 快速 **保存**.

![RTCDP](./images/vec6.png)

然后你会看到这个。 单击&#x200B;**下一步**。

![RTCDP](./images/vec7.png)

输入选件的名称，请使用此名称： `--demoProfileLdap-- - XT with Offers (VEC)`. 单击&#x200B;**下一步**。

![RTCDP](./images/vec8.png)

然后你会看到这个。 定义 **目标量度** 如所示。 单击“**保存并关闭**”。

![RTCDP](./images/vec9.png)

您的选件现已创建并正在发布。

![RTCDP](./images/vec10.png)

发布选件后，即可启用它。

下一步： [9.5通过电子邮件和短信使用您的决策](./ex5.md)

[返回模块9](./offer-decisioning.md)

[返回到所有模块](./../../overview.md)
