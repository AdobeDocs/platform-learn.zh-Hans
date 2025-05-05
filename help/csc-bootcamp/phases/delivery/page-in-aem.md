---
title: CSC Bootcamp — 在AEM中创建页面
description: CSC Bootcamp — 在AEM中创建页面
doc-type: multipage-overview
exl-id: 22587f83-135e-4e88-b51b-a90a4509a90f
source-git-commit: 143da6340b932563a3309bb46c1c7091e0ab2ee2
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 0%

---

# 在AEM中创建页面

AEM为您提供两个环境：创作环境和Publish环境。 通过这些交互可以将内容放到您的网站上，以便您的访客能够体验这些内容。

创作环境提供了用于在实际发布此内容之前创建、更新和审核此内容的机制：

- 作者创建和审查内容（可以是多种类型；例如，页面、资产、出版物等）
- 这些将在某一时刻发布到您的网站。

作为作者，您需要在AEM中整理您的网站。 其中涉及创建和命名内容页面，以便：

- 您可以轻松地在创作环境中找到它们
- 您网站的访客可以轻松地在发布环境中浏览这些页面

网站的结构可被视为保存内容页面的树结构。 这些内容页面的名称用于组成URL，而标题在查看页面内容时显示。 在以下示例中，页面的可访问URL将为/content/adobike/language-masters/en.html

![页面结构](./images/delivery-web-structure.png)

我们来看看如何向现有网站中添加一些新页面，以及如何重用某些内容。

## 创建主页

如上一节中所述，AEM页面层次结构采用树形结构的形式。 这意味着我们将从最高级别的页面开始：主页。

