---
title: 迁移默认页面加载规则
description: 在本练习中，您将了解如何将Adobe Experience Cloud Tags中的默认页面加载规则从Analytics扩展迁移到Web SDK扩展。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16760
exl-id: 783b464e-2974-41a1-9949-ac3ac0c786fc
source-git-commit: 2150ead50fee06b434d996183a959ad5f01dd2a8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 0%

---

# 迁移默认页面加载规则

在本练习中，您将了解如何将Adobe Experience Cloud Tags中的默认页面加载规则从Analytics扩展迁移到Web SDK扩展。

## 概述

让我们往后退一点。 Tags中可能有一个规则，该规则会在每个页面上触发，即设置一个或多个默认变量，然后向Adobe Analytics触发信标或点击的规则。 此规则当前使用Adobe Analytics扩展中的“actions”来执行这些操作。 在将实施迁移到Web SDK时，我们需要能够删除对Analytics扩展的任何引用（如操作），并将其替换为属于Web SDK的操作。 在下面的步骤中，我们将假定您具备上述条件，即您有一个默认页面加载规则，该规则会设置变量并在跟踪信标中将变量发送至Analytics。

## 迁移Set Variables操作

在本练习中，我们将创建一个Web SDK操作，该操作等效于Adobe Analytics扩展中的&#x200B;**Set Variables**&#x200B;操作。

1. 在数据收集UI和您的属性中，通过在左侧导航中选择&#x200B;**[!UICONTROL 规则]**&#x200B;屏幕来转到该屏幕。
1. 选择作为您的&#x200B;**Analytics默认加载规则**&#x200B;的规则。 如果您不知道哪个规则是默认加载规则，请与了解规则及其内含内容的人联系。 同样，我们寻找的规则要在每个页面上运行，设置一些默认变量（例如页面名称），然后将信标发送到Analytics。 我们将对此规则进行更改。 我的网站名为“All Pages - DOM Ready 50”，但你的网站可以命名任何名称。

   ![默认页面加载规则](assets/default-page-load-rule.jpg)

1. 要将当前操作从Analytics扩展迁移到Web SDK扩展，我们需要了解正在设置的变量。 因此，请单击&#x200B;**Adobe Analytics - Set Variables**&#x200B;操作，以便查看正在设置的变量（例如PageName、prop、eVars、event等）。

   ![Adobe Analytics — 设置变量](assets/aa-set-variables.jpg)
   1. 请注意该规则中设置了哪些变量

      ![正在设置的变量](assets/aa-vars-set.jpg)

1. 在页面顶部，将单选按钮更改为&#x200B;**提供JSON**，您将看到所设置变量的代码视图。 此代码视图和UI视图可以互换，当您在一个UI中设置任何内容时，它也会在另一个UI中更新。

   ![AA Set Vars JSON](assets/aa-setvars-json.jpg)

1. 将此数据复制到剪贴板或保存到文件以立即使用，因为在下一步中，您将将该代码粘贴到新的Web SDK操作中。
1. 退出Analytics的“设置变量”操作，以便返回规则。

   >[!IMPORTANT]
   >
   >在此步骤中有多个选项，包括：
   >1. 您只需更改现有操作即可，而无需添加新操作，保存现有操作后，会立即将所有数据剪切到新的Web SDK报表包，使其不再显示在当前Analytics报表包中。
   >1. 您可以创建一个新操作，以通过Web SDK将数据发送到Analytics中，暂时保留Analytics操作。 这样，您就可以将新的Web SDK报表包中的数据与当前的Analytics报表包中的数据进行比较。 **在本教程中，我们将对此执行操作。**&#x200B;请记住，在比较数据时，此方法将导致两次点击，这也会导致额外的服务器调用成本，直到您删除旧的Analytics扩展的操作为止。 显然，您不希望将Analytics扩展的操作永远保留在那里，而是希望保留足够长的时间，以验证数据是否正确流入新的Web SDK扩展的报表包中。

1. 单击&#x200B;**加号按钮**&#x200B;以添加新的Web SDK操作。

   ![添加新操作](assets/add-new-action.jpg)

1. 从“扩展”下拉列表中选择&#x200B;**Adobe Experience Platform Web SDK**。
1. 从“操作类型”下拉列表中选择&#x200B;**更新变量**。
1. 确保右侧面板顶部列出的&#x200B;**数据元素**&#x200B;确实是您新的变量类型数据元素。
1. 在右侧面板中，选择数据对象中的&#x200B;**Analytics**&#x200B;对象
   ![更新变量操作](assets/define-update-variable-action.jpg)
1. 现在，将单选按钮更改为&#x200B;**提供JSON或数据元素**，并将上一步中从“设置变量”复制的代码粘贴到此代码窗口中。 请记住，我们在本教程中展示的只是一些示例。 您正在复制和粘贴自己的变量。

   ![新Web SDK代码粘贴](assets/new-websdk-code-paste.jpg)
这个JSON复制工具是专为简化迁移而设计的，我相信您可以看到它非常简单，不必从旧操作中编写大量注释并将其应用到新操作中。

1. 您可以随时来回切换单选按钮，以查看代码版本（如上所示）或用于查看属性的UI版本中的值。 选择&#x200B;**提供单个属性**&#x200B;单选按钮以查看填充的属性。

   ![Web SDK属性1](assets/websdk-attributes-1.jpg)
   ![Web SDK属性2](assets/websdk-attributes-2.jpg)

1. 如果能够正确设置变量，请单击&#x200B;**保留更改/保存。**

## 迁移Send Beacon操作

在本练习中，我们将创建一个与Analytics“发送信标”操作等效的Web SDK，名为&#x200B;**发送事件**。

1. 返回您刚加入的默认页面规则。
1. 在操作部分中，单击&#x200B;**加号按钮**&#x200B;以添加其他操作。 这将是我们的&#x200B;**发送事件**&#x200B;操作。

   ![添加新操作2](assets/add-new-action-2.jpg)

1. 要配置该操作，请从“扩展”下拉列表中选择&#x200B;**Adobe Experience Platform Web SDK**。
1. 从操作类型中选择&#x200B;**发送事件**。
1. 在右侧面板中，选择&#x200B;**Data**&#x200B;对象旁边的数据元素图标。

   ![配置发送事件](assets/send-event-config.jpg)

1. 选择页面查看数据变量（或您称为新“数据”类型数据元素的任何变量），然后单击&#x200B;**选择**&#x200B;按钮。

   ![选择页面数据元素](assets/select-data-element-variable.jpg)

1. 单击&#x200B;**保留更改/保存**。
1. 您现在应该会在规则中看到所有四个操作（两个旧操作和两个新操作）

   ![所有四个操作](assets/all-four-actions.jpg)

## 我应该删除Analytics扩展的操作吗？

好问题。 答案取决于您是否要在删除旧操作之前验证新操作。 如上所述，如果您像在本教程中选择的那样保留将数据发送入的Analytics和Web SDK操作（发送信标和发送事件），则相同的数据将进入两个报表包(即Analytics扩展中的生产报表包和Web SDK扩展中的新验证报表包)。 这会使您的服务器调用次数翻倍，从而产生相关成本。 但是，这是有多少客户选择这样做，以便他们能够在关闭旧数据之前验证新数据。 在本教程的末尾，我们将进行一个练习，该练习会在您对验证感到满意后显示如何清理旧内容；但是，如果您现在要执行此操作以保存服务器调用并且不用担心验证问题，则可以随意跳至教程的结尾，或者直接将Analytics扩展的操作从规则中删除。
