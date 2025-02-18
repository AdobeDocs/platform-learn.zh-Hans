---
title: Adobe Journey Optimizer — 配置基于触发器的历程 — 订单确认
description: 在此部分中，您将配置基于触发器的历程 — 订单确认
kt: 5342
doc-type: tutorial
exl-id: e8cf1274-2a18-4870-b1e3-378e1779fac1
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# 3.4.1配置基于触发器的历程 — 订单确认

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.1.1创建事件

在菜单中，转到&#x200B;**配置**，然后单击&#x200B;**事件**&#x200B;下的&#x200B;**管理**。

![Journey Optimizer](./images/oc30.png)

在&#x200B;**事件**&#x200B;屏幕上，您会看到类似于此内容的视图。 单击&#x200B;**创建事件**。

![Journey Optimizer](./images/oc31.png)

然后，您将看到空的事件配置。

首先，为您的事件提供如下名称： `--aepUserLdap--PurchaseEvent`，然后添加如下描述： `Purchase Event`。

对于&#x200B;**类型**，请选择&#x200B;**单一**。
对于**事件ID类型**，选择&#x200B;**系统生成的**。

![Journey Optimizer](./images/eventidtype.png)

接下来是架构选择。 为本练习准备了一个方案。 请使用架构`Demo System - Event Schema for Website (Global v1.1) v.1`。

选择架构后，您将在&#x200B;**有效负载**&#x200B;部分看到许多字段正在被选择。 单击&#x200B;**编辑/铅笔**&#x200B;图标以向此事件添加其他字段。

![Journey Optimizer](./images/oc36.png)

然后您会看到此弹出窗口。 现在，您需要选中其他复选框才能在触发此事件时访问其他数据。

![Journey Optimizer](./images/oc37.png)

首先，选中行`--aepTenantId--`上的复选框。

![Journey Optimizer](./images/oc38.png)

接下来，向下滚动并选中第`commerce`行上的复选框。

![Journey Optimizer](./images/oc391.png)

接下来，向下滚动并选中第`productListItems`行上的复选框。 单击&#x200B;**确定**。

![Journey Optimizer](./images/oc39.png)

然后，您将看到其他字段已添加到该事件。 单击&#x200B;**保存**。

![Journey Optimizer](./images/oc40.png)

随后将保存您的新事件，您现在将在可用事件列表中看到您的事件。

再次单击您的事件以再次打开&#x200B;**编辑事件**屏幕。
再次将鼠标悬停在**有效负载**&#x200B;字段上可再次查看这3个图标。 单击&#x200B;**查看有效负载**&#x200B;图标。

![Journey Optimizer](./images/oc41.png)

您现在将看到预期有效负载的示例。 您的事件具有独特的编排eventID，您可以通过在该有效负荷中向下滚动直至看到`_experience.campaign.orchestration.eventID`来查找该事件。

![Journey Optimizer](./images/oc42.png)

事件ID是需要发送到Adobe Journey Optimizer以触发您将在下一步中构建的旅程的内容。 记下此eventID，因为您将在后续步骤之一中需要它。
`"eventID": "1c8148a8ab1993537d0ba4e6ac293dd4f2a88d80b2ca7be6293c3b28d4ff5ae6"`

单击&#x200B;**确定**，然后单击&#x200B;**取消**。

您的事件现已配置完毕，可随时使用。

## 3.4.1.2创建历程

在菜单中，转到&#x200B;**历程**&#x200B;并单击&#x200B;**创建历程**。

![Journey Optimizer](./images/oc43.png)

你会看到这个。 为您的历程命名。 使用`--aepUserLdap-- - Order Confirmation journey`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/oc45.png)

首先，您需要添加事件作为历程的起点。 搜索您的事件`--aepUserLdap--PurchaseEvent`并将其拖放到画布上。 单击&#x200B;**保存**。

![Journey Optimizer](./images/oc46.png)

接下来，在&#x200B;**操作**&#x200B;下，搜索&#x200B;**电子邮件**&#x200B;操作并将其添加到画布上。

![Journey Optimizer](./images/oc47.png)

将&#x200B;**类别**&#x200B;设置为&#x200B;**营销**，并选择一个允许您发送电子邮件的电子邮件表面。 在这种情况下，要选择的电子邮件表面为&#x200B;**电子邮件**。 确保同时启用了&#x200B;**电子邮件**&#x200B;和&#x200B;**电子邮件打开次数**&#x200B;的复选框。

