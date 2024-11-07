---
title: Adobe Journey Optimizer — 在Adobe Journey Optimizer中配置和使用短信渠道
description: Adobe Journey Optimizer — 在Adobe Journey Optimizer中配置和使用短信渠道
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '2300'
ht-degree: 3%

---

# 3.2.4创建历程和消息

在本练习中，您将使用Adobe Journey Optimizer创建一个历程和若干短信。

对于此用例，目标是根据客户所在位置的天气条件发送不同的SMS消息。 已定义三种方案：

- 摄氏10度以下
- 在10°和25°C之间
- 温度高于25摄氏度

对于这3种情况，您需要在Adobe Journey Optimizer中定义3条短信消息。

## 3.2.4.1创建历程

通过转到[Adobe Experience Cloud](https://experience.adobe.com)登录Adobe Journey Optimizer。 单击&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

您将被重定向到Journey Optimizer中的&#x200B;**主页**&#x200B;视图。 首先，确保使用正确的沙盒。 要使用的沙盒名为`--aepSandboxName--`。 若要从一个沙盒更改到另一个沙盒，请单击&#x200B;**PRODUCTION Prod (VA7)**，然后从列表中选择该沙盒。 在此示例中，沙盒名为&#x200B;**AEP Enablement FY22**。 然后，您将进入沙盒`--aepSandboxName--`的&#x200B;**主页**&#x200B;视图。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)


在左侧菜单中，转到&#x200B;**历程**，然后单击&#x200B;**创建历程**&#x200B;以开始创建您的历程。

![演示](./images/jocreate.png)

您应该为您的历程命名。

作为历程的名称，请使用`--aepUserLdap-- - Geofence Entry Journey`。 在此示例中，历程名称为`vangeluw - Geofence Entry Journey`。 此时不得设置其他值。 单击&#x200B;**确定**。

![演示](./images/joname.png)

在屏幕左侧，查看&#x200B;**事件**。 您应会在该列表中看到之前创建的事件。 选择它，然后将其拖放到历程画布上。 您的历程随后将类似于此。 单击&#x200B;**确定**。

![演示](./images/joevents.png)

接下来，单击&#x200B;**业务流程**。 您现在可以看到可用的&#x200B;**编排**&#x200B;功能。 选择&#x200B;**条件**，然后将其拖放到历程画布上。

![演示](./images/jo2.png)

您现在必须定义三个条件：

- 天气寒冷超过10摄氏度
- 它位于摄氏10度至25度之间
- 天气比25摄氏度还热

让我们定义第一个条件。

### 条件1：摄氏10度以下

单击&#x200B;**条件**。  单击&#x200B;**Path1**&#x200B;并编辑&#x200B;**比10 C**&#x200B;冷的路径的名称。 单击Path1表达式的&#x200B;**编辑**&#x200B;图标。

![演示](./images/jo5.png)

然后，您会看到空的&#x200B;**简单编辑器**&#x200B;屏幕。 您的查询将更高级，因此您将需要&#x200B;**高级模式**。 单击&#x200B;**高级模式**。

![演示](./images/jo7.png)

随后您将看到允许输入代码的&#x200B;**高级编辑器**。

![演示](./images/jo9.png)

选择以下代码并将其粘贴到&#x200B;**高级编辑器**&#x200B;中。

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 10`

你会看到这个。

![演示](./images/jo10.png)

为了在此条件下检索温度，您需要提供客户当前所在的城市。
**City**&#x200B;需要链接到动态参数`q`，就像我们之前在开放天气API文档中看到的一样。

单击屏幕快照中显示的字段&#x200B;**动态值： q**。

![演示](./images/jo11.png)

然后，您需要在一个可用数据源中找到包含客户当前城市的字段。

![演示](./images/jo12.png)

您可以通过导航到`--aepUserLdap--GeofenceEntry.placeContext.geo.city`找到该字段。

通过单击该字段，将其添加为参数`q`的动态值。 例如，将由您在移动应用程序中实施的地理位置服务填充此字段。 在我们的示例中，我们将使用演示网站的Admin Console来模拟此过程。 单击&#x200B;**确定**。

![演示](./images/jo13.png)

### 条件2：在摄氏10至25度之间

添加第一个条件后，您将看到此屏幕。 单击&#x200B;**添加路径**。

![演示](./images/joc2.png)

双击&#x200B;**Path1**&#x200B;并编辑&#x200B;**介于10和25 C**&#x200B;之间的路径名。 单击此路径中表达式的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joc6.png)

然后，您会看到空的&#x200B;**简单编辑器**&#x200B;屏幕。 您的查询将更高级，因此您将需要&#x200B;**高级模式**。 单击&#x200B;**高级模式**。

![演示](./images/jo7.png)

随后您将看到允许输入代码的&#x200B;**高级编辑器**。

![演示](./images/jo9.png)

选择以下代码并将其粘贴到&#x200B;**高级编辑器**&#x200B;中。

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 10 and #{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 25`

你会看到这个。

![演示](./images/joc10.png)

为了在此条件下检索温度，您需要提供客户当前所在的城市。
**City**&#x200B;需要链接到动态参数&#x200B;**q**，就像我们之前在开放天气API文档中看到的一样。

单击屏幕快照中显示的字段&#x200B;**动态值： q**。

![演示](./images/joc11.png)

然后，您需要在一个可用数据源中找到包含客户当前城市的字段。

![演示](./images/jo12.png)

您可以通过导航到`--aepUserLdap--GeofenceEntry.placeContext.geo.city`找到该字段。 通过单击该字段，将其添加为参数&#x200B;**q**&#x200B;的动态值。 例如，将由您在移动应用程序中实施的地理位置服务填充此字段。 在我们的示例中，我们将使用演示网站的Admin Console来模拟此过程。 单击&#x200B;**确定**。

![演示](./images/jo13.png)

接下来，您将添加第三个条件。

### 条件3：温度高于25°C

添加第二个条件后，您将看到此屏幕。 单击&#x200B;**添加路径**。

![演示](./images/joct2.png)

双击Path1以将名称更改为&#x200B;**比25 C**热。
然后，单击此路径中表达式的**编辑**&#x200B;图标。

![演示](./images/joct6.png)

然后，您会看到空的&#x200B;**简单编辑器**&#x200B;屏幕。 您的查询将更高级，因此您将需要&#x200B;**高级模式**。 单击&#x200B;**高级模式**。

![演示](./images/jo7.png)

随后您将看到允许输入代码的&#x200B;**高级编辑器**。

![演示](./images/jo9.png)

选择以下代码并将其粘贴到&#x200B;**高级编辑器**&#x200B;中。

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 25`

你会看到这个。

![演示](./images/joct10.png)

为了在此条件下检索温度，您需要提供客户当前所在的城市。
**City**&#x200B;需要链接到动态参数&#x200B;**q**，就像我们之前在开放天气API文档中看到的一样。

单击屏幕快照中显示的字段&#x200B;**动态值： q**。

![演示](./images/joct11.png)

然后，您需要在一个可用数据源中找到包含客户当前城市的字段。

![演示](./images/jo12.png)

您可以通过导航到```--aepUserLdap--GeofenceEntry.placeContext.geo.city```找到该字段。 通过单击该字段，将其添加为参数&#x200B;**q**&#x200B;的动态值。 例如，将由您在移动应用程序中实施的地理位置服务填充此字段。 在我们的示例中，我们将使用演示网站的Admin Console来模拟此过程。 单击&#x200B;**确定**。

![演示](./images/jo13.png)

您现在有三个已配置的路径。 单击&#x200B;**确定**。

![演示](./images/jo3path.png)

由于这是一个用于学习的历程，我们现在将配置几个操作来展示营销人员现在必须投放消息的各种选项。

## 3.2.4.2发送以下路径的消息：摄氏10度以下

对于每种温度环境，我们将尝试向客户发送短信。 我们只能在拥有客户可用的手机号码时发送短信，因此我们首先必须验证我们是否拥有该号码。

让我们关注&#x200B;**比10 C**&#x200B;更冷的情况。

![演示](./images/p1steps.png)

让我们获取另一个&#x200B;**Condition**&#x200B;元素，并将其拖动到下面的屏幕快照中。 我们将验证此客户是否有可用的手机号码。

![演示](./images/joa1.png)

由于这只是一个示例，因此我们仅在客户具有可用的手机号码时配置选项。 添加&#x200B;**具有移动设备？**&#x200B;的标签。

单击&#x200B;**Path1**&#x200B;路径的表达式的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joa2.png)

在左侧显示的数据源中，导航到&#x200B;**ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**。 您现在直接从Adobe Experience Platform的实时客户个人资料中读取手机号码。

![演示](./images/joa3.png)

选择字段&#x200B;**数字**，然后将其拖放到条件画布。

选择运算符&#x200B;**不为空**。 单击&#x200B;**确定**。

![演示](./images/joa4.png)

你会看到这个。 再次单击&#x200B;**确定**。

![演示](./images/joa6.png)

您的历程随后将类似于此。 如屏幕快照所示，单击&#x200B;**操作**。

![演示](./images/joa8.png)

选择操作&#x200B;**短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/joa9.png)

将&#x200B;**类别**&#x200B;设置为&#x200B;**营销**&#x200B;并选择允许您发送短信的短信表面。 在这种情况下，要选择的电子邮件表面为&#x200B;**短信**。

![ACOP](./images/journeyactions1.png)

下一步是创建消息。 为此，请单击&#x200B;**编辑内容**。

![ACOP](./images/journeyactions2.png)

您现在可以看到消息仪表板，您可以在其中配置短信的文本。 单击&#x200B;**撰写邮件**&#x200B;区域以创建邮件。

![Journey Optimizer](./images/sms3.png)

输入以下文本： `Brrrr... {{profile.person.name.firstName}}, it's freezing. 20% discount on jackets today!`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4.png)

你会看到这个。 单击左上角的箭头可返回您的历程。

![Journey Optimizer](./images/sms4a.png)

你以后会回到这里的。 单击&#x200B;**确定**。

![Journey Optimizer](./images/sms4b.png)

在左侧菜单中，返回&#x200B;**操作**，选择操作`--aepUserLdap--TextSlack`，然后将其拖放到&#x200B;**消息**&#x200B;操作之后。

![演示](./images/joa18.png)

转到&#x200B;**操作参数**&#x200B;并单击参数`TEXTTOSLACK`的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joa19.png)

在弹出窗口中，单击&#x200B;**高级模式**。

![演示](./images/joa20.png)

选择以下代码，复制该代码并将其粘贴到&#x200B;**高级模式编辑器**&#x200B;中。 单击&#x200B;**确定**。

`"Brrrr..." + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " It's freezing. 20% discount on Jackets today!"`

![演示](./images/joa21.png)

您将看到已完成的操作。 单击&#x200B;**确定**。

![演示](./images/joa22.png)

此历程路径现已准备就绪。

## 3.2.4.3为10°至25°摄氏度的路径发送消息

对于每种温度环境，我们将尝试向客户发送短信。 我们只能在拥有客户可用的手机号码时发送短信，因此我们首先必须验证我们是否拥有该号码。

让我们重点看一下10到25个C **路径之间的**。

![演示](./images/p2steps.png)

让我们获取另一个&#x200B;**Condition**&#x200B;元素，并将其拖动到下面的屏幕快照中。 我们将验证此客户是否有可用的手机号码。

![演示](./images/jop1.png)

由于这只是一个示例，因此我们仅在客户具有可用的手机号码时配置选项。 添加&#x200B;**具有移动设备？**&#x200B;的标签。

单击&#x200B;**Path1**&#x200B;路径的表达式的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joa2p2.png)

在左侧显示的数据源中，导航到&#x200B;**ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**。 您现在直接从Adobe Experience Platform的实时客户个人资料中读取手机号码。

![演示](./images/joa3.png)

选择字段&#x200B;**数字**，然后将其拖放到条件画布。

选择运算符&#x200B;**不为空**。 单击&#x200B;**确定**。

![演示](./images/joa4.png)

你会看到这个。 单击&#x200B;**确定**。

![演示](./images/joa6.png)

您的历程随后将类似于此。 如屏幕快照所示，单击&#x200B;**操作**。

![演示](./images/jop8.png)

选择操作&#x200B;**短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/jop9.png)

将&#x200B;**类别**&#x200B;设置为&#x200B;**营销**&#x200B;并选择允许您发送短信的短信表面。 在这种情况下，要选择的电子邮件表面为&#x200B;**短信**。

![ACOP](./images/journeyactions1z.png)

下一步是创建消息。 为此，请单击&#x200B;**编辑内容**。

![ACOP](./images/journeyactions2z.png)

您现在可以看到消息仪表板，您可以在其中配置短信的文本。 单击&#x200B;**撰写邮件**&#x200B;区域以创建邮件。

![Journey Optimizer](./images/sms3a.png)

输入以下文本： `What a nice weather for the time of year, {{profile.person.name.firstName}} - 20% discount on Sweaters today!`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4az.png)

