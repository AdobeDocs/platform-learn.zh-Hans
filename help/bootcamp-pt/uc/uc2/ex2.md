---
title: Bootcamp - Journey Optimizer创建您的活动 — 巴西
description: Bootcamp - Journey Optimizer创建您的活动 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 2.2克雷塞韦托

Faca登录无Adobe Journey Optimizer访问[Adobe Experience Cloud](https://experience.adobe.com)。 单击&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **Home** no Journey Optimizer。 Primeiro，验证一下Sandbox Correto。 不要做沙盒来开发用户`Bootcamp`。 沙盒外部的交互部分，客户端沙盒外部的交互部分。 Neste示例，**Bootcamp**&#x200B;中没有sandbox。 Voce estará na visualização da **Home**&#x200B;执行seu沙盒`Bootcamp`。

![ACOP](./images/acoptriglp.png)

无菜单à esquerda，role para baixo e clique em **配置**。 Em seguida， clique no botao **管理** abaixo de **活动**。

![ACOP](./images/acopmenu.png)

总之我们很清楚。 单击em **创建事件** para comecar a criar seu próprio evento。

![ACOP](./images/emptyevent.png)

新熊雅内拉·德·伊文托·瓦齐亚·伊拉·阿帕雷克。

![ACOP](./images/emptyevent1.png)

Em primeiro lugar， de um nome seu evento como， por示例： `seuSobrenomeAccountCreationEvent` e adicione uma descriçao como， por示例： `Account Creation Event`。

![ACOP](./images/eventdescription.png)

Em seguida， certifique-se de que **类型** está definido como **单一** e， para a selecao de **事件ID类型**，选择&#x200B;**系统生成**。

![ACOP](./images/eventidtype.png)

埃塔帕·塞金特，就是个选择方案。 准备练习的模式。 使用架构`Demo System - Event Schema for Website (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na secao **字段**。 Agora voce deve passar o mouse sobre a secao **字段** e tres ícones弹出式serao exibidos。 点击无&#x200B;**编辑**。

![ACOP](./images/eventpayload.png)

Voce verá uma janela弹出窗口de **字段**， onde voce deve selectionar alguns dos campos que precisamos para personalizar o email。 Escolheremos outros atributos de perfil posteriormente，利用dados já存在于Adobe Experience Platform。

![ACOP](./images/eventfields.png)

没有对象`_experienceplatform.demoEnvironment`，pcertifique-se de selecionar os campos **brandLogo** e **brandName**。

![ACOP](./images/eventpayloadbr.png)

没有对象`_experienceplatform.identification.core`，campo **电子邮件**&#x200B;的certifique-se de selecionar。

![ACOP](./images/eventpayloadbrid.png)

单击em **Ok**&#x200B;以使用备用的alteracoes。

![ACOP](./images/saveok.png)

阿姆·塞吉达，一个长吻鄂酒家。 单击em **保存** mais uma vez para salvar例如alteracoes..

![ACOP](./images/eventsave.png)

我们来看看你有什么好玩的。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **编辑事件**。 将鼠标指针移至&#x200B;**字段** para ver os 3 ícones outra vez。 单击no ícone **查看有效负载**。

![ACOP](./images/viewevent.png)

我们来看看这个例子吧。
Seu evento tem um eventID de orquestracao único， que voce pode encontrar rolando para baixo nesa carga útil （有效负荷）até visualizar `_experience.campaign.orchestration.eventID`。

![ACOP](./images/payloadeventID.png)

我们把Adobe Experience Platform的作品交给你了。 朗布尔目标事件ID，前方为后方。
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

单击em **确定** e，单击em seguida，单击em **取消**。

阿古拉·沃斯·泰努埃斯特·埃西奥。

Próxima etapa： [ 2.3 Crie sua mensagem de email](./ex3.md)

[乌苏亚里奥二号酒庄酒庄酒庄酒庄酒庄酒庄](./uc2.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
