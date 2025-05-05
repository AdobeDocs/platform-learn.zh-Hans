---
title: 将自定义代码迁移到Web SDK
description: 了解如何将自定义代码从Analytics扩展中的s对象迁移到Web SDK。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16761
source-git-commit: 346d4b2965248fb34341ad464f3f126667e3d940
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# 将自定义代码迁移到Web SDK

在本练习中，您将了解如何在Experience Platform标记中将自定义代码从Adobe Analytics扩展迁移到Adobe Experience Platform Web SDK扩展。

## 大免责声明

我确信您不会感到惊讶的是，我会在文档中添加一些这样的内容，以便开始为您说明使用代码的最好/最简单/最有效的方式。 可以编写、编辑和处理代码的方式显然有很多种。 在本练习中，我将为您提供一种方法，让您能够轻松地获取现有规则中的代码，然后复制该代码、添加更改，并使其适用于迁移的规则。 如果您想到了更好的方法去做，这真是太棒了，我不仅欢迎您使用它，而且还欢迎您与我们以及您在Experience League社区中的同行分享它（尤其是在有关此教程的社区帖子中）。 页面下半部分（使用实施插件）也是如此。 我建议你先做一些对你有好感的事。 好，让我们来了解一下细节。

>[!IMPORTANT]
>
>本着最后一段的精神，同样重要的是，建议您在迁移到Web SDK期间抓住这个机会来仔细查看您的代码，看看其中是否有任何代码应该更新甚至删除。 在下面的段落和步骤中，您将看到如何迁移代码，即使轻松地轻轻地将所有这些代码移过来，我还是建议您不要进行春季清理（这么说吧）。

## 迁移什么代码？

在本节中，我们将首先介绍的代码是您在任何Adobe Analytics操作（包括&#x200B;**Set Variable**&#x200B;操作）的“Custom Code”窗口中可能拥有的代码。 换言之，打开一个规则，然后在操作部分中向下查看。 如果具有“Adobe Analytics — 设置变量”操作，请单击以将其打开。

![设置变量代码](assets/set-variables-action.jpg)

然后在右侧向下滚动到底部，您将看到“自定义代码”窗口的“打开编辑器”按钮。 单击以打开。

![打开自定义代码编辑器](assets/open-aa-custom-code-editor.jpg)

如果其中含有代码，则需要迁移该代码，以便能够使用Web SDK执行该代码并将其发送到Adobe Analytics中。
这里的主要想法是，我们将把“s”对象转换为“content”。__adobe.analytics”。

我们只需在首次调用s对象之前添加一些额外的代码即可，以便它可以被Web SDK理解和处理。 我们将新更改的代码添加到的位置位于“Adobe Experience Platform Web SDK — 更新变量”操作的“自定义代码”窗口中。

例如，假设您在自定义代码窗口中具有以下代码块：

```javascript
const products = window.digitalData.products;
const productIndex = event.element.dataset.productIndex;
const product = products[productIndex];
s.products = [
product.cat3Tag,
product.id,
1,
product.price
].join(";");
```

您需要包含的代码如下所示：

```javascript
content.__adobe = content.__adobe || {};
content.__adobe.analytics = content.__adobe.analytics || {};
const s = content.__adobe.analytics;
```

因此，请按照以下步骤迁移自定义代码：

1. 在Adobe Analytics的“设置变量”操作中，将自定义代码复制到窗口中
1. 关闭该代码窗口，然后关闭（取消）操作。
1. 打开Web SDK — 单击以更新变量操作（或者，如果尚未执行此操作，请添加一个）。

   ![打开更新变量操作](assets/open-sdk-update-variable.jpg)

1. 选择右侧窗口顶部的分析对象

   ![选择分析对象](assets/select-analytics-object.jpg)

1. 向下滚动到底部并打开“自定义代码”窗口

   ![打开sdk自定义代码窗口](assets/open-sdk-custom-code.jpg)

1. 将粘贴到您从Analytics自定义代码窗口中获取的代码
1. 现在，将新几行代码放在现有代码的中间，以便它位于s对象第一次提及的上方，如以下示例所示：

![新的s代码](assets/new-s-code.jpg)

