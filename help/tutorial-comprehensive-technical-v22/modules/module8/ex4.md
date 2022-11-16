---
title: Adobe Journey Optimizer — 在Adobe Journey Optimizer中配置和使用短信渠道
description: Adobe Journey Optimizer — 在Adobe Journey Optimizer中配置和使用短信渠道
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 1a08f666-4ea3-43bc-ace7-5dc9854b89ad
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 4%

---

# 8.4创建历程和消息

在本练习中，您将使用Adobe Journey Optimizer创建一个历程和多条文本消息。

对于此用例，目标是根据客户位置的天气条件发送不同的短信消息。 已定义3个方案：

- 冷于10°C
- 10°至25°C
- 25°摄氏度

对于这3种情况，您需要在Adobe Journey Optimizer中定义3条短信消息。

## 8.4.1创建历程

通过转到Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 单击 **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

您将被重定向到 **主页**  查看Journey Optimizer。 首先，确保您使用的是正确的沙盒。 要使用的沙盒称为 `--aepSandboxId--`. 要从一个沙盒更改为另一个沙盒，请单击 **生产产品(VA7)** 并从列表中选择沙盒。 在此示例中，沙盒名为 **2022财年AEP启用**. 然后你会在 **主页** 沙盒视图 `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)


在左侧菜单中，转到 **历程** 单击 **创建历程** 以开始创建历程。

![演示](./images/jocreate.png)

您应该首先命名您的历程。

作为历程的名称，请使用 `--demoProfileLdap-- - Geofence Entry Journey`. 在此示例中，历程名称为 `vangeluw - Geofence Entry Journey`. 目前不得设置任何其他值。 单击&#x200B;**确定**。

![演示](./images/joname.png)

在屏幕左侧，查看 **事件**. 您应会在该列表中看到之前创建的事件。 选择它，然后将其拖放到历程画布上。 然后你的旅程就是这样。 单击 **确定**.

![演示](./images/joevents.png)

接下来，单击 **编排**. 您现在可以看到 **编排** 功能。 选择 **条件**，然后将其拖放到历程画布上。

![演示](./images/jo2.png)

您现在必须定义三个条件：

- 气温低于10°C
- 摄氏10°到25°之间
- 温度高于25°C

让我们定义第一个条件。

### 条件1:冷于10°C

单击 **条件**.  单击 **路径1** 和编辑路径的名称 **冷于10摄氏度**. 单击 **编辑** 图标。

![演示](./images/jo5.png)

然后，您会看到一个空的 **简单编辑器** 屏幕。 您的查询将更高级，因此您需要 **高级模式**. 单击 **高级模式**.

![演示](./images/jo7.png)

然后您将看到 **高级编辑器** 允许代码输入。

![演示](./images/jo9.png)

选择以下代码，并将其粘贴到 **高级编辑器**.

`#{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} <= 10`

然后你会看到这个。

![演示](./images/jo10.png)

为了在这种情况下检索温度，您需要提供客户当前所在的城市。
的 **城市** 需要链接到动态参数 `q`，与之前在Open Weather API文档中看到的一样。

单击字段 **动态值：q** 如屏幕截图所示。

![演示](./images/jo11.png)

然后，您需要在其中一个可用数据源中找到包含客户当前所在城市的字段。

![演示](./images/jo12.png)

您可以通过导航到 `--demoProfileLdap--GeofenceEntry.placeContext.geo.city`.

通过单击该字段，将添加为参数的动态值 `q`. 此字段将由填充，例如，您在移动设备应用程序中实施的地理位置服务。 在本例中，我们将使用演示网站的管理控制台来模拟此过程。 单击&#x200B;**确定**。

![演示](./images/jo13.png)

### 条件2:10°至25°C

添加第一个条件后，您将看到此屏幕。 单击 **添加路径**.

![演示](./images/joc2.png)

双击 **路径1** 和编辑 **10到25摄氏度**. 单击 **编辑** 图标。

![演示](./images/joc6.png)