你会看到这个。 单击左上角的箭头可返回您的历程。

![Journey Optimizer](./images/sms4azz.png)

您现在将看到已完成的操作。 单击&#x200B;**确定**。

![演示](./images/jop17.png)

在左侧菜单中，返回&#x200B;**操作**，选择操作`--aepUserLdap--TextSlack`，然后将其拖放到&#x200B;**消息**&#x200B;操作之后。

![演示](./images/jop18.png)

转到&#x200B;**操作参数**&#x200B;并单击参数`TEXTTOSLACK`的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joa19z.png)

在弹出窗口中，单击&#x200B;**高级模式**。

![演示](./images/joa20.png)

选择以下代码，复制该代码并将其粘贴到&#x200B;**高级模式编辑器**&#x200B;中。 单击&#x200B;**确定**。

`"What nice weather for the time of year, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " 20% discount on Sweaters today!"`

![演示](./images/jop21.png)

您将看到已完成的操作。 单击&#x200B;**确定**。

![演示](./images/jop22.png)

此历程路径现已准备就绪。

## 3.2.4.4发送以下路径的消息：温度超过25° Celsius

对于每种温度环境，我们将尝试向客户发送短信。 我们只能在拥有客户可用的手机号码时发送短信，因此我们首先必须验证我们是否拥有该号码。

