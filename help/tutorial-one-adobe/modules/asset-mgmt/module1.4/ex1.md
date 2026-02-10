---
title: 创建资源和Dynamic Media模板
description: 创建资源和Dynamic Media模板
kt: 5342
doc-type: tutorial
exl-id: 3867f23b-9b88-4971-a892-5821800e39ac
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 0%

---

# 1.4.1创建资产和Dynamic Media模板

>[!IMPORTANT]
>
>要完成本练习，您需要有权访问启用了AEM Assets Dynamic Media的有效AEM Assets CS创作环境。
>
>如果没有此类环境，请转到[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照上面的说明进行操作，您将有权访问此类环境。

>[!IMPORTANT]
>
>如果您之前已使用AEM CS环境配置了AEM Assets CS项目，则可能是您的AEM CS沙盒已休眠。 鉴于解除此类沙盒的休眠需要10-15分钟，最好现在就启动解除休眠过程，这样以后就不必等待它。

## 1.4.1.1创建您的Dynamic Media公司

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 您应选择的组织是`--aepImsOrgName--`。

![AEM Assets Dynamic Media](./images/aaemassdmcomp1.png)

向下滚动到&#x200B;**Dynamic Media公司**。 单击&#x200B;**+**&#x200B;图标以创建新的Dynamic Media公司。

![AEM Assets Dynamic Media](./images/aaemassdmcomp2.png)

输入以下信息：

- **公司名称**： `--aepUserLdap---CitiSignal`。
- **公司区域**：选择离您最近的区域。
- **公司管理员电子邮件**：输入您的管理员电子邮件。

单击&#x200B;**创建**。

![AEM Assets Dynamic Media](./images/aaemassdmcomp3.png)

您应该会看到此内容。

![AEM Assets Dynamic Media](./images/aaemassdmcomp4.png)

现在，您应会收到类似于以下内容的电子邮件，其中包含您的临时密码。 要更改密码，或者如果未收到电子邮件则检索密码，您应该安装&#x200B;**Adobe Dynamic Media Classic桌面应用程序**。 您可以在此处找到安装说明： [https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app)。

按照该处的说明操作，并在您的系统上安装应用程序后返回此处。

打开&#x200B;**Adobe Dynamic Media Classic桌面应用程序**。 如果您知道密码，请在此处输入密码，然后按照说明在首次登录时更改密码。

如果您不知道密码，请单击&#x200B;**忘记密码**&#x200B;链接并按照说明重置密码，然后返回此处登录。

![AEM Assets Dynamic Media](./images/aaemassdmcomp5.png)

成功登录后，您应该会看到一个类似于此内容的屏幕。

![AEM Assets Dynamic Media](./images/aaemassdmcomp6.png)

## 1.4.1.2在AEM中配置Dynamic Media

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 您应选择的组织是`--aepImsOrgName--`。

单击以打开您的Cloud Manager项目，该项目应称为`--aepUserLdap-- - CitiSignal AEM+ACCS`。

![AEM Assets Dynamic Media](./images/accsaemassets1.png)

单击您的环境。

![AEM Assets Dynamic Media](./images/accsaemassets3.png)

单击环境的URL。

![AEM Assets Dynamic Media](./images/accsaemassets2.png)

转到&#x200B;**工具**，转到&#x200B;**云服务**，然后转到&#x200B;**Dynamic Media配置**。

![AEM Assets Dynamic Media](./images/accsaemassets4.png)

选择&#x200B;**全局**（不要选中该复选框），然后单击&#x200B;**创建**。

![AEM Assets Dynamic Media](./images/accsaemassets5.png)

输入以下信息：

- **标题**：使用此标题： `--aepUserLdap-- - CitiSignal`。
- **电子邮件**：输入您的电子邮件地址。
- **密码**：输入您的Dynamic Media帐户密码
- **地区**：选择您在创建Dynamic Media公司时选择的地区，在本例中为&#x200B;**欧洲**。

单击&#x200B;**连接到Dynamic Media**。

![AEM Assets Dynamic Media](./images/accsaemassets6.png)

您应该会看到此内容。 配置以下内容：

- 选择&#x200B;**公司**： `--aepUserLdap-- - CitiSignal`。
- 将&#x200B;**发布Assets**&#x200B;设置为&#x200B;**立即**。
- 选中此复选框以&#x200B;**同步所有内容**。

单击&#x200B;**保存**。

![AEM Assets Dynamic Media](./images/accsaemassets7.png)

您的DYNAMIC Media配置现已完成。 单击&#x200B;**确定**。

![AEM Assets Dynamic Media](./images/accsaemassets8.png)

## 1.4.1.3导出您的资源

下载此文件[citisignal-fiber-max-is-coming.psd](./assets/citisignal-fiber-max-is-coming.psd){target="_blank"}，然后使用Adobe Photoshop将其打开。

您应该会看到此内容。 花旗信号正计划在纽约、巴黎和迪拜这3个城市推出Fiber Max。

通过显示或隐藏特定图层，可以查看设计者创建的图像。

以下是从Photoshop PSD模板导出图像文件的说明。 您也可以从这里[citisignal-dm-email-assets.zip](./assets/citisignal-dm-email-assets.zip){target="_blank"}下载完成的图像，并将文件解压缩到桌面上。

这是纽约的版本。

![AEM Assets Dynamic Media](./images/aemdm1.png)

这是迪拜的版本。

![AEM Assets Dynamic Media](./images/aemdm2.png)

这是巴黎的版本。

![AEM Assets Dynamic Media](./images/aemdm3.png)

将来可能会有许多其他城市CitiSignal将推出Fibre Max，因此可能会在此文件中创建新层。 目前，关注焦点集中在已提到的3个城市。

为了将这些变体与AEM Assets Dynamic Media结合使用，应单独将每个城市的图层导出为图像，而不使用背景文件，并且还应对背景图层进行另一次导出，而不包含任何城市。

现在，您应该只隐藏并显示其中一个图层。 要显示的第一个图层是&#x200B;**Paris**&#x200B;图层，所有其他图层都应隐藏。

要导出该图层，请转到&#x200B;**文件** > **导出** > **导出为……**。

![AEM Assets Dynamic Media](./images/aemdm4.png)

您应该会看到此内容。 选择文件类型&#x200B;**PNG**，确保启用了&#x200B;**透明度**，然后单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm5.png)

将文件名更改为`citisignal-fiber-max-is-coming-paris.png`并单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm6.png)