然后，您会看到一个空的 **简单编辑器** 屏幕。 您的查询将更高级，因此您需要 **高级模式**. 单击 **高级模式**.

![演示](./images/jo7.png)

然后您将看到 **高级编辑器** 允许代码输入。

![演示](./images/jo9.png)

选择以下代码，并将其粘贴到 **高级编辑器**.

`#{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} > 10 and #{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} <= 25`

然后你会看到这个。

![演示](./images/joc10.png)

为了在此条件中检索温度，您需要提供客户当前所在的城市。
的 **城市** 需要链接到动态参数 **q**，与之前在Open Weather API文档中看到的一样。

单击字段 **动态值：q** 如屏幕截图所示。

![演示](./images/joc11.png)

然后，您需要在其中一个可用数据源中找到包含客户当前所在城市的字段。

![演示](./images/jo12.png)

您可以通过导航到 `--demoProfileLdap--GeofenceEntry.placeContext.geo.city`. 通过单击该字段，将添加为参数的动态值 **q**. 此字段将由填充，例如，您在移动设备应用程序中实施的地理位置服务。 在本例中，我们将使用演示网站的管理控制台来模拟此过程。 单击&#x200B;**确定**。

![演示](./images/jo13.png)

接下来，您将添加第3个条件。

### 条件3:25°摄氏度

添加第二个条件后，您将看到此屏幕。 单击 **添加路径**.

![演示](./images/joct2.png)

双击路径1将名称更改为 **温度高于25摄氏度**.
然后，单击 **编辑** 图标。

![演示](./images/joct6.png)

然后，您会看到一个空的 **简单编辑器** 屏幕。 您的查询将更高级，因此您需要 **高级模式**. 单击 **高级模式**.

![演示](./images/jo7.png)

然后您将看到 **高级编辑器** 允许代码输入。

![演示](./images/jo9.png)

选择以下代码，并将其粘贴到 **高级编辑器**.

`#{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} > 25`

然后你会看到这个。

![演示](./images/joct10.png)

为了在此条件中检索温度，您需要提供客户当前所在的城市。
的 **城市** 需要链接到动态参数 **q**，与之前在Open Weather API文档中看到的一样。

单击字段 **动态值：q** 如屏幕截图所示。

![演示](./images/joct11.png)

然后，您需要在其中一个可用数据源中找到包含客户当前所在城市的字段。

![演示](./images/jo12.png)

您可以通过导航到 ```--demoProfileLdap--GeofenceEntry.placeContext.geo.city```. 通过单击该字段，将添加为参数的动态值 **q**. 此字段将由填充，例如，您在移动设备应用程序中实施的地理位置服务。 在本例中，我们将使用演示网站的管理控制台来模拟此过程。 单击&#x200B;**确定**。

![演示](./images/jo13.png)

您现在有三个已配置的路径。 单击 **确定**.

![演示](./images/jo3path.png)

由于这是一个用于学习目的的历程，我们现在将配置几个操作，以展示营销人员现在必须投放消息的各种选项。

## 8.4.2发送路径消息：冷于10°C

对于每个温度环境，我们将尝试向客户发送一条短信。 我们只能在客户有手机号码时发送短信，因此我们必须首先确认是否有。

让我们专注于 **冷于10摄氏度**.

![演示](./images/p1steps.png)

我们再来一个 **条件** 元素，并按照以下屏幕截图所示拖动该元素。 我们会核实此客户是否有可用的手机号码。

![演示](./images/joa1.png)

由于这只是一个示例，我们仅在配置客户具有可用手机号码的选项。 添加标签 **有手机吗？**.

单击 **编辑** 图标 **路径1** 路径。

![演示](./images/joa2.png)

在左侧显示的数据源中，导航到 **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**. 您现在直接从Adobe Experience Platform的实时客户资料中读取手机号码。

![演示](./images/joa3.png)

选择字段 **数值**，然后将其拖放到条件画布中。

选择运算符 **不为空**. 单击 **确定**.

![演示](./images/joa4.png)

