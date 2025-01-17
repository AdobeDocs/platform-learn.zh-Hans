---
title: 创建Cloud Manager项目
description: 创建Cloud Manager项目
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 2fe7d2528132301f559f9d51faa9ad128f5d890f
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# 2.1.3设置您的AEM CS环境

## 2.1.3.1设置您的GitHub存储库

转到[https://github.com](https://github.com){target="_blank"}。 单击&#x200B;**登录**。

![AEMCS](./images/aemcssetup1.png)

输入您的凭据。 单击&#x200B;**登录**。

![AEMCS](./images/aemcssetup2.png)

登录后，您将看到您的GitHub功能板。

![AEMCS](./images/aemcssetup3.png)

转到[https://github.com/AdobeDevXSC/citisignal-one](https://github.com/AdobeDevXSC/citisignal-one){target="_blank"}。 你会看到这个。 单击&#x200B;**使用此模板**，然后单击&#x200B;**新建存储库**。

![AEMCS](./images/aemcssetup4.png)

对于&#x200B;**存储库名称**，请使用`citisignal`。 将可见性设置为&#x200B;**私有**。 单击&#x200B;**创建存储库**。

![AEMCS](./images/aemcssetup5.png)

几秒钟后，您将创建存储库。

![AEMCS](./images/aemcssetup6.png)

接下来，转到[https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}。 单击&#x200B;**配置**。

![AEMCS](./images/aemcssetup7.png)

单击您的GitHub帐户。

![AEMCS](./images/aemcssetup8.png)

单击&#x200B;**仅选择存储库**，然后添加刚刚创建的存储库。 接下来，单击&#x200B;**安装**。

![AEMCS](./images/aemcssetup9.png)

然后您会获得此确认。

![AEMCS](./images/aemcssetup10.png)

## 2.1.3.2更新文件fstab.yaml

在您的GitHub存储库中，单击以打开文件`fstab.yaml`。

![AEMCS](./images/aemcssetup11.png)

单击&#x200B;**编辑**&#x200B;图标。

![AEMCS](./images/aemcssetup12.png)

您现在需要更新第4行字段&#x200B;**url**&#x200B;的值。

![AEMCS](./images/aemcssetup13.png)

您需要通过特定AEM CS环境的URL与GitHub存储库的设置替换当前值。

这是URL的当前值： `https://author-p131639-e1282833.adobeaemcloud.com/bin/franklin.delivery/adobedevxsc/citisignal-one/main`。

URL有3个部分需要更新

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX应替换为您的AEM CS创作环境的URL。

应将YYYY替换为您的GitHub用户帐户。

ZZZ应该被替换为您在上一个练习中使用的GitHub存储库的名称。

您可以通过转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}来查找AEM CS创作环境的URL。 单击您的&#x200B;**程序**&#x200B;以将其打开。

![AEMCS](./images/aemcs6.png)

接下来，单击&#x200B;**环境**&#x200B;选项卡上的3个点&#x200B;**...**，然后单击&#x200B;**查看详细信息**。

![AEMCS](./images/aemcs9.png)

然后，您将看到环境详细信息，包括&#x200B;**作者**&#x200B;环境的URL。 复制URL。

![AEMCS](./images/aemcs10.png)

XXX = `author-p148073-e1511503.adobeaemcloud.com`

对于GitHub用户帐户名称，您可以在浏览器的URL中轻松找到它。 在此示例中，用户帐户名称为`woutervangeluwe`。

YYYY = `woutervangeluwe`

![AEMCS](./images/aemcs11.png)

对于GitHub存储库名称，您还可以在GitHub中打开的浏览器窗口中找到它。 在这种情况下，存储库名称为`citisignal`。

ZZZ = `citisignal`

![AEMCS](./images/aemcs12.png)

这3个值组合在一起，导致需要在文件`fstab.yaml`中配置此新URL。

`https://author-p148073-e1511503.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal/main`

单击&#x200B;**提交更改……**。

![AEMCS](./images/aemcs13.png)

单击&#x200B;**提交更改**。

![AEMCS](./images/aemcs14.png)

文件`fstab.yaml`现已更新。

## 2.1.3.3上传CitiSignal资产

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 单击您的&#x200B;**程序**&#x200B;以将其打开。

![AEMCS](./images/aemcs6.png)

接下来，单击创作环境的URL。

![AEMCS](./images/aemcssetup18.png)

单击&#x200B;**使用Adobe**&#x200B;登录。

![AEMCS](./images/aemcssetup19.png)

然后，您将看到创作环境。

![AEMCS](./images/aemcssetup20.png)

您的URL将如下所示：`https://author-p148073-e1511503.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

您现在需要访问AEM的&#x200B;**CRX包管理器**&#x200B;环境。 为此，请从URL中删除`ui#/aem/aem/start.html?appId=aemshell`并将其替换为`crx/packmgr`，这意味着您的URL现在应如下所示：
`https://author-p148073-e1511503.adobeaemcloud.com/crx/packmgr`。
按**Enter**&#x200B;以加载包管理器环境

![AEMCS](./images/aemcssetup22.png)

接下来，单击&#x200B;**上传包**。

![AEMCS](./images/aemcssetup21.png)

单击&#x200B;**浏览**&#x200B;以查找要上载的包。

要上传的包名为&#x200B;**citisignal-assets.zip**，可从此处下载： [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip){target="_blank"}。

![AEMCS](./images/aemcssetup23.png)

选择包并单击&#x200B;**打开**。

![AEMCS](./images/aemcssetup24.png)

接下来，单击&#x200B;**确定**。

![AEMCS](./images/aemcssetup25.png)

随后将上传包。

![AEMCS](./images/aemcssetup26.png)

接下来，在刚刚上传的包上单击&#x200B;**安装**。

![AEMCS](./images/aemcssetup27.png)

单击&#x200B;**安装**。

![AEMCS](./images/aemcssetup28.png)

几分钟后，将安装您的包。

![AEMCS](./images/aemcssetup29.png)

现在可以关闭此窗口。


## 2.1.3.4Publish花旗信号资产

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 单击您的&#x200B;**程序**&#x200B;以将其打开。

![AEMCS](./images/aemcs6.png)

接下来，单击创作环境的URL。

![AEMCS](./images/aemcssetup18.png)

单击&#x200B;**使用Adobe**&#x200B;登录。

![AEMCS](./images/aemcssetup19.png)

然后，您将看到创作环境。 单击&#x200B;**站点**。

![AEMCS](./images/aemcsassets1.png)

单击&#x200B;**文件**。

![AEMCS](./images/aemcsassets2.png)

单击以选择文件夹&#x200B;**CitiSignal**，然后单击&#x200B;**管理发布**。

![AEMCS](./images/aemcsassets3.png)

单击&#x200B;**下一步**。

![AEMCS](./images/aemcsassets4.png)

单击&#x200B;**Publish**。

![AEMCS](./images/aemcsassets5.png)

您的资产现已发布。

## 2.1.3.5创建CitiSignal网站

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 单击您的&#x200B;**程序**&#x200B;以将其打开。

![AEMCS](./images/aemcs6.png)

接下来，单击创作环境的URL。

![AEMCS](./images/aemcssetup18.png)

单击&#x200B;**使用Adobe**&#x200B;登录。

![AEMCS](./images/aemcssetup19.png)

然后，您将看到创作环境。 单击&#x200B;**站点**。

![AEMCS](./images/aemcssetup30.png)

单击&#x200B;**创建**，然后单击&#x200B;**从模板创建站点**。

![AEMCS](./images/aemcssetup31.png)

单击&#x200B;**导入**。

![AEMCS](./images/aemcssetup32.png)

您现在需要为站点导入预配置的模板。 您可以在[此处](./../../../assets/aem/citisignal-edge-delivery-services-template-0.0.4.zip){target="_blank"}下载模板。 将文件保存到桌面。

接下来，选择文件`citisignal-edge-delivery-services-template-0.0.4.zip`并单击&#x200B;**打开**。

![AEMCS](./images/aemcssetup33.png)

你会看到这个。 单击选择您刚刚上传的模板，然后单击&#x200B;**下一步**。

![AEMCS](./images/aemcssetup34.png)

您现在需要填写一些详细信息。

- 网站标题：使用&#x200B;**CitiSignal**
- 站点名称：使用&#x200B;**citisignal-one**
- GitHub URL：复制您之前使用的GitHub存储库的URL

![AEMCS](./images/aemcssetup35.png)

你就能拥有这个了。 单击&#x200B;**创建**。

![AEMCS](./images/aemcssetup36.png)

正在创建您的站点。 这可能需要几分钟的时间。 单击&#x200B;**确定**。

![AEMCS](./images/aemcssetup37.png)

几分钟后刷新屏幕，您随后将看到新创建的CitiSignal网站。

![AEMCS](./images/aemcssetup38.png)

## 2.1.3.6Publish花旗讯号网站

接下来，单击&#x200B;**CitiSignal**&#x200B;前面的复选框。 然后，单击&#x200B;**管理发布**。

![AEMCS](./images/aemcssetup39.png)

单击&#x200B;**下一步**。

![AEMCS](./images/aemcssetup40.png)

单击&#x200B;**包括子设置**。

![AEMCS](./images/aemcssetup41.png)

单击选中&#x200B;**包括子项**&#x200B;复选框，然后单击取消选中其他复选框。 单击&#x200B;**确定**。

![AEMCS](./images/aemcssetup42.png)

单击&#x200B;**Publish**。

![AEMCS](./images/aemcssetup43.png)

然后你将被送回这里。 导航到&#x200B;**CitiSignal** > **us** > **en**。 单击&#x200B;**索引**&#x200B;前面的复选框，然后单击&#x200B;**编辑**。

![AEMCS](./images/aemcssetup44.png)

您的网站随后将在&#x200B;**通用编辑器**&#x200B;中打开。

![AEMCS](./images/aemcssetup45.png)

现在，在将XXX替换为您的GitHub用户帐户（本例中为`woutervangeluwe`）之后，您可以通过转到`main--citisignal--XXX.aem.page/us/en`和/或`main--citisignal--XXX.aem.live/us/en`来访问您的网站。

在此示例中，完整URL将变为：
`https://main--citisignal--woutervangeluwe.aem.page/us/en`和/或`https://main--citisignal--woutervangeluwe.aem.live/us/en`。

可能需要一些时间才能正确显示所有资源，因为它们需要先发布。

您随后将看到以下内容：

![AEMCS](./images/aemcssetup46.png)

几分钟后，资源将全部正确加载。

![AEMCS](./images/aemcssetup47.png)

## 2.1.3.7测试页面性能

转到[https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}。 输入URL并单击&#x200B;**分析**。

![AEMCS](./images/aemcssetup48.png)

然后，您会看到您的网站在移动和桌面可视化图表中均获得了高分：

**移动设备**：

![AEMCS](./images/aemcssetup49.png)

**桌面**：

![AEMCS](./images/aemcssetup50.png)

下一步： [2.1.4配置自定义块](./ex4.md){target="_blank"}

[返回模块2.1](./aemcs.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
