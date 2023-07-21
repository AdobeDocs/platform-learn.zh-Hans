---
title: Bootcamp — 将物理和数字相结合 — Journey Optimizer创建您的活动 — 巴西
description: Bootcamp — 将物理和数字相结合 — Journey Optimizer创建您的活动 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 2133b560-09d8-419d-bb99-05d0f3df52cc
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 3.2 Crie seu evento

Faca登录无Adobe Journey Optimizer访问权限 [Adobe Experience Cloud]. 小团体 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Voce será redirecionado para a **主页** 没有Journey Optimizer。 Primeiro，验证一下Está对Sandbox Correto的评价。 我做沙盒也行 `Bootcamp`. Para alternar de um sandbox para outtro， clique em **Prod** 选择沙盒和沙盒。 Neste示例，不要做沙盒 **Bootcamp**. 达维斯达拉之家 **主页** 执行seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

没有esquerda菜单，role para baixo e clique em **配置**. 塞吉达，小圈子 **管理** em事件。

![ACOP](./images/acopmenu.png)

我们来做个小事。 小团体 **创建事件** para comecar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

Em primeiro lugar， de um nome ao seu evento como， por示例： `yourLastNameBeaconEntryEvent` e adicione uma descriçao como， por示例： `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida， certifique-se de que **类型** 绝对的科莫 **单一** e， para a seleção de **事件ID类型**，选择器 **系统生成**.

![ACOP](./images/eventidtype.png)

埃塔帕塞吉内特是选择图式的。 准备体育锻炼的模式。 使用模式 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na secao **字段**. Agora voce deve passar o mouse sobre a secao **字段** e tres ícones快显视窗exibidos。 小集团，不，不 **编辑**.

![ACOP](./images/eventpayload.png)

Voce verá uma janela弹出窗口 **字段**，onde voce deve selecionar alguns dos campos que precisamos para personalizar a jornada。 Escolheremos outros attributos de perfil posteriormente，利用dados já存在于Adobe Experience Platform

![ACOP](./images/eventfields.png)

在物件上发挥的作用 `Place context` 我买了一个caixa de seleção。 Com isso， todo o contexto da localização do cliente será disponibilizado para a jornada. 小团体 **确定** 如变体。

![ACOP](./images/eventpayloadbr.png)

塞吉达，我们来个长沙发吧。 小团体 **保存** 马伊什·乌马·韦斯·帕拉萨尔瓦斯·苏亚斯·阿尔泰拉科斯。

![ACOP](./images/eventsave.png)

我们一起来做吧。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **编辑事件** 梅斯·乌玛·维兹。 鼠标密码 **字段** 第3个艾科内斯。 小圈子 **视图**.

![ACOP](./images/viewevent.png)

Agora voce verá um expero do payload esperado.
Seu evento tem um eventID de orquestracao único， que voce pode encontracr rolando para baixo nesa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

为了能更好地理解和理解Adobe Experience Platform的秘密，我们准备了各种方法。 Lembre-se deste eventID， voce pode precisar dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

小团体 **确定** e，em seguida，小团体 **取消标记**.

沃斯·特米努埃斯特·艾希西奥。

埃塔帕： [3.3 Crie sua jornada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
