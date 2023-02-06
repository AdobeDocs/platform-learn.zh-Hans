---
title: Bootcamp — 混合物理和数字 — Journey Optimizer创建历程和推送 — 巴西通知
description: Bootcamp — 混合物理和数字 — Journey Optimizer创建历程和推送 — 巴西通知
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 2%

---

# 3.3 Crie sua jornada e notificação push

Neste exeracticio， você irá配置jornada e a mensagem precisa ser acionada quando alguém inser ir uma sinalização（信标）usando o aplicativo móvel。

Faça login no Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). 团 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **主页** 不，Journey Optimizer。 普里米罗，我的梦想是沙盒的。 没人会沙箱里的 `Bootcamp`. Para alternar de um sandbox para outro， plicaem **生产** 选择沙盒和沙盒。 新样本，没人做沙盒 **Bootcamp**. Você estará na visualização da **主页**  做seu沙盒 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1小日记

没有菜单，小朋友 **历程**. 阿姆·塞吉达，小团 **创建历程** 新约拉达河。

![ACOP](./images/createjourney.png)

那是我的天。

![ACOP](./images/journeyempty.png)

前不行动，从头开始 **事件**. 波凯诺梅乌奥文托 `yourLastNameBeaconEntryEvent` e代替 `yourLastName` 佩洛·苏·索布雷诺姆。 Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

阿戈拉认为，这一切都是乔纳达的事。 Você pode fazer isso indo para o lado esquerdo da e procando pelo seu evento na lista de eventos。

![ACOP](./images/eventlist.png)

选择一个seu evento， arraste e solte o evento na tela de jornada。 《我的日记》。 团 **确定** 萨尔瓦·苏亚斯·阿尔特拉松斯。

![ACOP](./images/journeyevent.png)

科莫·塞贡达·埃塔帕·达·约纳达， você deve adicionar uma ação **推送**. Vá para o lado esquerdo da tela para **操作**，选择ação **推送** arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

不要用lado direito da tela， agora você deve criar sua notifição推。

定义a **类别** 科科 **营销** e selecione uma supfície push que permite envior notificações push. Nesse caso，一个浅薄的人推着选手 **mmeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

团 **编辑内容**.

![ACOP](./images/emptymsg.png)

Em seguida，一个有害的人：

![ACOP](./images/emailmsglist.png)

用上面的话来定义。

坎波德特克斯托团 **标题**.

![Journey Optimizer](./images/msg5.png)

德克斯托，科米切 **奥拉**. 个人化团体。

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o to kom de personalização para o campo **名字** 她是阿尔玛泽纳多 `profile.person.name.firstName`. 无菜单esquerda， selecione **配置文件属性**, para baixo/navegue para encontra o elemento **人员** e plicue na seta para avançum nível até chegar ao campo `profile.person.name.firstName`. 伊科内集团 **+** para adicionar o campo à tela。 团 **保存**.

![Journey Optimizer](./images/msg7.png)

Então， você irá retor nar para esta tela。 个人化团体 **正文**.

![Journey Optimizer](./images/msg11.png)

德克斯托，埃斯克里瓦 `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

阿姆·塞吉达，小团  **上下文属性** 然后 **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

团 **事件**.

![ACOP](./images/jomsg4.png)

Cligue no nome do seu evento， que deve semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

团 **放置上下文**.

![ACOP](./images/jomsg6.png)

团 **POI互动**.

![ACOP](./images/jomsg7.png)

团 **POI详细信息**.

![ACOP](./images/jomsg8.png)

团 **+** 图标号 **POI名称**.
是塞吉达，是塞金特塞拉。 团 **保存**.

![ACOP](./images/jomsg9.png)

我的脑袋很象。 Cligue na seta no canto superesquerdo para retorn a sua jornada。

![ACOP](./images/jomsg11.png)

团 **确定**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada， você deve adicionar uma ação  **sendMessageToScreen** 操作。 Vá para o lado esquerdo da tela para **操作**，选择ação **sendMessageToScreen** arraste e solte a ação no terceiro nó da sua jornada. 她的话，我就是个空话。

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar mensagem no ponto de extremidade usado pela exibição na loja. 阿桑 **sendMessageToScreen** 她想要玛蒂普拉斯·瓦里维斯·塞贾姆·德菲达斯。 Você pode visualizar essas variáveis rolando para baixo até ver **操作参数**.

![ACOP](./images/jomsg16.png)

Agora você precisa definir os valores para cada parâmetro de ação. Siga esta tabela para entender quais alores são equisários e onde.

| 参数 | 值 |
|:-------------:| :---------------:|
| 投放 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 名字 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 沙盒 | `'bootcamp'` |
| 容器ID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Paradefinir是Valores， Clium noícone **编辑**.

![ACOP](./images/jomsg17.png)

Em seguida， selecione **高级模式**.

![ACOP](./images/jomsg18.png)

Em seguida， cole o valor com bas a tabela acima. 团 **确定**.

![ACOP](./images/jomsg19.png)

Repita加强了对para adicionar valores para cada campo的处理。

>[!IMPORTANT]
>
>Para o campo ECID， há uma referncia ao evento`yourLastNameBeaconEntryEvent`. 朗布雷 — 塞替基尔  `yourLastName` 佩洛·苏·索布雷诺姆。

最后，最后一个Semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Ar para cima e clique **确定**.

![ACOP](./images/jomsg21.png)

您仍需要为历程提供一个名称。 为此，您可以单击 **属性** 图标。

![ACOP](./images/journeyname.png)

我的船就是。 使用 `yourLastName - Beacon Entry Journey`. 团 **确定** 萨尔瓦·苏亚斯·阿尔特拉松斯。

![ACOP](./images/journeyname1.png)

我的歌声是公开的 **发布**.

![ACOP](./images/publishjourney.png)

团 **发布** 诺瓦门特。

![ACOP](./images/publish1.png)

Você verá uma barra de confirmmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

我们的生活很愉快。

这是行动。

埃塔帕： [3.4佐田泰斯特](./ex4.md)

[乌萨里奥河3](./uc3.md)

[托多斯 — 莫杜洛斯](../../overview.md)