![ACOP](./images/journeyactions1.png)

下一步是创建消息。 为此，请单击&#x200B;**编辑内容**。

![ACOP](./images/journeyactions2.png)

您现在可以看到此内容。 单击&#x200B;**主题行**&#x200B;文本字段。

![ACOP](./images/journeyactions3.png)

在文本区域中，开始写入&#x200B;**感谢您的订购，**&#x200B;然后单击&#x200B;**Personalization**&#x200B;图标。

![Journey Optimizer](./images/oc5.png)

主题行尚未完成。 接下来，您需要为存储在`profile.person.name.firstName`下的字段&#x200B;**名字**&#x200B;引入个性化令牌。 在左侧菜单中，向下滚动以查找&#x200B;**人员** > **全名** > **名字**&#x200B;字段，然后单击&#x200B;**+**&#x200B;图标以将个性化令牌添加到主题行中。 单击&#x200B;**保存**。

![Journey Optimizer](./images/oc6.png)

你以后会回到这里的。 单击&#x200B;**编辑电子邮件正文**&#x200B;以创建电子邮件的内容。

![Journey Optimizer](./images/oc7.png)

在下一个屏幕中，单击&#x200B;**从头开始设计**。

![Journey Optimizer](./images/oc8.png)

在左侧菜单中，您将找到可用于定义电子邮件结构（行和列）的结构组件。

将&#x200B;**1:1列**&#x200B;拖放到画布上8次，这样您应该可以：

![Journey Optimizer](./images/oc9.png)

在左侧菜单中，转到&#x200B;**片段**。 将您之前在[练习3.1.2.1](./../ajob2c-1/ex2.md)中创建的标题拖动到画布中的第一个组件上。 将您之前在[练习3.1.2.2](./../ajob2c-1/ex2.md)中创建的页脚拖到画布中的最后一个组件上。

![Journey Optimizer](./images/fragm1.png)

单击左侧菜单中的&#x200B;**+**&#x200B;图标。 转到&#x200B;**Contents**&#x200B;以开始将内容添加到画布上。

![Journey Optimizer](./images/oc10.png)

转到&#x200B;**Contents**&#x200B;并将&#x200B;**Image**&#x200B;组件拖放到第二行。 单击&#x200B;**浏览**。

![Journey Optimizer](./images/oc15.png)

打开文件夹&#x200B;**citi-signal-images**，单击以选择图像&#x200B;**citisignal-preparing.png**，然后单击&#x200B;**选择**。

![Journey Optimizer](./images/oc14.png)

在&#x200B;**样式**&#x200B;下，将宽度更改为&#x200B;**40%**。

![Journey Optimizer](./images/oc14a.png)

接下来，转到&#x200B;**Contents**&#x200B;并将&#x200B;**Text**&#x200B;组件拖放到第三行。

![Journey Optimizer](./images/oc17.png)

选择该组件中的默认文本&#x200B;**请在此处键入您的文本。**&#x200B;并用以下文本替换它：

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

将光标放在文本&#x200B;**您好**&#x200B;旁边，然后单击&#x200B;**添加Personalization**。

![Journey Optimizer](./images/oc19.png)

导航到&#x200B;**人员** > **全名** > **名字**&#x200B;字段，然后单击&#x200B;**+**&#x200B;图标以将个性化令牌添加到主题行中。 单击&#x200B;**保存**。

![Journey Optimizer](./images/oc20.png)

您随后将看到以下内容：

![Journey Optimizer](./images/oc21.png)

接下来，转到&#x200B;**Contents**&#x200B;并将&#x200B;**Text**&#x200B;组件拖放到第四行。

![Journey Optimizer](./images/oc22.png)

选择该组件中的默认文本&#x200B;**请在此处键入您的文本。**&#x200B;并用以下文本替换它：

`Order Information`

将字体大小更改为&#x200B;**26px**&#x200B;并将文本居中在此单元格中。 然后，您将拥有以下权限：

![Journey Optimizer](./images/oc23.png)

接下来，转到&#x200B;**目录**&#x200B;并将&#x200B;**HTML**&#x200B;组件拖放到第五行上。 单击HTML组件，然后单击&#x200B;**显示源代码**。

![Journey Optimizer](./images/oc24.png)

在&#x200B;**编辑HTML**&#x200B;弹出窗口中，粘贴此HTML：

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

单击&#x200B;**保存**。

![Journey Optimizer](./images/oc25.png)