要显示的下一层是&#x200B;**Dubai**&#x200B;层，所有其他层都应隐藏。

要导出该图层，请转到&#x200B;**文件** > **导出** > **导出为……**。

![AEM Assets Dynamic Media](./images/aemdm4a.png)

您应该会看到此内容。 选择文件类型&#x200B;**PNG**，确保启用了&#x200B;**透明度**，然后单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm5a.png)

将文件名更改为`citisignal-fiber-max-is-coming-dubai.png`并单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm6a.png)

下一个要显示的图层是&#x200B;**New York**&#x200B;图层，所有其他图层都应隐藏。

要导出该图层，请转到&#x200B;**文件** > **导出** > **导出为……**。

![AEM Assets Dynamic Media](./images/aemdm4b.png)

您应该会看到此内容。 选择文件类型&#x200B;**PNG**，确保启用了&#x200B;**透明度**，然后单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm5b.png)

将文件名更改为`citisignal-fiber-max-is-coming-newyork.png`并单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm6b.png)

下一个要显示的图层是&#x200B;**背景**&#x200B;图层，所有其他图层都应隐藏。

要导出该图层，请转到&#x200B;**文件** > **导出** > **导出为……**。

![AEM Assets Dynamic Media](./images/aemdm4c.png)

您应该会看到此内容。 选择文件类型&#x200B;**PNG**，确保启用了&#x200B;**透明度**，然后单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm5c.png)