现在，您可以在Custom Code窗口中保存代码，并将更改保留在Update Variables操作中。 您还需要保存规则并在工作库中发布新更改。

## 插件呢？

如果您在Adobe Analytics中实施了“appMeasurement”，并使用Experience Platform标记（以前称为“Launch”）中的Analytics扩展，则您可能要使用一个或多个JavaScript“插件”来设置变量或执行其他任务。 如果这些JavaScript函数和调用位于规则内的代码窗口中，则此页面上的上述信息应可帮助您将代码迁移到Web SDK。
但是，更有可能的情况是，插件代码位于Adobe Analytics扩展本身配置的代码窗口中。 要检查您是否有要迁移的插件和其他代码，请转到“数据收集和标记”打开Analytics扩展，打开您的资产，然后单击左侧导航栏中的&#x200B;**扩展**。

1. 选择页面顶部的&#x200B;**Installed**&#x200B;选项卡，然后选择您的Adobe Analytics扩展。
1. 然后在页面右侧，单击&#x200B;**配置**

   ![配置analytics扩展](assets/configure-analytics-extension.jpg)

1. 展开&#x200B;**使用自定义代码配置跟踪器**&#x200B;部分
1. 单击&#x200B;**打开编辑器**

   ![打开主编辑器](assets/aa-extension-custom-code-window.jpg)

此时，您将能够看到其中包含的代码，并且您可能具有JavaScript“插件”，即代码片段，可帮助您获取所需的一些数据并将其分配给自定义维度等。

从真正的Adobe Analytics意义上来说，并非此代码窗口中的所有内容都可以被视为插件。 在决定如何迁移代码时，请务必了解这一点。

### 有关从扩展的主代码窗口迁移代码的建议

同样，并非代码窗口中的所有内容都可以是Adobe Consulting创建的官方插件。 其中有些可能是您编写的代码，无论您是否将该代码称为插件。 我们建议做两个更改。 它们使用新的扩展，并将您的其余代码复制并粘贴到新位置。

**首先**，标记中有一个名为&#x200B;**常用Web SDK插件**&#x200B;的扩展。 此扩展是Adobe Analytics文档中列出的实施插件总列表的子集。 通过将此扩展安装到Tags资产中，您可以安装所包含插件的代码。 然后，要使用这些插件，您可以在创建新&#x200B;**数据元素**&#x200B;时找到它们。 稍后再详细介绍。

**秒**，如果希望在Adobe Analytics中发送事件之前运行代码，则可以在Web SDK扩展的配置中提供一个代码窗口，以便放置所有（或部分）代码。 查找该代码窗口的步骤如下：

1. 假定您已经将Web SDK扩展添加到资产，请导航到&#x200B;**扩展**&#x200B;并选择&#x200B;**已安装**&#x200B;选项卡
1. 选择&#x200B;**Adobe Experience Platform Web SDK扩展**，然后单击右边栏上的&#x200B;**配置**&#x200B;将其打开。

   ![配置Web SDK扩展](assets/configure-websdk-extension.jpg)

1. 向下滚动到&#x200B;**数据收集**&#x200B;部分，然后单击以打开&#x200B;**onBeforeEventSend**&#x200B;的代码窗口。

   ![onBeforeEventSend](assets/on-before-event-send-window.jpg)

您将在此处粘贴任何要在事件从Web SDK发送到Analytics之前运行的代码。 这基本上就是doPlugins函数在您旧的Analytics实施中所执行的操作。

**好消息**&#x200B;是，此代码应在&#x200B;**任何时间**&#x200B;运行，您执行发送事件时，无论是在页面加载时还是在自定义链接中发生这种情况，都应运行此代码，设置您的变量等。

#### 我需要更改代码吗？

好吧，有也没有。 是的，您确实需要更改一些小更改，但不，只要您确实更改了这些小更改，就不需要更改大部分代码：

_&#x200B;**代码更改1：**&#x200B;_
在您选择之后（或之前），将“插件”代码粘贴到Web SDK扩展的代码窗口中，请从代码中&#x200B;**删除**&#x200B;个“doPlugin”行。 您不需要这些代码，因为它们是appMeasurement.js的一部分，而不是Web SDK代码的一部分，因此它们会导致错误。

