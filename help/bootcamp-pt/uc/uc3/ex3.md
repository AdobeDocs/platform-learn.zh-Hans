---
title: Bootcamp — 将物理和数字相结合 — Journey Optimizer创建您的旅程并推送 — Brazilnotification
description: Bootcamp — 将物理和数字相结合 — Journey Optimizer创建您的旅程并推送 — Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# 3.3 Crie sua jornada e notificação push

Neste exercício， voce irá configurar a jornada e a mensagem que ses acionada quando alguém inserir uma sinalização （信标） usando o o aplicativo móvel.

Faca登录无Adobe Journey Optimizer访问[Adobe Experience Cloud](https://experience.adobe.com)。 单击&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **Home** no Journey Optimizer。 Primeiro，验证一下Sandbox Correto。 不要做沙盒来开发用户`Bootcamp`。 Para alternar de um sandbox para outtro，click em **Prod**&#x200B;选择沙盒类型。 Neste示例，**Bootcamp**&#x200B;中没有sandbox。 Voce estará na visualização da **Home**&#x200B;执行seu沙盒`Bootcamp`。

![ACOP](./images/acoptriglp.png)

## 3.3.1城田crie a sua jornada

无菜单à esquerda，请单击em **历程**。 Em seguida，单击em **创建历程** para criar nova jornada。

![ACOP](./images/createjourney.png)

我们来看看吧。

![ACOP](./images/journeyempty.png)

前方没有练习，新录制了&#x200B;**活动**。 将事件`yourLastNameBeaconEntryEvent`替换为`yourLastName` pelo seu sobrenome。 Este foi o resultado da criação do Evento：

![ACOP](./images/eventdone.png)

Agora voce deve consider este evento como o o início desta Jornada. Voce pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

选择seuo evento， arraste e solte o evento na tela de jornada。 苏亚·乔纳达·阿古拉·德韦塞梅兰特·奥·塞甘特。 单击em **确定** para salvar例如alteracoes。

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada， voce deve adicionar ação **推送**。 Vá para o lado esquerdo da tela para **操作**，选择a acao **推送** e arraste solte a acao no segundo nó da sua jornada。

![ACOP](./images/journeyactions.png)

没有lado direito da tela， agora voce deve criar sua notificação push.

定义&#x200B;**类别**&#x200B;组合&#x200B;**营销**&#x200B;选择推送表面que权限环境通知推送。 Nesse caso，超级推送&#x200B;**mmeewis-app-mobile-bootcamp**&#x200B;的selecionada用户。

![ACOP](./images/journeyactions1.png)

## 3.3.2编写手册

单击&#x200B;**编辑内容**。

![ACOP](./images/emptymsg.png)

塞吉达，一个长长的阿巴伊克索，前身是：

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação推送。

单击无campo de texto **标题**。

![Journey Optimizer](./images/msg5.png)

Na área de texto， comece **Olá**。 没有个人化的集团。

![Journey Optimizer](./images/msg6.png)

Agora voce precisa trazer o token de personalização para campo **名字** qestá armazenado em `profile.person.name.firstName`。 没有菜单à esquerda，选择&#x200B;**Profile Attributes**，role para baixo/navegue para encontrar o elemento **Person** e clique na seta para avancar um nível até chegar ao campo `profile.person.name.firstName`。 小团无ícone **+**&#x200B;对甘波à tela的辅助线。 单击&#x200B;**保存**。

![Journey Optimizer](./images/msg7.png)

恩陶，请回音。 Clique no ícone de personalização lado do campo **正文**。

![Journey Optimizer](./images/msg11.png)

艾瑞亚·德·特克斯托，埃斯克雷瓦`Bem-vindo(a)`。

![Journey Optimizer](./images/msg12.png)

Em seguida，单击em **上下文属性** e **Journey Orchestration**。

![ACOP](./images/jomsg3.png)

单击em **活动**。

![ACOP](./images/jomsg4.png)

群组no name do sevento，que deve ser semelhante ao seguinte： **yourLastNameBeaconEntryEvent**。

![ACOP](./images/jomsg5.png)

单击&#x200B;**放置上下文**。

![ACOP](./images/jomsg6.png)

单击&#x200B;**POI交互**。

![ACOP](./images/jomsg7.png)

单击&#x200B;**POI详细信息**。

![ACOP](./images/jomsg8.png)

点击编号&#x200B;**+**&#x200B;图标编号&#x200B;**POI名称**。
塞吉达，再说一遍。 单击**保存**。

![ACOP](./images/jomsg9.png)

我们一起吃吧。 小团体没有上级的手法，以备不时之需。

![ACOP](./images/jomsg11.png)

单击&#x200B;**确定**。

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada， voce deve adicionar ação **sendMessageToScreen**。 Vá para o lado esquerdo da tela para **操作**，选择acao **sendMessageToScreen** e arraste solte a acao no terceiro nó da sua jornada。 塞吉达，敬请光临。

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma acao personalizada que irá publicar uma mensagem no **端点** usado pela exibicao na loja。 acao **sendMessageToScreen** espera que múltiplas variáveis sejam definidas。 Voce pode visualizar essas variáveis rolando para baixo até ver **操作参数**。

![ACOP](./images/jomsg16.png)

Agora voce precia definir os valores para cada parametro de acao. 圣内塞萨里奥斯 — 昂代斯岛上的圣塔贝拉岛。

| 参数 | 值 |
|:-------------:| :---------------:|
| 投放 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 名字 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| 事件主题 | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir esses valores， clique no ícone **编辑**。

![ACOP](./images/jomsg17.png)

Em seguida，选择&#x200B;**高级模式**。

![ACOP](./images/jomsg18.png)

塞吉达，在塔贝拉·阿西马的球场上。 单击&#x200B;**确定**。

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID， há uma referencia ao evento`yourLastNameBeaconEntryEvent`。 Lembre-se de substituir `yourLastName` pelo seu sobrenome。

最后，我们来做最后的甜点：

![ACOP](./images/jomsg20.png)

角色para cima e clique em **确定**。

![ACOP](./images/jomsg21.png)

您仍需要为历程命名。 您可以通过单击屏幕右上角的&#x200B;**属性**&#x200B;图标来执行此操作。

![ACOP](./images/journeyname.png)

沃斯·波德插入了nome da jornada aqui。 使用`yourLastName - Beacon Entry Journey`。 单击em **确定** para salvar例如alteracoes。

![ACOP](./images/journeyname1.png)

Agora voce pode publicar sua jornada clicando em **Publish**。

![ACOP](./images/publishjourney.png)

单击em **Publish** novamente。

![ACOP](./images/publish1.png)

我们向大家介绍一下我们的情况。

![ACOP](./images/published.png)

我们来做个活生生的朋友。

你可真够操心的。

Próxima etapa： [3.4 Teste sua jornada](./ex4.md)

[Retornar para fluxo de Usuário 3](./uc3.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
