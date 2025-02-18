---
title: 使用AJO翻译服务创建营销活动
description: 使用AJO翻译服务创建营销活动
kt: 5342
doc-type: tutorial
exl-id: 536caf45-c614-48e8-adbb-6dc67d1a9606
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# 3.5.2创建营销活动

转到[https://experience.adobe.com/](https://experience.adobe.com/)。 单击&#x200B;**Journey Optimizer**。

![翻译](./images/ajolp1.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。

![ACOP](./images/ajolp2.png)

>[!NOTE]
>
>如果您已在练习[练习3.1.2.1](./../ajob2c-1/ex2.md)和[练习3.1.2.2](./../ajob2c-1/ex2.md)中创建了页眉和页脚片段，请跳到练习3.5.2.3创建光纤营销活动。 不再创建您的页眉和页脚片段。

## 3.5.2.1创建您的标头片段

在左侧菜单中，单击&#x200B;**片段**。 片段是Journey Optimizer中可重用的组件，可避免重复并便于将来进行应当影响所有消息的更改，例如对电子邮件中的页眉或页脚的更改。

单击&#x200B;**创建片段**。

![ACOP](./images/fragm1.png)

输入名称`--aepUserLdap-- - CitiSignal - Header`并选择&#x200B;**类型：可视片段**。 单击&#x200B;**创建**。

![ACOP](./images/fragm2.png)

你会看到这个。 在左侧菜单中，您将找到可用于定义电子邮件结构（行和列）的结构组件。

将&#x200B;**1:1列**&#x200B;从菜单拖放到画布中。 这将是徽标图像的占位符。

![Journey Optimizer](./images/fragm3.png)

接下来，您可以使用内容组件在这些块中添加内容。 将&#x200B;**Image**&#x200B;组件拖放到第一行的第一个单元格中。 单击&#x200B;**浏览**。

![Journey Optimizer](./images/fragm4.png)

然后，您将看到一个弹出窗口打开，其中显示您的AEM Assets媒体库。 转到文件夹&#x200B;**citi-signal-images**，单击以选择图像&#x200B;**CitiSignal-Logo-White.png**，然后单击&#x200B;**选择**。

>[!NOTE]
>
>如果您在AEM Assets库中看不到Citi Signal图像，您可以在[此处](./../../../../assets/ajo/CitiSignal-images.zip)找到它们。 将它们下载到桌面，创建文件夹&#x200B;**citi-signal-images**，然后上传该文件夹中的所有图像。

![Journey Optimizer](./images/fragm5.png)

你会看到这个。 您的图像是白色的，尚未显示。 您现在应该定义背景颜色，以使图像正确显示。 单击&#x200B;**样式**，然后单击&#x200B;**背景颜色**&#x200B;框。

![Journey Optimizer](./images/fragm6.png)

在弹出窗口中，将&#x200B;**十六进制**&#x200B;颜色代码更改为&#x200B;**#8821F4**，然后通过单击&#x200B;**100%**&#x200B;字段来更改焦点。 然后，您会看到应用于图像的新颜色。

![Journey Optimizer](./images/fragm7.png)

现在这个图像也有点大。 让我们将&#x200B;**宽度**&#x200B;切换器滑动到&#x200B;**40%**&#x200B;以更改宽度。

![Journey Optimizer](./images/fragm8.png)

您的标头片段现已准备就绪。 单击&#x200B;**保存**，然后单击箭头返回上一屏幕。

![Journey Optimizer](./images/fragm9.png)

您的片段需要先发布，然后才能使用。 单击&#x200B;**发布**。

![Journey Optimizer](./images/fragm10.png)

几分钟后，您会看到片段的状态已更改为&#x200B;**实时**。
接下来，您应该为电子邮件的页脚创建新片段。 单击**创建片段**。

![Journey Optimizer](./images/fragm11.png)

## 3.5.2.2创建页脚片段

单击&#x200B;**创建片段**。

![Journey Optimizer](./images/fragm11.png)

输入名称`--aepUserLdap-- - CitiSignal - Footer`并选择&#x200B;**类型：可视片段**。 单击&#x200B;**创建**。

![Journey Optimizer](./images/fragm12.png)

你会看到这个。 在左侧菜单中，您将找到可用于定义电子邮件结构（行和列）的结构组件。

将&#x200B;**1:1列**&#x200B;从菜单拖放到画布中。 这将是页脚内容的占位符。

![Journey Optimizer](./images/fragm13.png)

接下来，您可以使用内容组件在这些块中添加内容。 将&#x200B;**HTML**&#x200B;组件拖放到第一行的第一个单元格中。 单击组件以将其选中，然后单击&#x200B;**&lt;/>**&#x200B;图标以编辑HTML源代码。

![Journey Optimizer](./images/fragm14.png)

你会看到这个。

![Journey Optimizer](./images/fragm15.png)

复制以下HTML代码片段并将其粘贴到Journey Optimizer中的&#x200B;**编辑HTML**&#x200B;窗口中。

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

你就能拥有这个了。 在第7、12和17行，您现在需要使用AEM Assets库中的资源插入图像文件。

![Journey Optimizer](./images/fragm16.png)

确保光标位于第7行，然后单击左侧菜单中的&#x200B;**Assets**。 单击&#x200B;**打开资产选择器**&#x200B;以选择您的图像。

![Journey Optimizer](./images/fragm17.png)

打开文件夹&#x200B;**citi-signal-images**，然后单击选择图像&#x200B;**Icon_Facebook.png**。 单击&#x200B;**选择**。

![Journey Optimizer](./images/fragm18.png)

确保光标位于第12行，然后单击&#x200B;**打开资产选择器**&#x200B;以选择图像。

![Journey Optimizer](./images/fragm19.png)

打开文件夹&#x200B;**citi-signal-images**，然后单击选择图像&#x200B;**Icon_X.png**。 单击&#x200B;**选择**。

![Journey Optimizer](./images/fragm20.png)

确保光标位于第17行，然后单击&#x200B;**打开资产选择器**&#x200B;以选择图像。

![Journey Optimizer](./images/fragm21.png)

打开文件夹&#x200B;**citi-signal-images**&#x200B;并单击以选择图像&#x200B;**Icon_Instagram.png**。 单击&#x200B;**选择**。

![Journey Optimizer](./images/fragm22.png)

你会看到这个。 单击&#x200B;**保存**。

![Journey Optimizer](./images/fragm23.png)

然后你就可以回到编辑器中了。 您的图标尚未显示，因为背景和图像文件全部为白色。 若要更改背景颜色，请转到&#x200B;**样式**&#x200B;并单击&#x200B;**背景颜色**&#x200B;复选框。

![Journey Optimizer](./images/fragm24.png)

将&#x200B;**十六进制**&#x200B;颜色代码更改为&#x200B;**#000000**。

![Journey Optimizer](./images/fragm25.png)

将对齐方式更改为居中。

![Journey Optimizer](./images/fragm26.png)

让我们在页脚中添加一些其他部分。 将&#x200B;**Image**&#x200B;组件拖放到刚刚创建的HTML组件上方。 单击&#x200B;**浏览**。

![Journey Optimizer](./images/fragm27.png)

单击选择图像文件&#x200B;**`CitiSignal_Footer_Logo.png`**&#x200B;并单击&#x200B;**选择**。

![Journey Optimizer](./images/fragm28.png)

转到&#x200B;**样式**&#x200B;并单击&#x200B;**背景颜色**&#x200B;复选框，让我们将其再次更改为黑色。 将&#x200B;**十六进制**&#x200B;颜色代码更改为&#x200B;**#000000**。

![Journey Optimizer](./images/fragm29.png)

将宽度更改为&#x200B;**20%**&#x200B;并验证对齐方式是否设置为居中。

![Journey Optimizer](./images/fragm30.png)

接下来，将&#x200B;**Text**&#x200B;组件拖放到您创建的HTML组件下。 单击&#x200B;**浏览**。

![Journey Optimizer](./images/fragm31.png)

通过替换占位符文本来复制并粘贴以下文本。

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

将&#x200B;**文本对齐方式**&#x200B;设置为居中。

![Journey Optimizer](./images/fragm32.png)

将&#x200B;**字体颜色**&#x200B;更改为白色，**#FFFFFF**。

![Journey Optimizer](./images/fragm33.png)

将&#x200B;**背景颜色**&#x200B;更改为黑色，**#000000**。

![Journey Optimizer](./images/fragm34.png)

选择页脚中的文本&#x200B;**取消订阅**，然后单击菜单栏中的&#x200B;**链接**&#x200B;图标。 将&#x200B;**Type**&#x200B;设置为&#x200B;**外部选择退出/取消订阅**，并将URL设置为&#x200B;**https://aepdemo.net/unsubscribe.html**（取消订阅链接不允许有空白URL）。

![Journey Optimizer](./images/fragm35.png)

你就能拥有这个了。 您的页脚现已准备就绪。 单击&#x200B;**保存**，然后单击箭头返回上一页。

![Journey Optimizer](./images/fragm36.png)

单击&#x200B;**发布**&#x200B;发布您的页脚，以便将其用在电子邮件中。

![Journey Optimizer](./images/fragm37.png)

几分钟后，您会看到页脚的状态已更改为&#x200B;**实时**。

![Journey Optimizer](./images/fragm38.png)

## 3.5.2.3创建光纤营销活动

您现在将创建一个营销活动。 上一个练习基于事件的历程依赖于传入体验事件或受众进入或退出来触发1个特定客户的历程，与此不同的是，营销活动面向整个受众一次，其中包含新闻稿、一次性促销活动或通用信息等独特内容，或者定期发送类似内容，如实例生日营销活动和提醒。

在菜单中，转到&#x200B;**营销活动**&#x200B;并单击&#x200B;**创建营销活动**。

![Journey Optimizer](./images/oc43.png)

选择&#x200B;**计划 — 营销**，然后单击&#x200B;**创建**。

![Journey Optimizer](./images/campaign1.png)

在营销活动创建屏幕上，配置以下内容：

- **名称**： `--aepUserLdap-- - CitiSignal Fiber`。
- **描述**：光纤营销活动
- **身份类型**：更改为电子邮件

![Journey Optimizer](./images/campaign2.png)

向下滚动至&#x200B;**操作**。 对于&#x200B;**操作**，请选择&#x200B;**电子邮件**。

![Journey Optimizer](./images/campaign3.png)

然后，选择现有的&#x200B;**电子邮件配置**。 你将在几分钟后编辑内容。

![Journey Optimizer](./images/campaign3a.png)

向上滚动到&#x200B;**受众**。 单击&#x200B;**选择受众**。

![Journey Optimizer](./images/campaign2b.png)

对于&#x200B;**受众**，请选择您在[1.3.3中创建的受众，以创建名为`--aepUserLdap-- - CitiSignal Eligible for Fiber`的联合合成](./../../datacollection/dc1.3/ex3.md)。 单击&#x200B;**保存**。

![Journey Optimizer](./images/campaign2a.png)

向下滚动到&#x200B;**计划**。 对于&#x200B;**计划**，请选择&#x200B;**在特定日期和时间**&#x200B;并设置所选时间。

![Journey Optimizer](./images/campaign4.png)

您现在可以开始创建电子邮件本身。 向上滚动，然后单击&#x200B;**编辑内容**。

![Journey Optimizer](./images/campaign5.png)

你会看到这个。 对于&#x200B;**主题行**，请使用以下内容：

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

接下来，单击&#x200B;**编辑电子邮件正文**。

![Journey Optimizer](./images/campaign6.png)

从头开始选择&#x200B;**设计**。

![Journey Optimizer](./images/campaign7.png)

你会看到这个。 在左侧菜单中，您将找到可用于定义电子邮件结构（行和列）的结构组件。

将&#x200B;**1:1列**&#x200B;拖放到画布上4次，这会为您提供以下结构：

![Journey Optimizer](./images/campaign8.png)

在左侧菜单中，转到&#x200B;**片段**。 将之前创建的标题拖到画布中的第一个组件上。 将之前创建的页脚拖到画布中的最后一个组件上。

![Journey Optimizer](./images/campaign9.png)

单击左侧菜单中的&#x200B;**+**&#x200B;图标。 转到&#x200B;**Contents**&#x200B;以开始将内容添加到画布上。

![Journey Optimizer](./images/campaign10.png)

将&#x200B;**Text**&#x200B;组件拖放到第二行。

![Journey Optimizer](./images/campaign11.png)

选择该组件中的默认文本&#x200B;**请在此处键入您的文本。**&#x200B;并将其替换为以下文本。 将对齐方式更改为&#x200B;**居中对齐**。

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal customer, you're in pole position to discover our new Fiber offering. Have a look at the below offer and update your contract!

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

将&#x200B;**Image**&#x200B;组件拖放到第3行。 单击&#x200B;**浏览**。

![Journey Optimizer](./images/campaign13.png)

选择您在前面的模块中创建的AEM Assets存储库。 该存储库应命名为`--aepUserLdap-- - Citi Signal dev`。 单击以打开文件夹`--aepUserLdap-- - Workfront Assets`。

![Journey Optimizer](./images/campaign15a.png)

单击以选择图像&#x200B;**2048x2048_buynow.png**，然后单击&#x200B;**选择**。

![Journey Optimizer](./images/campaign14.png)

您的基本新闻稿电子邮件现已准备就绪。 单击&#x200B;**保存**。

![Journey Optimizer](./images/ready.png)

单击左上角主题行文本旁边的&#x200B;**箭头**，返回营销活动仪表板。

![Journey Optimizer](./images/campaign19.png)

单击&#x200B;**查看以激活**。

![Journey Optimizer](./images/campaign20.png)

然后，您可能会收到此错误。 如果是这种情况，您可能需要等待长达24小时，直到评估受众，然后尝试再次激活您的营销活动。 您可能还需要更新营销活动计划，以便稍后运行。

![Journey Optimizer](./images/campaign21a.png)

单击&#x200B;**激活**。

![Journey Optimizer](./images/campaign21.png)

激活后，您的营销活动将计划运行。

![Journey Optimizer](./images/campaign22.png)

您已完成此练习。

## 后续步骤

转到[3.5.3向电子邮件添加语言](./ex3.md)

返回[Adobe Journey Optimizer：翻译服务](./ajotranslationsvcs.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
