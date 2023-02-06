---
title: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
description: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 奥别蒂沃斯

- 关于CJA
- 教皇和教皇协会
- Entenda o workflow do CJA:达科内桑德达多斯奥斯洞察

## 4.1.1Customer Journey Analytics?

OCustomer Journey Analytics(CJA)forence uma interface em os times de Analytics、Negócios e Tecnologia conseguem unir todos dos da dos da companisa a jornada cross-channel(online e offline)do cliente de ponta a ponta。 O CJAé capaz de fornecer contexto e clareza para essa jornada， trazendo uma visão acionável em cima dificuldades no processo de conversão e possibilitando o planejamento de experincias relatentes e personalizadas nos pontos matos is relatedantes。

在Adobe Experience PlatformAnalysis Workspace。 一个Adobe Experience Platform,com o CJA， marcas agora podem contextulazar e visualizar todos， para que as ee equipes de negócios e insights possam aprender com eles， analisando toda a jornada on-line para-off-do cliente。

当enegócios e insights podem conversar com o CJA时， fazer perguntas e obter respostas em tempo real com a interface do usuário da arrastar e soltar， apontar e clicar e fácil de usar do Analysis Workspace。

![演示](./images/cja-adv-analysis1.png)

## 4.1.2主要优势

Os três principais bentios para os clients são:

- 一种能力 — 即对地分析 — 的洞察(或者，民主主义者，或者，或者，或者，或者，或者。
- cliente em jornada上下文(ou seja， os dados podem ser visualizados sequencialmente， abrangendo múltiplos canais on-line off-line)。
- a capacidade de aproveitar o poder dos dados sem qua haja a neussidade(ou seja， permite que indivíduos usem dados par desbloquear insights e análises profundas para ativação de marketing)。

## 4.1.3 ## 4.1.3 Por que escolher oCustomer Journey Analytics?

O CJA não se destina a suptiir um applicativo de BI atual， comoPower BI, Microstrategy， Locker ou Tableau。 O objetivo dess aplicativos de BIé visualizar dados para criar painéis corpativos para que todos em organizadação possam ver métricas importantes rapidamente. O objetivo do CJAé trazer poder de análise para as emarketing e Negócios， tornando-o u ma ferramenta de análise obrigatória para essoas



Tradicionalmente， os aplicativos de BI têm sido incapazes de permitir a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI precisam saber a pergunta com antecedência
- 就像大道银行
- Habilidades de SQL são dequestárias.
- Os aplicativos de BI não permitem vicke pergunte to motio de um acontecmento.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente。

Portanto、uusários de negócios e analistas chegam a becos sem saída quase imediatamente、tornando a análise cara、lenta、inflexível e desconectada dos sistemas de ação。

Com o CJA você pode ter uma visão completa da jornada do cliente， usando dados offline e online， com as ferramentas certas para reduzir o tempo de insight， tornando os usurios usuários de negócios independentes par que algo a contecou e como a isso。

![演示](./images/cja-use-case.png)

## 4.1.4全面Customer Journey Analytics

Antes de iniciar os próximos experacticios， e essencial compression quais etapas são equisárias para trazer da Adobe Experience Platform para o CJA visualizá-los e obter alguns insights profundos。 我要给你个机会。 Vamos verificar:

![演示](./images/cja-work-flow.jpg)

antes de iniciar as etapa acima， não se esqueça da etapa 0, que e funder os dados que estão disponíveis na Adobe Experience Platform。

**垃圾进去，垃圾出去。** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são configurados。 Comprender os dados que estão na Adobe Experience Platform falirá as coisas， não só na parte de conexão de dados， mas também na hora de construcir visualizações e fazer análises。

## 4.1.5 Etapa 0:全面数据集Adobe Experience Platform

Faça login na Adobe Experience Platform acessando a URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登录后，我会在Adobe Experience Platform。

![数据获取](../uc1/images/home.png)

连续性，职业是选择者 **沙盒**. 没人会用沙盒做选择 ``Bootcamp``. 法泽岛 **[!UICONTROL 生产]** 不能向上级迪雷托·达特拉下手。 从沙盒到沙盒，从沙盒到沙盒。

![数据获取](../uc1/images/sb1.png)

Verifique将架构与数据集一起托管在Adobe Experience Platform。

| 数据集 | 架构 |
| ----------------- |-------------| 
| 演示系统 — 网站事件数据集（全局v1.1） | 演示系统 — 网站的事件模式（全局v1.1） |
| 演示系统 — 呼叫中心事件数据集（全局v1.1） | 演示系统 — 呼叫中心事件模式（全局v1.1） |
| 演示系统 — 语音助理事件数据集（全局v1.1） | 演示系统 — 语音助理事件模式（全局v1.1） |

Certifique-se de ter verificado ao menos:

- 身份：CRMID、phoneNumber、ECID、电子邮件。 哪些标识是主标识符，哪些是次标识符？
您可以通过打开架构并查看对象来查找标识符 `_experienceplatform.identification.core`. 查看架构 [演示系统 — 网站的事件模式（全局v1.1）](https://experience.adobe.com/platform/schema).

- 标识：CRMID、phoneNumber、ECID、电子邮件。 Qua是圣身份识别者，圣身份识别者，塞昆达里奥斯？
Você pode enconcrar os identification abrindo um schema e objeto observanto o o bjeto `_experienceplatform.identification.core`. 架构验证 [演示系统 — 网站的事件模式（全局v1.1）](https://experience.adobe.com/platform/schema).

![演示](./images/identity.png)

- 探索o objeto de comércio dentro做模式 [演示系统 — 网站的事件模式（全局v1.1）](https://experience.adobe.com/platform/schema).

![演示](./images/commerce.png)

- 可视化工具 [数据集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dado

Agora você está ponto para começar a usar a interface do usuário doCustomer Journey Analytics。

埃塔帕： [连接数据集da Adobe Experience Platform无Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Uuário 4](./uc4.md)

[托多斯 — 莫杜洛斯](../../overview.md)
