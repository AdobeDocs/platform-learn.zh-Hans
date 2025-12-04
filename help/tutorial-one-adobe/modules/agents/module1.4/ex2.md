---
title: 在您的网站上实施Brand Concierge
description: 在您的网站上实施Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# 1.4.2在您的网站上实施Brand Concierge

>[!IMPORTANT]
>
>要完成此练习，您需要有权访问有效的AEM Assets CS创作环境和AEM CS/EDS网站。
>
>如果没有此类环境，请转到[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照上面的说明进行操作，您将有权访问此类环境。

>[!IMPORTANT]
>
>如果您之前已使用AEM CS环境配置了AEM Assets CS项目，则可能是您的AEM CS沙盒已休眠。 鉴于解除此类沙盒的休眠需要10-15分钟，最好现在就启动解除休眠过程，这样以后就不必等待它。

## 1.4.2.1配置您的网站以显示Brand Concierge - AEM Author

为了让Brand Concierge显示在您的网站上，您需要创建一个新的自定义块，该块需要添加到新页面中，您需要确保将新页面添加到网站的导航中。

现在，您需要按此顺序配置以下项目：

- 创建用于在您的网站上加载Brand Concierge的新自定义块。
- 在您的网站上为Brand Concierge创建新页面。
- 在新创建的Brand Concierge页面上链接新创建的自定义块。
- 在网站的导航标头文件中添加引用，以导航到新创建的Brand Concierge页面。

### 创建新的自定义块

要创建新的自定义块，请导航到链接到您网站的GitHub存储库。

![块](./images/block1.png)

#### component-definition.json

向下滚动，直到看到文件&#x200B;**component-definition.json**&#x200B;并将其打开

![块](./images/block8.png)

单击&#x200B;**pencl**&#x200B;图标以开始编辑文件。

![块](./images/block8a.png)

向下滚动直到看到&#x200B;**块**&#x200B;为止。 将光标设置在组件&#x200B;**卡片**&#x200B;的右括号下

![块](./images/block9.png)

粘贴此代码并在代码块后面输入逗号&#x200B;**，**：

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

单击&#x200B;**提交更改……**。

![块](./images/block10.png)

单击&#x200B;**提交更改**。

![块](./images/block10a.png)

#### component-models.json

向下滚动直到看到文件&#x200B;**component-models.json**&#x200B;为止，然后单击&#x200B;**铅笔**&#x200B;图标以开始编辑该文件。

![块](./images/block11.png)

向下滚动，直到看到最后一个项目。 将光标设置在最后一个组件的右括号旁边。

![块](./images/block12.png)

输入逗号&#x200B;**，**，然后按回车键，并在下一行粘贴此代码：

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

单击&#x200B;**提交更改……**。

![块](./images/block13.png)

单击&#x200B;**提交更改**。

![块](./images/block13a.png)

#### component-filters.json

向下滚动直到看到文件&#x200B;**component-filters.json**&#x200B;为止，然后单击&#x200B;**铅笔**&#x200B;图标以开始编辑该文件。

![块](./images/block14.png)

您应该会看到此内容。

![块](./images/block14a.png)

在&#x200B;**部分**&#x200B;下，输入逗号`,`并将组件`"brandconcierge"`的ID粘贴到当前最后一行之后。

单击&#x200B;**提交更改……**。

![块](./images/block15.png)

单击&#x200B;**提交更改**。

![块](./images/block15a.png)

#### brandconcierge.css

创建块时，最佳做法是为块的样式创建文件，并且该文件应与块具有相同的名称。 您现在应创建该文件，我们现在将保留为空。

转到&#x200B;**块**&#x200B;文件夹。 然后，单击&#x200B;**添加文件**&#x200B;并选择&#x200B;**新建文件**。

![块](./images/css1.png)

在文本框中，输入`brandconcierge/brandconcierge.css`。 文件暂时可以保留为空。 单击&#x200B;**提交更改……**。

![块](./images/css2.png)

单击&#x200B;**提交更改**。

![块](./images/css3.png)

#### brandconcierge.js

创建块时，最佳做法是为与块相关的javascript创建一个文件，该文件应与块同名。

单击&#x200B;**添加文件**&#x200B;并选择&#x200B;**新建文件**。

![块](./images/js1.png)

在文本框中，输入`brandconcierge.js`。 文件暂时可以保留为空。 单击&#x200B;**提交更改……**。

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![块](./images/js2.png)

单击&#x200B;**提交更改**。

![块](./images/js3.png)

### 创建新页面并链接新的自定义块

转到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 单击您的&#x200B;**程序**&#x200B;以将其打开。

![AEMCS](./images/aemcs6.png)

接下来，单击&#x200B;**环境**&#x200B;选项卡上的3个点&#x200B;**...**，然后单击&#x200B;**查看详细信息**。

![AEMCS](./images/aemcs9.png)

然后，您将看到环境详细信息。 单击&#x200B;**作者**&#x200B;环境的URL。

>[!NOTE]
>
>您的环境可能处于休眠状态。 如果是这种情况，您需要先解除环境休眠。

![AEMCS](./images/aemcs10.png)

然后，您应该会看到您的AEM创作环境。 转到&#x200B;**站点**。

![AEMCS](./images/block21.png)

转到&#x200B;**花旗信号**。 单击&#x200B;**创建**&#x200B;并选择&#x200B;**页面**。

![AEMCS](./images/block23.png)

选择&#x200B;**页面**&#x200B;并单击&#x200B;**下一步**。

![AEMCS](./images/block24.png)

输入以下值：

- 标题： **Brand Concierge**
- 名称： **brandconcierge**
- 页面标题： **Brand Concierge**

单击&#x200B;**创建**。

![AEMCS](./images/block25.png)

选择&#x200B;**打开**。

![AEMCS](./images/block22.png)

您应该会看到此内容。

![AEMCS](./images/block26.png)

单击空白区域以选择&#x200B;**节**&#x200B;组件。 然后，单击右菜单中的加号&#x200B;**+**&#x200B;图标。

![AEMCS](./images/block27.png)

随后，您应该会在可用块列表中看到自定义块。 单击以将其选中。

![AEMCS](./images/block28.png)

然后，您应该会看到一个空块被添加到此页面。 此块将使用您将在下一步中添加的JavaScript库动态加载。

单击&#x200B;**发布**。

![AEMCS](./images/block29.png)

再次单击&#x200B;**发布**。

![AEMCS](./images/block30.png)

您的新页面现已发布，并且现在可以添加到下一步的导航标题中。

### 更新导航标头文件

在您的AEM Sites概述中，转到&#x200B;**CitiSignal**&#x200B;并选中文件&#x200B;**Header/nav**&#x200B;的复选框。 单击&#x200B;**编辑**。

![AEMCS](./images/nav0.png)

在预览屏幕中选择&#x200B;**文本**&#x200B;字段，然后单击屏幕右侧的&#x200B;**文本**&#x200B;字段对其进行编辑。

![AEMCS](./images/nav0a.png)

在导航菜单中新建一个包含文本`Brand Concierge`的菜单选项。 然后，选择文本&#x200B;**Brand Concierge**&#x200B;并单击&#x200B;**链接**&#x200B;图标。

![AEMCS](./images/nav1.png)

为字段&#x200B;**Path或URL** `/content/CitiSignal/brandconcierge.html`输入此项，为字段`Brand Concierge`Title **输入**。 单击&#x200B;**保存**。

![AEMCS](./images/nav3.png)

然后您应该拥有此项。 单击&#x200B;**完成**。

![AEMCS](./images/nav4.png)

然后您应该拥有此项。 单击&#x200B;**发布**。

![AEMCS](./images/nav4a.png)

再次单击&#x200B;**发布**。

![AEMCS](./images/nav5.png)

您的新页面现已添加到菜单中。

## 1.4.2.2配置您的网站以显示Brand Concierge - GitHub

在使用AEM创作环境更新内容后，您现在需要更新用于网站的GitHub存储库中的一些代码。

### Javascript库

要在运行在AEM CS/EDS上的网站上实施Brand Concierge，需要以下库：

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

将所有3个文件下载到桌面。

![Brand Concierge](./images/aem0.png)

转到AEM CS/EDS网站的GitHub项目。 转到&#x200B;**脚本**。

![Brand Concierge](./images/aem1.png)

单击&#x200B;**添加文件**，然后选择&#x200B;**上传文件**。

![Brand Concierge](./images/aem3.png)

单击&#x200B;**选择您的文件**。

![Brand Concierge](./images/aem3a.png)

从桌面选择所有3个文件&#x200B;**styleConfigurations.js、alloy.js和brandconciergemain.js**，然后单击&#x200B;**打开**。

![Brand Concierge](./images/aem4.png)

单击&#x200B;**提交更改**。

![Brand Concierge](./images/aem5.png)

### 更新head.html

在上一步中，您上传了3个新库。 现在，加载您的网站时需要加载这些库，加载方法是在文件&#x200B;**head.html**&#x200B;中添加对这些文件的引用。

此外，您还需要在&#x200B;**head.html**&#x200B;文件中提供说明，以确保以正确的顺序和正确的方式加载库。

为此，请单击&#x200B;**代码**&#x200B;以转到AEM CS/EDS网站的GitHub项目。

![Brand Concierge](./images/aem6.png)

向下滚动一点。 打开文件&#x200B;**head.html**。

![Brand Concierge](./images/aem7.png)

单击&#x200B;**铅笔**&#x200B;图标编辑此文件。

![Brand Concierge](./images/aem8.png)

您应该会看到此内容。

![Brand Concierge](./images/aem9.png)

向下滚动到第43行并粘贴以下内容：

以下代码中有2个字段需要更新：

>[!IMPORTANT]
>
>- **datastreamId**&#x200B;当前设置为“XXXXX”，需要用您在上一步中创建的数据流的ID替换。
>- **orgId**&#x200B;需要替换为Adobe Experience Cloud实例的IMS组织ID。

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

单击&#x200B;**提交更改……**。

![Brand Concierge](./images/aem10.png)

单击&#x200B;**提交更改**。

![Brand Concierge](./images/aem11.png)

您现在更新了在网站上加载库所需的代码。

![Brand Concierge](./images/aem12.png)

## 1.4.2.3测试您的配置

现在，在将XXX替换为您的GitHub用户帐户（本例中为`main--citisignal-aem-accs--XXX.aem.page`）之后，您可以通过转到`main--citisignal-aem-accs--XXX.aem.live`或`woutervangeluwe`来测试您网站上的更改。

在此示例中，完整URL将变为：
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page`和/或`https://main--citisignal-aem-accs--woutervangeluwe.aem.live`。

可能需要一些时间才能正确显示所有资源，因为它们需要先发布。

您应该会看到此内容。 单击&#x200B;**Brand Concierge**。

![Brand Concierge](./images/aem13.png)

然后，您应该会看到此Brand Concierge，您可以在其中输入提示。

![Brand Concierge](./images/aem14.png)

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}