让我们重点关注&#x200B;**比25 C**&#x200B;路径更温暖。

![演示](./images/p3steps.png)

让我们获取另一个&#x200B;**Condition**&#x200B;元素，并将其拖动到下面的屏幕快照中。 您将验证是否为此客户提供了可用手机号码。

![演示](./images/jod1.png)

由于这只是一个示例，因此我们仅在客户具有可用的手机号码时配置选项。 添加&#x200B;**具有移动设备？**&#x200B;的标签。

单击&#x200B;**Path1**&#x200B;路径的表达式的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joa2p3.png)

在左侧显示的数据源中，导航到&#x200B;**ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**。 您现在直接从Adobe Experience Platform的实时客户个人资料中读取手机号码。

![演示](./images/joa3.png)

选择字段&#x200B;**数字**，然后将其拖放到条件画布。

选择运算符&#x200B;**不为空**。 单击&#x200B;**确定**。

![演示](./images/joa4.png)

你会看到这个。 单击&#x200B;**确定**。

![演示](./images/joa6.png)

您的历程随后将类似于此。 如屏幕快照所示，单击&#x200B;**操作**。

![演示](./images/jod8.png)

选择操作&#x200B;**短信**，然后将其拖放到刚刚添加的条件之后。

![演示](./images/jod9.png)