然后你会看到这个。 单击 **确定** 再次。

![演示](./images/joa6.png)

然后，您的历程将如下所示。 单击 **操作** 如屏幕截图所示。

![演示](./images/joa8.png)

选择操作 **短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/joa9.png)

设置 **类别** to **营销** 并选择一个短信界面，以便您发送短信。 在这种情况下，要选择的电子邮件界面是 **短信**.

![ACOP](./images/journeyactions1.png)

下一步是创建消息。 要实现此目的，请单击 **编辑内容**.

![ACOP](./images/journeyactions2.png)

现在，您会看到消息仪表板，您可以在其中配置短信的文本。 单击 **撰写消息** 区域创建消息。

![Journey Optimizer](./images/sms3.png)

输入以下文本： `Brrrr... {{profile.person.name.firstName}}, it's freezing. 20% discount on jackets today!`. 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4.png)

然后你会看到这个。 单击左上角的箭头以返回您的历程。

![Journey Optimizer](./images/sms4a.png)

然后你会回来。 单击 **确定**.

![Journey Optimizer](./images/sms4b.png)

在左侧菜单中，返回 **操作**，选择操作 `--demoProfileLdap--TextSlack`，然后将其拖放到 **消息** 操作。

![演示](./images/joa18.png)

转到 **操作参数** ，然后单击 **编辑** 图标 `TEXTTOSLACK`.

![演示](./images/joa19.png)

在弹出窗口中，单击 **高级模式**.

![演示](./images/joa20.png)

选择以下代码，复制该代码并将其粘贴到 **高级模式编辑器**. 单击 **确定**.

`"Brrrr..." + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " It's freezing. 20% discount on Jackets today!"`

![演示](./images/joa21.png)

您将看到已完成的操作。 单击 **确定**.

![演示](./images/joa22.png)

历程的此路径现已准备就绪。

## 8.4.3发送路径消息：10°至25°C

对于每个温度环境，我们将尝试向客户发送一条短信。 我们只能在客户有手机号码时发送短信，因此我们必须首先确认是否有。

让我们专注于 **10到25摄氏度** 路径。

![演示](./images/p2steps.png)

我们再来一个 **条件** 元素，并按照以下屏幕截图所示拖动该元素。 我们会核实此客户是否有可用的手机号码。

![演示](./images/jop1.png)

由于这只是一个示例，我们仅在配置客户具有可用手机号码的选项。 添加标签 **有手机吗？**.

单击 **编辑** 图标 **路径1** 路径。

![演示](./images/joa2p2.png)

在左侧显示的数据源中，导航到 **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**. 您现在直接从Adobe Experience Platform的实时客户资料中读取手机号码。

![演示](./images/joa3.png)

选择字段 **数值**，然后将其拖放到条件画布中。

选择运算符 **不为空**. 单击 **确定**.

![演示](./images/joa4.png)

然后你会看到这个。 单击 **确定**.

![演示](./images/joa6.png)

然后，您的历程将如下所示。 单击 **操作** 如屏幕截图所示。

![演示](./images/jop8.png)

选择操作 **短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/jop9.png)

设置 **类别** to **营销** 并选择一个短信界面，以便您发送短信。 在这种情况下，要选择的电子邮件界面是 **短信**.

![ACOP](./images/journeyactions1z.png)

下一步是创建消息。 要实现此目的，请单击 **编辑内容**.

![ACOP](./images/journeyactions2z.png)

现在，您会看到消息仪表板，您可以在其中配置短信的文本。 单击 **撰写消息** 区域创建消息。

![Journey Optimizer](./images/sms3a.png)

输入以下文本： `What a nice weather for the time of year, {{profile.person.name.firstName}} - 20% discount on Sweaters today!`. 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4az.png)

然后你会看到这个。 单击左上角的箭头以返回您的历程。

![Journey Optimizer](./images/sms4azz.png)

您现在将看到已完成的操作。 单击 **确定**.

![演示](./images/jop17.png)

