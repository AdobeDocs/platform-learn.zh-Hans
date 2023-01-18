---
title: Bootcamp - Journey Optimizer创建历程和电子邮件消息
description: Bootcamp - Journey Optimizer创建历程和电子邮件消息
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 4%

---

# 2.3创建历程和电子邮件消息

在本练习中，您将配置用户在演示网站上创建帐户时需要触发的历程。

通过转到Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Journey Optimizer**.

![ACOP](./images/acophome.png)

您将被重定向到 **主页**  查看Journey Optimizer。 首先，确保您使用的是正确的沙盒。 要使用的沙盒称为 `Bootcamp`. 要从一个沙盒更改为另一个沙盒，请单击 **生产** 并从列表中选择沙盒。 在此示例中，沙盒名为 **Bootcamp**. 然后你会在 **主页** 沙盒视图 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1创建历程

在左侧菜单中，单击 **历程**. 接下来，单击 **创建历程** 以创建新历程。

![ACOP](./images/createjourney.png)

然后，您将看到一个空历程屏幕。

![ACOP](./images/journeyempty.png)

在上一个练习中，您创建了一个 **事件**. 你这样命名的 `yourLastNameAccountCreationEvent` 替换 `yourLastName` 姓氏。 这是事件创建的结果：

![ACOP](./images/eventdone.png)

现在，您需要将此事件作为此历程的开始。 为此，您可以转到屏幕左侧，并在事件列表中搜索您的事件。

![ACOP](./images/eventlist.png)

选择您的事件，将其拖放到历程画布上。 您的历程现在如下所示：

![ACOP](./images/journeyevent.png)

作为历程的第二步，您需要添加一个 **等待** 中。 转到屏幕的左侧，转到 **编排** 中找到此内容。 您将使用配置文件属性，并且需要确保将其填充到实时客户配置文件中。

![ACOP](./images/journeywait.png)

你的旅程现在是这样。 您需要在屏幕右侧配置等待时间。 设置为1分钟。 这将为在事件触发后配置文件属性的可用性提供充足的时间。

![ACOP](./images/journeywait1.png)

单击 **确定** 以保存更改。

作为历程的第三步，您需要添加 **电子邮件** 操作。 转到屏幕左侧的 **操作**，选择 **电子邮件** 操作，然后将其拖放到历程中的第二个节点。 你现在看到这个。

![ACOP](./images/journeyactions.png)

设置 **类别** to **营销** 并选择用于发送电子邮件的电子邮件界面。 在这种情况下，要选择的电子邮件界面是 **电子邮件**. 确保对应的复选框 **电子邮件的点击** 和 **电子邮件打开** 都已启用。

![ACOP](./images/journeyactions1.png)

下一步是创建消息。 要实现此目的，请单击 **编辑内容**.

![ACOP](./images/journeyactions2.png)

## 2.3.2创建消息

要创建消息，请单击 **编辑内容**.

![ACOP](./images/journeyactions2.png)

你现在看到这个。

![ACOP](./images/journeyactions3.png)

单击 **主题行** 文本。

![Journey Optimizer](./images/msg5.png)

在文本区域中开始写入 **你好**

![Journey Optimizer](./images/msg6.png)

主题行尚未完成。 接下来，您需要为字段引入个性化令牌 **名字** 存储在 `profile.person.name.firstName`. 在左侧菜单中，向下滚动以查找 **人员** 元素并单击箭头可更深入地查看级别。

![Journey Optimizer](./images/msg7.png)

现在，查找 **全名** 元素并单击箭头可更深入地查看级别。

![Journey Optimizer](./images/msg8.png)

最后，找到 **名字** ，然后单击 **+** 签到旁边。 然后，您将看到文本字段中会显示个性化令牌。

![Journey Optimizer](./images/msg9.png)

接下来，添加文本 **，感谢您注册！**&#x200B;的问题。单击&#x200B;**保存**。

![Journey Optimizer](./images/msg10.png)

然后你会回来。 单击 **Email Designer** 以创建电子邮件的内容。

![Journey Optimizer](./images/msg11.png)

在下一个屏幕中，系统将显示3种提供电子邮件内容的不同方法：

- **从头开始设计**:从空白画布开始，然后使用WYSIWYG编辑器拖放结构和内容组件以直观地构建电子邮件的内容。
- **编码您自己的**:使用HTML对电子邮件模板进行编码，以创建您自己的电子邮件模板
- **导入HTML**:导入现有HTML模板，您将能够对其进行编辑。

单击 **导入HTML**.

![Journey Optimizer](./images/msg12.png)

拖放文件 **mailtemplatebootcamp.html**，您可以下载 [此处](../../assets/html/mailtemplatebootcamp.html.zip). 单击导入。

![Journey Optimizer](./images/msg13.png)

然后，您将看到此默认电子邮件模板：

![Journey Optimizer](./images/msg14.png)

让我们个性化电子邮件。 单击文本旁边的 **你好** ，然后单击 **添加个性化** 图标。

![Journey Optimizer](./images/msg35.png)

接下来，您需要将 **名字** 存储在 `profile.person.name.firstName`. 在菜单中，找到 **人员** 元素，向下展开到 **全名** 元素，然后单击 **+** 图标将名字字段添加到表达式编辑器中。

单击&#x200B;**保存**。

![Journey Optimizer](./images/msg36.png)

现在，您会注意到个性化字段是如何添加到文本的。

![Journey Optimizer](./images/msg37.png)

单击 **保存** 来保存您的消息。

![Journey Optimizer](./images/msg55.png)

通过单击 **箭头** 主题行文本旁边的。

![Journey Optimizer](./images/msg56.png)

您现在已完成创建注册电子邮件。 单击左上角的箭头以返回您的历程。

![Journey Optimizer](./images/msg57.png)

单击 **确定**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3发布历程

您仍需要为历程提供一个名称。 为此，您可以单击 **属性** 图标。

![ACOP](./images/journeyname.png)

然后，您可以在此处输入历程的名称。 请使用 `yourLastName - Account Creation Journey`. 单击 **确定** 以保存更改。

![ACOP](./images/journeyname1.png)

您现在可以通过单击 **发布**.

![ACOP](./images/publishjourney.png)

单击 **发布** 再次。

![ACOP](./images/publish1.png)

然后，您将看到一个绿色确认栏，表示您的历程现已发布。

![ACOP](./images/published.png)

你现在已经完成了这个练习。

下一步： [2.4测试您的历程](./ex4.md)

[返回到用户流量2](./uc2.md)

[返回到所有模块](../../overview.md)