- 转到[https://author-p71057-e991028.adobeaemcloud.com/](https://author-p71057-e991028.adobeaemcloud.com/)上的AEM作者，然后使用我们提供的凭据登录。

- 从AEM的“开始”菜单中，选择导航\>站点

![选择站点图标](./images/delivery-web-aem-sites.png)

- 首先，我们将现有树结构导航到要创建主页的位置。 通过依次选择第一列中的“Adobike”和第二列中的“Bootcamp”来导航树结构。 然后，要在此页面下创建页面，请单击“创建”按钮，然后在弹出的菜单中选择“页面”。

![查找回引导营内容](./images/delivery-web-create-page.png)

- 这将打开一个用于配置我们的新页面的新屏幕。 首先，我们可以选择一个页面模板。 利用AEM中的页面模板，可定义页面的结构，并定义可在此页面上使用的内容。 由于我们要创建主页（一个登陆页面），因此我们将选择登陆页面模板，然后单击“下一步”按钮以继续。

![选择正确的模板](./images/delivery-web-create-page-template.png)

- 在下一个屏幕中，您将能够使用一些初始信息填充页面。 最重要的信息是标题（必填属性，以\*指示），该属性旨在为您页面提供一个有意义的名称。 如果您未填写“名称”，AEM将按照SEO最佳实践自动生成您的页面可用的URL。 在这种情况下，您可以将此字段留空。 也可以填写其他某些属性，您可以浏览其他选项卡，但出于此引导营的目的，暂不填写任何其他属性。 准备好创建页面时，只需单击“创建”按钮。

![填写属性](./images/delivery-web-create-page-properties.png)

- AEM现在将创建您的页面。 完成后，您将看到一个弹出窗口，允许您通过单击“打开”按钮打开新创建的页面。

![打开新创建的页面](./images/delivery-web-create-page-success.png)

- 您现在将到达AEM编辑器。 这是一个“所见即所得”（或WYSIWYG）编辑器，您可以在其中将组件拖放到页面中以构建页面。 让我们看一下导航：
  ![aem的wysiwig编辑器](./images/delivery-web-page-editor-home.png)
   - 在左侧，有一个侧面板，其中包含可在页面上使用的资产、可在此页面上使用的组件（或构建块），以及一个方便使用的树视图，该视图向您展示页面的结构方式。 单击任意这些图标以打开其视图。
   - 在右侧，您会看到“布局容器”。 您可以在此处放置所需组件。
   - 让我们使用一些内容填充页面。 您可以随意填充主页。 在以下示例中，我们使用了链接到产品页面的图像组件，以及两个Teaser组件。

![主页](./images/delivery-web-homepage.png)

## 利用体验片段重用体验

我们现在已创作主页，该页面已完全准备好我们的Adobike启动。 但是，其中的某些内容（例如我们的自行车的独特卖点）可以在多个页面上重复使用。

理想情况下，我们希望仅创建一次此独特的销售点体验，以便我们可以集中管理它并确保个性化但一致的体验。 在AEM中，我们可以对“体验片段”执行此操作。 体验片段是由一个或多个组件组成的组，其中包括可在页面中引用的内容和布局。 它们可以包含任何组件。

让我们立即使用它：

- 转到[https://author-p71057-e991028.adobeaemcloud.com/](https://author-p71057-e991028.adobeaemcloud.com/)上的AEM作者，然后使用我们提供的凭据登录。

- 从AEM的“开始”菜单中，选择导航\>体验片段

![选择XF图标](./images/delivery-web-xf.png)

- 在以下屏幕中，让我们创建一个文件夹，您的团队可以使用它存储可重复使用的体验。 在列视图中，导航到Adobike \> Bootcamp ，然后单击“创建\>文件夹”按钮。

![创建文件夹](./images/delivery-web-create-xf-folder.png)

- 在弹出的模式窗口中，为您的文件夹提供团队的名称。 您可以将name字段留空，AEM将自动为您生成它。 为文件夹命名后，单击“创建”按钮以创建文件夹。

![为其命名](./images/delivery-web-create-xf-folder-name.png)

- 此时您应该会看到文件夹弹出窗口。 单击它，然后单击创建\>体验片段按钮。

![创建一个xf](./images/delivery-web-create-xf.png)

- 首先，让我们选择一个体验片段模板。 与页面一样，体验片段可以基于多个模板，每个模板都预见预定义的体验。 在本例中，由于我们想要在我们的网站中重复使用内容，因此让我们通过选中左上角的复选框，然后单击“下一步”按钮来选择“体验片段Web变体模板”。

![选择xf模板](./images/delivery-web-create-xf-template.png)

- 为您的体验片段提供一个有意义的标题，例如“Adobike USPs”，然后单击创建按钮。

![给xf一个标题](./images/create-xf-properties.png)

- 创建体验片段后，单击模式窗口中的“打开”按钮，以便我们可以在体验片段中添加一些内容。

![单击“打开”](./images/delivery-web-create-xf-success.png)

- 就像在编辑页面时一样，您可以看到一个布局容器，您可以在其中添加一些内容。

![xf编辑器](./images/delivery-web-xf-editor.png)

- 我们将从主页复制组件。 在新选项卡中，导航到主页（如上一章所述），选择要复制的组件，然后单击复制图标。

![复制组件](./images/delivery-web-copy-from-home.png)

- 然后，返回您的体验片段，单击布局容器并单击粘贴按钮。

![粘贴组件](./images/delivery-web-paste-to-xf.png)

>[!NOTE]
>
> 提示：AEM允许您在任何页面或体验片段中使用“布局模式”。 这允许您调整组件大小并优化任何设备的体验。

- 从顶部菜单中，打开下拉菜单并选择“布局”以进入布局模式。

![更改为布局模式](./images/delivery-web-layout-mode.png)

- 然后，您可以选择任何组件并调整其大小，只需拖动组件两侧的手柄以与屏幕上显示的列对齐。

![根据需要调整组件大小](./images/delivery-web-layout-resize.png)

- 默认情况下，您正在编辑所有断点。 但是，如果要编辑特定断点，可以从页面顶部的工具栏中选择匹配的设备。 随后将突出显示您随后要为其创作断点。

![选择断点](./images/delivery-web-bp-before.png)

- 如您所见，移动设备上的双列布局看起来并不太好。 让我们在移动设备上创建一个单列布局。 正如您在桌面上看到的，我们的体验保持不变，但在移动设备上，我们现在只用一列内容提供了更好的体验。

![针对移动设备进行优化](./images/delivery-web-bp-after.png)

- 最后，我们现在可以在主页上重复使用此体验。 将“体验片段”组件拖放到页面上您希望我们的内容显示的位置。 您可以删除我们复制的内容，因为我们将从体验片段中使用该内容。

![拖放xf组件](./images/delivery-web-xf-on-home.png)

- 打开体验片段组件的配置对话框，然后使用路径选择器选择您创建体验片段的位置。

![单击文件夹图标](./images/delivery-web-xf-dialog.png)

![选择正确的XF](./images/delivery-web-select-xf.png)

- 最后，我们的页面上提供了可重复使用的体验。

![更新的主页](./images/delivery-web-xf-result.png)

## 创建产品页面

使用与AEM集成的Adobe Commerce时，您可以获得通用的产品详细信息页面，当您从生成的概述导航站点时将使用该页面。 但是，有时我们也希望看到一个将产品特定内容和启发内容结合在一起的启发页面。 让我们复制自己预制的商店，然后创建一个富有启迪的产品页面。

- 转到[https://author-p71057-e991028.adobeaemcloud.com/](https://author-p71057-e991028.adobeaemcloud.com/)上的AEM作者，然后使用我们提供的凭据登录。

- 从AEM的“开始”菜单中，选择导航\>站点

![选择站点图标](./images/delivery-web-aem-sites.png)

- 在列概述中，将预制的网站导航到商店： Adobike \>语言母版\> Adobike \>商店。 然后，选中带有复选框的商店页面并单击“创建\> Live Copy”。 在不涉及太多具体内容的情况下，这将创建一个可在站点中使用的页面副本，以便您能够使用AEM的多站点管理器重复使用现有页面和内容。

![创建Live Copy](./images/delivery-web-create-lc.png)

- 在弹出的屏幕中，选中团队名称旁边的复选框以将其站点作为目标。 然后，单击下一步按钮。

![选择目标](./images/delivery-web-lc-destination.png)

- 由于我们不会深入了解多站点管理器，因此您可以接管此配置。\
  Title： Shop\
  名称：shop\
  转出配置：标准转出配置\
  配置Live Copy后，单击“创建”按钮。

![配置Live Copy](./images/delivery-web-lc-config.png)

>[!NOTE]
>
> 想进一步了解实时副本吗？ 签出[“正在创建和同步活动副本”。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/msm/creating-live-copies.html?lang=zh-Hans)

- 完成后，您现在应该会在您的网站上看到该商店。 选择它，然后单击创建\>页面，以创建我们富有启迪的产品页面。

![创建产品页](./images/delivery-web-create-pdp.png)

- 由于我们要在页面上显示产品信息，因此现在让我们使用产品页面模板创建一个页面。 选择它，然后单击下一步按钮。

![使用产品页面模板](./images/delivery-web-create-pdp-template.png)

- 填写页面元数据，然后单击创建按钮，操作与主页类似。 创建页面后，您可以通过单击打开按钮来打开该页面。 如您所见，该页面已填充了产品详细信息组件。

![完成配置](./images/delivery-web-pdp-initial.png)

- 首先，我们将添加之前创建的体验片段。 然后，我们可以在页面上添加任何我们仍想要的其他内容。 最后，我们将配置产品详细信息组件，以显示Adobike产品，方法是：在配置对话框中选择产品查找器，然后选择我们的Adobike类别并选中产品旁边的复选框。 然后，单击添加按钮。

![选择产品查找器](./images/delivery-web-configure-product.png)

![选择产品](./images/delivery-web-select-product.png)

- 现在，我们有了完整的鼓舞人心的页面，包括来自Adobe Commerce的集中管理的内容和产品信息。

![产品页](./images/delivery-web-pdp-result.png)

下一步：[第3阶段 — 投放：Campaign GO/NO-GO](./go-nogo.md)

[返回第3阶段 — 交付：验证移动应用程序](./app.md)

[返回所有模块](../../overview.md)