将文件名更改为`citisignal-fiber-max-is-coming-background`并单击&#x200B;**导出**。

![AEM Assets Dynamic Media](./images/aemdm6c.png)

然后，您应该将这些文件放在所选的导出位置中。

![AEM Assets Dynamic Media](./images/aemdm7.png)

## 1.4.1.4将您的资源上传到AEM Assets CS

转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 转到&#x200B;**Experience Manager Assets**。

![AEM Assets Dynamic Media](./images/aemdm8.png)

选择您的存储库，其名称应为`--aepUserLdap-- - CitiSignal AEM + ACCS`。

![AEM Assets Dynamic Media](./images/aemdm9.png)

转到&#x200B;**Assets**，然后单击&#x200B;**创建文件夹**。

![AEM Assets Dynamic Media](./images/aemdm10.png)

对于文件夹，请使用名称： `--aepUserLdap-- - CitiSignal Dynamic Media`。 单击&#x200B;**创建**。

![AEM Assets Dynamic Media](./images/aemdm11.png)

双击以打开刚刚创建的文件夹。

![AEM Assets Dynamic Media](./images/aemdm12.png)

单击&#x200B;**添加Assets**。

![AEM Assets Dynamic Media](./images/aemdm13.png)

单击&#x200B;**浏览**，然后选择&#x200B;**浏览文件**。

![AEM Assets Dynamic Media](./images/aemdm15.png)

选择在上一步中导出的4个PNG文件。

![AEM Assets Dynamic Media](./images/aemdm16.png)

单击&#x200B;**上传**。

![AEM Assets Dynamic Media](./images/aemdm17.png)

您的图像现在可在AEM Assets CS中使用。

![AEM Assets Dynamic Media](./images/aemdm18.png)

等待几分钟，然后打开&#x200B;**Adobe Dynamic Media Classic桌面应用程序**，您现在应该也会看到上传的图像在Dynamic Media中变得可用。

![AEM Assets Dynamic Media](./images/aemdm19.png)

## 1.4.1.5配置Dynamic Media模板

在左侧菜单中，转到&#x200B;**Dynamic Media Assets**。 单击以打开您的文件夹`--aepUserLdap-- - CitiSignal Dynamic Media`。 然后单击&#x200B;**创建模板**。

![AEM Assets Dynamic Media](./images/aemdm20.png)

输入以下信息：

- **模板名称**： `--aepUserLdap-- - CitiSignal Fiber Max Launch Email Assets`
- **画布宽度**： `600px`
- **画布高度**： `600px`

单击&#x200B;**创建**。

![AEM Assets Dynamic Media](./images/aemdm21.png)

您应该会看到此内容。 单击&#x200B;**添加图像**&#x200B;图标。

![AEM Assets Dynamic Media](./images/aemdm22.png)

将文件&#x200B;**citisignal-fiber-max-is-coming_citisignal-background.png**&#x200B;拖动到画布上，使其适合画布。

![AEM Assets Dynamic Media](./images/aemdm23.png)

接下来，将文件&#x200B;**citisignal-fiber-max-is-coming_citisignal-newyork.png**&#x200B;拖动到画布上，使其适合画布。

![AEM Assets Dynamic Media](./images/aemdm24.png)

接下来，将文件&#x200B;**citisignal-fiber-max-is-coming_citisignal-dubai.png**&#x200B;拖动到画布上，使其适合画布。

![AEM Assets Dynamic Media](./images/aemdm25.png)

接下来，将文件&#x200B;**citisignal-fiber-max-is-coming_citisignal-paris.png**&#x200B;拖动到画布上，使其适合画布。

![AEM Assets Dynamic Media](./images/aemdm26.png)

现在，模板中的所有3个变体同时作为不同的层。 通过单击&#x200B;**图层**&#x200B;图标，您可以显示/隐藏特定图层，在该图标中，您可以看到所有图层当前均可见。

![AEM Assets Dynamic Media](./images/aemdm27.png)

