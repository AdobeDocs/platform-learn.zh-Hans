---
title: Bootcamp - Journey Optimizer创建您的活动 — 巴西
description: Bootcamp - Journey Optimizer创建您的活动 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

Faca登录无Adobe Journey Optimizer访问权限 [Adobe Experience Cloud](https://experience.adobe.com). 小团体 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **主页** 没有Journey Optimizer。 Primeiro，验证一下Está对Sandbox Correto的评价。 我做沙盒也行 `Bootcamp`. Para alternar de um sandbox para outtro， clique em Prod e selection o sandbox na lista. Neste示例，不要做沙盒 **Bootcamp**. 达维斯达拉之家 **主页** 执行seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

没有esquerda菜单，role para baixo e clique em **配置**. 塞吉达，小圈子 **管理** abaixo de **事件**.

![ACOP](./images/acopmenu.png)

我们来做个小事。 小团体 **创建事件** para comecar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar， de um nome ao seu evento como， por示例： `seuSobrenomeAccountCreationEvent` e adicione uma descriçao como， por示例： `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida， certifique-se de que **类型** 绝对的科莫 **单一** e， para a seleção de **事件ID类型**，选择器 **系统生成**.

![ACOP](./images/eventidtype.png)

埃塔帕塞吉内特是选择图式的。 准备体育锻炼的模式。 使用模式 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na secao **字段**. Agora voce deve passar o mouse sobre a secao **字段** e tres ícones快显视窗exibidos。 小圈子 **编辑**.

![ACOP](./images/eventpayload.png)

Voce verá uma janela弹出窗口 **字段**，onde voce deve selectionar alguns dos campos que precisamos para personalizar o email。 Escoleremos outros attributos de perfil posteriormente，利用dados já存在于Adobe Experience Platform。

![ACOP](./images/eventfields.png)

无对象 `_experienceplatform.demoEnvironment`， pcertifique-se de selectionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

无对象 `_experienceplatform.identification.core`，坎波地区的certifique-se de selecionar **电子邮件**.

![ACOP](./images/eventpayloadbrid.png)

小团体 **确定** 去救世主，如异类。

![ACOP](./images/saveok.png)

塞吉达，一个叫塞吉达的泰拉阿拜克索酒庄人。 小团体 **保存**  马伊斯·乌玛·韦斯·帕拉萨尔瓦·苏亚斯……

![ACOP](./images/eventsave.png)

我们一起来做吧。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **编辑事件**. 鼠标密码 **字段** 第3个伊科内斯·奥特拉·韦斯。 小圈子 **查看有效负荷**.

![ACOP](./images/viewevent.png)

我们来做个例子吧。
Seu evento tem um eventID de orquestracao único， que voce pode encontracr rolando para baixo nesa carga útil （有效负荷） até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

为了能更好地理解和理解Adobe Experience Platform的秘密，我们准备了各种方法。 Lembre-se deste eventID， voce pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

小团体 **确定** e，em seguida，小团体 **取消**.

Agora voce终止este练习。

埃塔帕： [ 2.3 Crie sua mensagem de email](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