在左侧菜单中，返回 **操作**，选择操作 `--demoProfileLdap--TextSlack`，然后将其拖放到 **消息** 操作。

![演示](./images/jop18.png)

转到 **操作参数** ，然后单击 **编辑** 图标 `TEXTTOSLACK`.

![演示](./images/joa19z.png)

在弹出窗口中，单击 **高级模式**.

![演示](./images/joa20.png)

选择以下代码，复制该代码并将其粘贴到 **高级模式编辑器**. 单击 **确定**.

`"What nice weather for the time of year, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " 20% discount on Sweaters today!"`

![演示](./images/jop21.png)

您将看到已完成的操作。 单击 **确定**.

![演示](./images/jop22.png)

历程的此路径现已准备就绪。

## 8.4.4发送路径消息：25°摄氏度

对于每个温度环境，我们将尝试向客户发送一条短信。 我们只能在客户有手机号码时发送短信，因此我们必须首先确认是否有。

让我们专注于 **温度高于25摄氏度** 路径。

![演示](./images/p3steps.png)

我们再来一个 **条件** 元素，并按照以下屏幕截图所示拖动该元素。 您将验证此客户是否有可用的手机号码。

![演示](./images/jod1.png)

由于这只是一个示例，我们仅在配置客户具有可用手机号码的选项。 添加标签 **有手机吗？**.

单击 **编辑** 图标 **路径1** 路径。

![演示](./images/joa2p3.png)

在左侧显示的数据源中，导航到 **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**. 您现在直接从Adobe Experience Platform的实时客户资料中读取手机号码。

![演示](./images/joa3.png)

选择字段 **数值**，然后将其拖放到条件画布中。

选择运算符 **不为空**. 单击 **确定**.

![演示](./images/joa4.png)

然后你会看到这个。 单击&#x200B;**确定**。

![演示](./images/joa6.png)

然后，您的历程将如下所示。 单击 **操作** 如屏幕截图所示。

![演示](./images/jod8.png)

选择操作 **短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/jod9.png)

设置 **类别** to **营销** 并选择一个短信界面，以便您发送短信。 在这种情况下，要选择的电子邮件界面是 **短信**.

![ACOP](./images/journeyactions1zy.png)

下一步是创建消息。 要实现此目的，请单击 **编辑内容**.

![ACOP](./images/journeyactions2zy.png)

现在，您会看到消息仪表板，您可以在其中配置短信的文本。 单击 **撰写消息** 区域创建消息。

![Journey Optimizer](./images/sms3ab.png)

输入以下文本： `So warm, {{profile.person.name.firstName}}! 20% discount on swimwear today!`. 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4ab.png)

然后你会看到这个。 单击左上角的箭头以返回您的历程。

![Journey Optimizer](./images/sms4azzz.png)

您现在将看到已完成的操作。 单击 **确定**.

![演示](./images/jod17.png)

在左侧菜单中，返回 **操作**，选择操作 `--demoProfileLdap--TextSlack`，然后将其拖放到 **消息** 操作。

![演示](./images/jod18.png)

转到 **操作参数** ，然后单击 **编辑** 图标 `TEXTTOSLACK`.

![演示](./images/joa19zzz.png)

在弹出窗口中，单击 **高级模式**.

![演示](./images/joa20.png)

选择以下代码，复制该代码并将其粘贴到 **高级模式编辑器**. 单击 **确定**.

`"So warm, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + "! 20% discount on swimwear today!"`

![演示](./images/jod21.png)

您将看到已完成的操作。 单击 **确定**.

![演示](./images/jod22.png)

历程的此路径现已准备就绪。

## 8.4.5发布历程

您的历程现已完全配置。 单击 **发布**.

![演示](./images/jodone.png)

单击 **发布** 再次。

![演示](./images/jopublish1.png)

您的历程现已发布。

![演示](./images/jopublish2.png)

下一步： [8.5触发您的历程](./ex5.md)

[返回模块8](journey-orchestration-external-weather-api-sms.md)

[返回到所有模块](../../overview.md)