通过隐藏几个图层，您可以控制图像的外观。 在此示例中，只有&#x200B;**Paris**&#x200B;的图层以及背景图层可见。

![AEM Assets Dynamic Media](./images/aemdm28.png)

接下来，您需要添加文本图层。 单击&#x200B;**文本图层**&#x200B;图标。

![AEM Assets Dynamic Media](./images/aemdm29.png)

您应该会看到此内容。

![AEM Assets Dynamic Media](./images/aemdm30.png)

您可以随意调整文本字段，无论您认为哪种适合，以下是一个示例。 不要忘记启用选项&#x200B;**智能文本调整大小**，以便在以后插入的真实文本看起来不会有问题。

![AEM Assets Dynamic Media](./images/aemdm31.png)

添加第二个文本图层，使其看起来像这样。 不要忘记启用选项&#x200B;**智能文本调整大小**，以便在以后插入的真实文本看起来不会有问题。

![AEM Assets Dynamic Media](./images/aemdm32.png)

选择第一个文本图层。 单击这3个点&#x200B;**...**，然后选择&#x200B;**编辑**。

![AEM Assets Dynamic Media](./images/aemdm33.png)

您应该会看到此内容。 向下滚动。

![AEM Assets Dynamic Media](./images/aemdm34.png)

单击&#x200B;**switcher**&#x200B;图标，以启用字段&#x200B;**Text**。 将&#x200B;**参数名称**&#x200B;更改为`title`。

![AEM Assets Dynamic Media](./images/aemdm35.png)

选择第二个文本图层。 单击这3个点&#x200B;**...**，然后选择&#x200B;**编辑**。

![AEM Assets Dynamic Media](./images/aemdm36.png)

您应该会看到此内容。 向下滚动。

![AEM Assets Dynamic Media](./images/aemdm37.png)

单击&#x200B;**switcher**&#x200B;图标，以启用字段&#x200B;**Text**。 将&#x200B;**参数名称**&#x200B;更改为`body`。

![AEM Assets Dynamic Media](./images/aemdm38.png)

为&#x200B;**Paris**&#x200B;选择图层。 单击3个点&#x200B;**...**，然后单击&#x200B;**编辑**。

![AEM Assets Dynamic Media](./images/aemdm39.png)

转到&#x200B;**参数**。 启用字段&#x200B;**隐藏**&#x200B;并输入&#x200B;**参数名称**： `city_paris`。 单击&#x200B;**保存**。

![AEM Assets Dynamic Media](./images/aemdm40.png)

为&#x200B;**迪拜**&#x200B;选择图层。 单击3个点&#x200B;**...**，然后单击&#x200B;**编辑**。

![AEM Assets Dynamic Media](./images/aemdm41.png)

转到&#x200B;**参数**。 启用字段&#x200B;**隐藏**&#x200B;并输入&#x200B;**参数名称**： `city_dubai`。 单击&#x200B;**保存**。

![AEM Assets Dynamic Media](./images/aemdm42.png)

为&#x200B;**New York**&#x200B;选择图层。 单击3个点&#x200B;**...**，然后单击&#x200B;**编辑**。

![AEM Assets Dynamic Media](./images/aemdm43.png)

转到&#x200B;**参数**。 启用字段&#x200B;**隐藏**&#x200B;并输入&#x200B;**参数名称**： `city_ny`。 单击&#x200B;**保存**。

![AEM Assets Dynamic Media](./images/aemdm44.png)

单击&#x200B;**预览**。

![AEM Assets Dynamic Media](./images/aemdm45.png)

为&#x200B;**Include all parameters**&#x200B;启用切换器，并按照屏幕快照中的指示更改某些输入变量。 您应该会根据提供的输入动态看到图像更改。 对于字段&#x200B;**city_paris**、**city_dubai**&#x200B;和&#x200B;**city_ny**，值为0表示不隐藏此图像，值为1表示将隐藏此图像。

![AEM Assets Dynamic Media](./images/aemdm46.png)

通过更改某些变量，您现在可以看到另一幅图像正在显示。

