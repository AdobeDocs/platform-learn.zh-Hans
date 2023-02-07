---
title: Bootcamp - Journey Optimizer创建活动 — 巴西
description: Bootcamp - Journey Optimizer创建活动 — 巴西
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

Faça login no Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). 团 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **主页** 不，Journey Optimizer。 普里米罗，我的梦想是沙盒的。 没人会沙箱里的 `Bootcamp`. para alternar de um sandbox para outro， cligue em Prod e selecione o sandbox na lista。 新样本，没人做沙盒 **Bootcamp**. Você estará na visualização da **主页** 做seu沙盒 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

没有菜单，角色是“baixo e clie” **配置**. Em seguida，帮不了 **管理** abaixo de **事件**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. 团 **创建事件** 为此，我谨请客人。

![ACOP](./images/emptyevent.png)

乌玛·诺瓦·雅内拉·德·埃文托·瓦齐亚·阿帕雷克。

![ACOP](./images/emptyevent1.png)

Em primeiro lugar， dê um nome ao seu evento como， por smadeo: `seuSobrenomeAccountCreationEvent` e adicione uma描述como， por smade: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida， certifique-se de que **类型** 我就是 **单一** e，第seleção de **事件ID类型**，选择一项 **系统生成**.

![ACOP](./images/eventidtype.png)

一个塞莱桑的图式。 我准备了这项运动。 使用架构 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， você vários campos sendo selecionados na seção **字段**. Agora você deve passar o mouse sobre a seção **字段** e trêsícones弹出窗口serão exibidos。 伊科内集团 **编辑**.

![ACOP](./images/eventpayload.png)

Você verá uma janela poup de **字段**, onde você deve selecionar alguns dos campos que precisamos para personalizar o e-mail. Escolheremos outros atributos de perfil后验室，利用ando os dados já exists na Adobe Experience Platform。

![ACOP](./images/eventfields.png)

无对象 `_experienceplatform.demoEnvironment`, pcertifique se de selecionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

无对象 `_experienceplatform.identification.core`, certifique se de selecionar o campo **电子邮件**.

![ACOP](./images/eventpayloadbrid.png)

团 **确定** 萨尔瓦·苏亚斯·阿尔特拉松斯。

![ACOP](./images/saveok.png)

Em seguida，一个有抗感染力的人。 团 **保存**  马伊斯·乌马·韦斯·萨尔瓦·苏亚斯·阿尔特拉松斯……

![ACOP](./images/eventsave.png)

我们要好好地去。

![ACOP](./images/eventdone.png)

Miclu n seu evento novamente para abrir mais uma vez a tela **编辑事件**. 老鼠奶酪 **字段** 第3段，西科内斯·韦兹。 伊科内集团 **查看有效负载**.

![ACOP](./images/viewevent.png)

我的心里很清楚。
Seu evento tem um事件ID de orquestraçãoúnico， qu você pode encontrar rolando para baixo nessa cargaútil（有效负荷）até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventIDé o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você a construirá em dos próximos excrecios. Lembre-se deste eventID， você pode precisar dele posterormente。
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

团 **确定** e、em、seguida、glicke em **取消**.

我的行动中，我不由自主。

埃塔帕： [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[乌萨里奥2号河道](./uc2.md)

[托多斯 — 莫杜洛斯](../../overview.md)