![删除doPlugins代码行](assets/remove-doplugins.jpg)

_&#x200B;**代码更改2：**&#x200B;_
您需要执行的另一项更改是添加一些代码，以便定义“s”对象，这非常类似于上文讨论的有关规则操作中的代码的内容。 在这种情况下，我们将需要以稍微不同的方式定义代码，添加已在规则操作中定义的“数据”节点，但此处不适用。
此定义应放置在代码窗口的顶部。 需要在中复制的代码(将代码放入Web SDK扩展时)如下所示：

```javascript
content.data.__adobe = content.data.__adobe || {};
content.data.__adobe.analytics = content.data.__adobe.analytics || {};
const s = content.data.__adobe.analytics;
```

_&#x200B;**同时更改代码：**&#x200B;_
下面是上面列出的代码，但我们刚刚讨论了这两个更改：

![已更新代码](assets/update-code.jpg)

### 将主扩展代码迁移到Web SDK的步骤

如上所述，建议包含两个方面：使用新的“常用Web SDK插件”扩展，以及将Analytics扩展配置中的代码复制并粘贴到Web SDK扩展配置中。 请牢记这一点，并注意页面顶部的重要说明以清理代码，以下是较高层级的推荐步骤：

1. 从Analytics扩展的配置代码窗口中复制所有代码，并将其粘贴到Web SDK扩展配置中的onBeforeEventSend窗口中（虽然我们可能正在复制需要删除或更新的ID代码，但我们会在新窗口中对代码进行几轮复制）。
1. 现在在Web SDK扩展中查看您的代码，并查找&#x200B;**常用Web SDK插件**&#x200B;扩展中定义的插件的插件调用或函数定义。 安装插件扩展后，您可以在Web SDK数据元素定义窗口中找到插件列表。 您还可以在该扩展的[文档](https://exchange.adobe.com/apps/ec/108520)中找到它。
1. 对于在新的Web SDK插件扩展中找到的每个插件，请从代码中删除该扩展及其调用，并确保随后通过创建数据元素，然后在相应的规则中调用该数据元素以设置变量等措施来补偿该删除。
1. 接下来，对代码进行传递，以查看是否存在对appMeasurement.js文件中定义的函数的任何调用。 **以上代码更改1**&#x200B;就是一个例子，此时您可以删除doPlugins代码（如果尚未删除）。 对于其他实例，当调用代码中任何位置都未定义的函数时，这种情况最为明显。 您还可以与Adobe客户支持或Experience League社区中的同行确认，确保该代码属于这种情况。
1. 接下来，通过您的代码来更新或删除任何不再适用于您的分析需求的旧代码，如本页顶部所建议的那样。
1. 现在，执行上面列出的&#x200B;**代码更改2**，添加额外的行，以便对s对象的任何引用都不会在代码中导致错误。
1. 最后但肯定不是最重要的，测试，测试，再测试一些。 之后，再次测试。 确保您的代码在Experience Platform调试器以及Adobe Analytics的报表中提供您预期的结果。

>[!NOTE]
>
>关于上述步骤的最后两点想法。
>首先，您可能认为将所有的插件代码都留在其中会比将其删除并使用新的“常用Web SDK插件”扩展更容易。 这是事实，但是通过使用扩展，您可以获得以下优势：使用UI、定义可重用数据元素，以及将来自动接收任何代码更新。 这也许值得做出改变。
>
>其次，谈到“切换”，您现在还可以决定更新所有的自定义代码，以便它完全不引用旧的“s”对象，这类似于上面步骤5的扩展。 当然，这完全可以接受，而且是一个好主意。 此迁移教程只是为了尽量简化自定义代码的迁移，以防您拥有大量自定义代码并且没有资源立即更新所有代码。 由您决定。

在本课程结束时，我们将以我们开始学习的方式讲述，并承认有许多种编写代码的方法，如果您希望以这种方式编写代码，本文档将为您提供一些可遵循的步骤。 主要的一点是，您的代码可以正常运行，并且会得到您期望的结果，因此请随意按照您的方式操作，我是否提到您应该进行测试？