![AEM Assets Dynamic Media](./images/aemdm47.png)

通过更改更多变量，您现在可以看到另一幅图像正在显示。

要将此模板与Adobe Journey Optimizer结合使用，并满足此用例的要求，您应该添加另一个层，该层将用于根据Adobe Experience Platform中实时客户档案一部分的字段动态更改需要显示的文件的路径。

在dataprep期间，在Adobe Experience Platform架构中创建了一个字段来存储客户的&#x200B;**最接近的转出城市**。 字段的路径为`--aepTenantId--.individualCharacteristics.fiber_rollout.closest_rollout_city`。

>[!NOTE]
>
>Adobe Experience Platform架构下方的屏幕截图仅供参考。 无需导航到AEP即可自行可视化图表。

![AEM Assets Dynamic Media](./images/aemdm50.png)

在下一个练习中，您将使用该字段动态选择要向哪个客户显示的图像。

要实现此目的，应添加新的图像图层。

首先，我们隐藏包含转出城市图像的其它图层。

![AEM Assets Dynamic Media](./images/aemdm51.png)

接下来，转到&#x200B;**图像**&#x200B;并选择一个城市的随机图像并将其添加到画布中，确保它适合整个画布。 您选择的城市图像并不重要，因为路径将在下一个练习中由AJO动态更改。

![AEM Assets Dynamic Media](./images/aemdm52.png)


![AEM Assets Dynamic Media](./images/aemdm53.png)

转到&#x200B;**参数**。

单击&#x200B;**切换器**&#x200B;图标，以启用字段&#x200B;**隐藏**。 将&#x200B;**参数名称**&#x200B;更改为`dynamic_city_hide`。

单击&#x200B;**切换器**&#x200B;图标，以启用字段&#x200B;**隐藏**。 将&#x200B;**参数名称**&#x200B;更改为`dynamic_city_image`。

单击&#x200B;**保存**。

![AEM Assets Dynamic Media](./images/aemdm54.png)

单击&#x200B;**预览**。

![AEM Assets Dynamic Media](./images/aemdm55.png)

您应该会看到此内容。 启用切换器图标以&#x200B;**包含所有参数**。 更改屏幕快照中指示的某些输入变量。 您应该会根据提供的输入动态看到图像更改。 静态字段&#x200B;**city_paris**、**city_dubai**&#x200B;和&#x200B;**city_ny**&#x200B;应设置为1，这意味着这些图像将被隐藏。

字段&#x200B;**dynamic_city_hide**&#x200B;应设置为0，这意味着该字段将会显示。

字段&#x200B;**dynamic_city_image**&#x200B;现在具有指向巴黎图像的URL，如下所示： `vangeluwCitiSignalDM/citisignal-fiber-max-is-coming_citisignal-paris-1`。

![AEM Assets Dynamic Media](./images/aemdm56.png)

在URL中选择&#x200B;**paris**&#x200B;一词。

![AEM Assets Dynamic Media](./images/aemdm57.png)

将&#x200B;**paris**&#x200B;更改为`newyork`，然后在UI中的其他位置单击以查看纽约市图像的图像更改。

![AEM Assets Dynamic Media](./images/aemdm58.png)

选择单词&#x200B;**new york**&#x200B;并将其更改为`dubai`，然后在UI中的其他位置单击以查看迪拜城市图像的图像更改。

最后，单击&#x200B;**发布**。

![AEM Assets Dynamic Media](./images/aemdm60.png)

您应该会看到此内容。 单击&#x200B;**是**。

![AEM Assets Dynamic Media](./images/aemdm61.png)

您的Dynamic Media模板现已配置并成功发布。 在下一个练习中，您将将该模板与Adobe Journey Optimizer中的电子邮件营销活动结合使用。

## 后续步骤

下一步：[将您的Dynamic Media模板用于Adobe Journey Optimizer](./ex2.md){target="_blank"}

返回[Adobe Experience Manager Assets和Dynamic Media](./aemassetsdm.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
