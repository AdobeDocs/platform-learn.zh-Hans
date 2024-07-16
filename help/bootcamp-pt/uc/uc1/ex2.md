---
title: Bootcamp — 实时客户个人资料 — 可视化您自己的实时客户个人资料 — UI — 巴西
description: Bootcamp — 实时客户个人资料 — 可视化您自己的实时客户个人资料 — UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# 1.2以可视化方式呈现客户对实时数据的预犯 — UI

Neste excício， voce irá fazer登录Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI。

## 史托里亚

没有Perfil do cliente em tempo real， todos os dados do perfil sao exibidos juntamente com os dados do evento， além das associacoes de segmentos existes. Os dados mostrados podem vir de qualquer lugar， de aplicativos daAdobe解决方案外部。 Essa é a exibicao mais poderosa da Adobe Experience Platform， o verdadeiro local do sistema de experiencia.

## 1.2.1使用visualização do perfil do cliente na Adobe Experience Platform

访问[Adobe Experience Platform](https://experience.adobe.com/platform)。 德波伊斯·德·法泽尔登入后，我去Adobe Experience Platform的帕吉娜。

![数据获取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙盒**。 我做沙箱是你的精选。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙盒] dedicado。

![数据获取](./images/sb1.png)

无菜单，访问&#x200B;**配置文件** e **浏览**。

![客户个人资料](./images/homemenu.png)

没有painel Visualizador de perfil no seu site， voce pode包含visao geral da identidade。 Cada识别了está vinculada的命名空间。

![客户个人资料](./images/identities.png)

没有painel Visualizador de perfil， agora voce pode ver uma identidade semelhante a seguinte：

| 命名空间 | 标识 |
|:-------------:| :---------------:|
| Experience CloudID (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform， todos os IDs sao igualmente important。 前言，在ECID时代ID服务非常重要，没有上下文到Adobe的ID服务estavam vinculados ao ECID em uma relação hierárquica。 在Adobe Experience Platform上，isso mudou e cada ID pode ser considerado um identificador primário。

要确定上下文所依赖的父项，请遵循规范。 Seo voce perguntar ao seu呼叫中心： **Qual é o ID mais important？** Eles provavelmente responderao： **o número de telefone！** Mas se voce à sua equipe de CRM， eles responderao： **o endereco de email！** A Adobe Experience Platform entende essa complexidade e gerencia isso para voce. Cada aplicativo， seja um aplicativo da Adobe ou nao， se comunicará com a Adobe Experience Platform referindo-se ao ID que consideram principal. 简单的功能。

Para o campo **身份命名空间**，选择&#x200B;**ECID** e para o campo **身份值** insira o ECID que voce pode encontrrar no painel Visualizador de perfil do site do Bootcamp。 单击&#x200B;**视图**。 你背叛了我。 群集编号&#x200B;**配置文件ID** para abrir seu配置文件。

![客户个人资料](./images/popupecid.png)

Agora voce tem uma visão geral de alguns **Atributos de perfil**&#x200B;重要用户要遵守保密协议。

![客户个人资料](./images/profile.png)

访问&#x200B;**事件**， onde voce pode ver as entradas de cada evento de experiencia vinculado ao seu Perfil。

![客户个人资料](./images/profileee.png)

打开opcao de menu **区段成员资格**。 要确保符合资格，我们还要努力。

![客户个人资料](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que voce个性化客户体验与客户。

Próxima etapa： [1.3 Crie um segmento - UI](./ex3.md)

[乌苏亚里奥酒庄酒庄酒庄酒庄1号](./uc1.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
