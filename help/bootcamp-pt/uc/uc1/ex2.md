---
title: Bootcamp - Real-time Customer Profile — 可视化您自己的Real-time Customer Profile - UI — 巴西
description: Bootcamp - Real-time Customer Profile — 可视化您自己的Real-time Customer Profile - UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---

# 1.2真实地呈现客户体验的先决条件 — UI

Neste exercício， voce irá fazer登录Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI。

## 史托里亚

没有Perfil do cliente em tempo real， todos os dados do perfil sao exibidos juntamente com os dados do evento， além das associacoes de segmentos existes. Os dados mostrados podem vir de qualquer lugar， de aplicativos daAdobe解决方案外部。 Essa é a exibicao mais poderosa da Adobe Experience Platform， o verdadeiro local do sistema de experiencia.

## 1.2.1使用visualizaçao do perfil do cliente na Adobe Experience Platform

访问 [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer登录，voce irá访问página inicial da Adobe Experience Platform。

![数据获取](./images/home.png)

永恒的万年期，先有先兆 **沙盒**. 做沙箱也不行，我是布特坎普。 你这小嘴真不赖啊 **[!UICONTROL 生产产品]** 娜丽莎·阿苏尔·娜帕特·苏必利尔·达·泰拉。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙盒] 奉献精神。

![数据获取](./images/sb1.png)

无菜单，访问 **配置文件** e **浏览**.

![客户配置文件](./images/homemenu.png)

没有painel Visualizador de perfil没有seu站点，voce pode包含一个visao geral da identidade。 Cada识别了está vinculada的命名空间。

![客户配置文件](./images/identities.png)

没有painel Visualizador de perfil， agora voce pode ver uma identidade semelhante a seguinte：

| 命名空间 | 标识 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform， todos os IDs sao igualmente importants. 前言，在ECID时代ID服务很重要，没有上下文可为AdobeID服务estavam vinculados ao ECID em uma relaçao hierárquica。 Com a Adobe Experience Platform， isso mudou e cada ID pode ser considerado um identificador primário.

要识别上下文依赖的初级用户，请执行以下操作： Se voce perguntar ao seu呼叫中心： **ID女士是否重要？** Eles提供了回复： **不许打扰你！** Mas se voce perguntar à sua equipe de CRM， eles responderao ： **o endereco de email！** 一个Adobe Experience Platform在语音方面做出了一些复杂的事情。 Cada aplicativo， seja um aplicativo da Adobe ou nao， se comunicará com a Adobe Experience Platform referindo-se ao ID que consideram principal. 简化了功能。

Para o campo **身份命名空间**，选择器 **ECID** e para o campo **标识值** 在ECID中，任何音符都不会出现任何画笔Visualizador de perfil do site do Bootcamp。 小团体 **视图**. 你背叛了我。 小团体否 **配置文件ID** 一手包办事。

![客户配置文件](./images/popupecid.png)

Agora voce tem uma visão geral de alguns **Attributos de perfil** 重要的是要让客户背叛。

![客户配置文件](./images/profile.png)

访问 **事件**，然后把酒瓶当成entradas de cada evento de experiencia vinculado ao seu Perfil。

![客户配置文件](./images/profileee.png)

打开opcao de菜单，打开 **区段成员资格**. 要确保符合资格，我们还要努力。

![客户配置文件](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que voce periencia do cliente para um cliente anonimo ou conhecido.

埃塔帕： [1.3 Crie um segmento - UI](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