你就能拥有这个了。 单击&#x200B;**保存**&#x200B;以保存进度。

![Journey Optimizer](./images/oc26.png)

转到&#x200B;**目录**&#x200B;并将&#x200B;**HTML**&#x200B;组件拖放到第六行。 单击HTML组件，然后单击&#x200B;**显示源代码**。

![Journey Optimizer](./images/oc57.png)

在&#x200B;**编辑HTML**&#x200B;弹出窗口中，粘贴此HTML：

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

然后，您将拥有以下权限：

![Journey Optimizer](./images/oc58.png)

您现在必须通过对作为触发历程的事件一部分的productListItems对象的引用替换&#x200B;**xxx**。

![Journey Optimizer](./images/oc59.png)

首先，先删除HTML代码中的&#x200B;**xxx**。

![Journey Optimizer](./images/oc60.png)

在左侧菜单中，单击&#x200B;**上下文属性**。 此上下文将传递到历程中的消息。

你会看到这个。 单击&#x200B;**Journey Orchestration**&#x200B;旁边的箭头可更深入地查看。

![Journey Optimizer](./images/oc601.png)

单击&#x200B;**事件**&#x200B;旁边的箭头可更深入地探讨。

![Journey Optimizer](./images/oc62.png)

单击`--aepUserLdap--PurchaseEvent`旁边的箭头可更深入地钻研。

![Journey Optimizer](./images/oc63.png)

单击&#x200B;**productListItems**&#x200B;旁边的箭头可更深入地查看。

![Journey Optimizer](./images/oc64.png)

单击&#x200B;**名称**&#x200B;旁边的&#x200B;**+**&#x200B;图标以将其添加到画布。 你就能拥有这个了。 您现在需要选择&#x200B;**.name**（如下面的屏幕快照所示），然后您应该删除&#x200B;**.name**。

![Journey Optimizer](./images/oc65.png)

你就能拥有这个了。 单击&#x200B;**保存**。

![Journey Optimizer](./images/oc66.png)

您将立即返回Designer电子邮件。 单击&#x200B;**保存**&#x200B;以保存进度。

![Journey Optimizer](./images/oc67.png)

接下来，转到&#x200B;**目录**&#x200B;并将&#x200B;**HTML**&#x200B;组件拖放到第七行。 单击HTML组件，然后单击&#x200B;**显示源代码**。

![Journey Optimizer](./images/oc68.png)

在&#x200B;**编辑HTML**&#x200B;弹出窗口中，粘贴此HTML：

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

此HTML代码中有2个引用&#x200B;**xxx**。 现在，您必须使用对作为触发历程的事件一部分的productListItems对象的引用，来替换每个&#x200B;**xxx**。

![Journey Optimizer](./images/oc69.png)

首先，删除HTML代码中的前&#x200B;**xxx**。

![Journey Optimizer](./images/oc71.png)

在左侧菜单中，单击&#x200B;**上下文属性**。
单击**Journey Orchestration**&#x200B;旁边的箭头可更深入地查看。

![Journey Optimizer](./images/oc72.png)

单击&#x200B;**事件**&#x200B;旁边的箭头可更深入地探讨。

![Journey Optimizer](./images/oc722.png)

单击`--aepUserLdap--PurchaseEvent`旁边的箭头可更深入地钻研。

![Journey Optimizer](./images/oc73.png)

单击&#x200B;**Commerce**&#x200B;旁边的箭头可更深入地查看。

![Journey Optimizer](./images/oc733.png)

单击&#x200B;**顺序**&#x200B;旁边的箭头可更深入地查看。

![Journey Optimizer](./images/oc74.png)

单击&#x200B;**总价**&#x200B;旁边的&#x200B;**+**&#x200B;图标以将其添加到画布中。

![Journey Optimizer](./images/oc75.png)

你就能拥有这个了。 现在删除HTML代码中的第二个&#x200B;**xxx**。

![Journey Optimizer](./images/oc76.png)

再次单击&#x200B;**总价**&#x200B;旁边的&#x200B;**+**图标以将其添加到画布中。
您还可以将**Order**&#x200B;对象中的字段&#x200B;**Currency**添加到画布上，如此处所示。
完成后，单击**保存**&#x200B;以保存更改。

![Journey Optimizer](./images/oc77.png)

然后，您将返回到Designer电子邮件。 再次单击&#x200B;**保存**。

![Journey Optimizer](./images/oc78.png)