将&#x200B;**类别**&#x200B;设置为&#x200B;**营销**&#x200B;并选择允许您发送短信的短信表面。 在这种情况下，要选择的电子邮件表面为&#x200B;**短信**。

![ACOP](./images/journeyactions1zy.png)

下一步是创建消息。 为此，请单击&#x200B;**编辑内容**。

![ACOP](./images/journeyactions2zy.png)

您现在可以看到消息仪表板，您可以在其中配置短信的文本。 单击&#x200B;**撰写邮件**&#x200B;区域以创建邮件。

![Journey Optimizer](./images/sms3ab.png)

输入以下文本： `So warm, {{profile.person.name.firstName}}! 20% discount on swimwear today!`。 单击&#x200B;**保存**。

![Journey Optimizer](./images/sms4ab.png)

你会看到这个。 单击左上角的箭头可返回您的历程。

![Journey Optimizer](./images/sms4azzz.png)

您现在将看到已完成的操作。 单击&#x200B;**确定**。

![演示](./images/jod17.png)

在左侧菜单中，返回&#x200B;**操作**，选择操作`--aepUserLdap--TextSlack`，然后将其拖放到&#x200B;**消息**&#x200B;操作之后。

![演示](./images/jod18.png)

转到&#x200B;**操作参数**&#x200B;并单击参数`TEXTTOSLACK`的&#x200B;**编辑**&#x200B;图标。

![演示](./images/joa19zzz.png)

在弹出窗口中，单击&#x200B;**高级模式**。

![演示](./images/joa20.png)

选择以下代码，复制该代码并将其粘贴到&#x200B;**高级模式编辑器**&#x200B;中。 单击&#x200B;**确定**。

`"So warm, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + "! 20% discount on swimwear today!"`

![演示](./images/jod21.png)

您将看到已完成的操作。 单击&#x200B;**确定**。

![演示](./images/jod22.png)

此历程路径现已准备就绪。

## 3.2.4.5 Publish您的历程

您的历程现已完全配置。 单击&#x200B;**Publish**。

![演示](./images/jodone.png)

再次单击&#x200B;**Publish**。

![演示](./images/jopublish1.png)

您的历程现已发布。

![演示](./images/jopublish2.png)

下一步： [3.2.5触发您的历程](./ex5.md)

[返回模块3.2](journey-orchestration-external-weather-api-sms.md)

[返回所有模块](../../../overview.md)