单击左上角主题行文本旁边的&#x200B;**箭头**，返回消息仪表板。

![Journey Optimizer](./images/oc79.png)

单击左上角的箭头可返回您的历程。

![Journey Optimizer](./images/oc79a.png)

单击&#x200B;**保存**&#x200B;以关闭您的电子邮件操作。

![Journey Optimizer](./images/oc79b.png)

单击&#x200B;**发布**&#x200B;以发布您的历程。

![Journey Optimizer](./images/oc511.png)

再次单击&#x200B;**发布**。

![Journey Optimizer](./images/oc512.png)

您的历程现已发布。

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5更新您的Adobe Experience Platform数据收集客户端资产

转到[Adobe Experience Platform数据收集](https://experience.adobe.com/launch/)并选择&#x200B;**标记**。

这是您之前看到的Adobe Experience Platform数据收集属性页面。

![属性页](./../../../../modules/delivery-activation/datacollection/dc1.1/images/launch1.png)

在&#x200B;**快速入门**&#x200B;中，演示系统为您创建了两个客户端属性：一个用于网站，另一个用于移动应用程序。 通过在&#x200B;**[!UICONTROL 搜索]**&#x200B;框中搜索`--aepUserLdap--`来查找它们。 单击以打开&#x200B;**Web**&#x200B;属性。

![搜索框](./../../../../modules/delivery-activation/datacollection/dc1.1/images/property6.png)

转到&#x200B;**数据元素**。 搜索并打开数据元素&#x200B;**XDM — 购买**。

![Journey Optimizer](./images/oc91.png)

你会看到这个。 导航到字段&#x200B;**_experience.campaign.orchestration.eventID**，并在此处填写您的eventID。 此处要填写的eventID是您在练习3.4.1.1中创建的eventID。1单击&#x200B;**保存**&#x200B;或&#x200B;**保存到库**。

![Journey Optimizer](./images/oc92.png)

将更改保存在资产中，然后通过更新开发库发布更改。

![Journey Optimizer](./images/oc93.png)

您的更改现已部署并可进行测试。

## 3.4.1.6使用演示网站测试您的订单确认电子邮件

让我们通过在演示网站上购买产品来测试更新的历程。

转到[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登录后，您将看到此内容。 单击网站项目上的3个点&#x200B;**...**，然后单击&#x200B;**运行**&#x200B;以将其打开。

![DSN](./../../datacollection/dc1.1/images/web8.png)

随后您将看到您的演示网站已打开。 选择URL并将其复制到剪贴板。

![DSN](../../../getting-started/gettingstarted/images/web3.png)

打开一个新的无痕浏览器窗口。

![DSN](../../../getting-started/gettingstarted/images/web4.png)

粘贴您在上一步中复制的演示网站的URL。 然后，系统将要求您使用Adobe ID登录。

![DSN](../../../getting-started/gettingstarted/images/web5.png)

选择您的帐户类型并完成登录过程。

![DSN](../../../getting-started/gettingstarted/images/web6.png)

然后，您会看到您的网站已加载到无痕浏览器窗口中。 对于每个练习，您将需要使用新的无痕浏览器窗口来加载演示网站URL。

![DSN](../../../getting-started/gettingstarted/images/web7.png)

请查看配置文件查看器面板和实时客户配置文件，将&#x200B;**Experience Cloud ID**&#x200B;作为当前未知客户的主要标识符。

![演示](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv2.png)

转到“注册/登录”页面。 单击&#x200B;**创建帐户**。

![演示](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

填写您的详细信息，然后单击&#x200B;**注册**，之后您将被重定向到上一页。

![演示](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

将任何产品添加到购物车

![Journey Optimizer](./images/cart1a.png)

转到&#x200B;**购物车**&#x200B;页面。 单击&#x200B;**签出**。

![Journey Optimizer](./images/cart1.png)

接下来，验证这些字段并在必要时填写。 单击&#x200B;**继续**。

![Journey Optimizer](./images/cart2.png)

单击&#x200B;**确认订单**。

![Journey Optimizer](./images/cart2a.png)

您的订单现已确认。

![Journey Optimizer](./images/cart2b.png)

然后，您将在几秒钟内收到订单确认电子邮件。

![Journey Optimizer](./images/oc98.png)

您已完成此练习。

## 后续步骤

转到[3.4.2配置基于批次的新闻稿历程](./ex2.md){target="_blank"}

返回[Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
