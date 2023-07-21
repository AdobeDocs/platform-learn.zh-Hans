---
title: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
description: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 目标

- 对CJA的了解
- CJA文件格式
- CJA工作流程的Entenda： da conexao de dados aos insights

## 4.1.1Customer Journey Analytics？

OCustomer Journey Analytics(CJA) fornece uma interface em que os times de Analytics，Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada cross-channel（在线e离线）do cliente de ponta a ponta。 O CJA é capaz de forneceer contexto e clareza para essa jornada， trazendo uma visao acionável em cima das dificuldades no processo de converso e posibilitando o o planejamento de experiencias relevants e personalizadas nos pontos mais relevants.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. CJA的Adobe Experience Platform é o cérebro da comunicação e da orquestração e， com o CJA， as marcas agora podem contextualizar e visualizar todos esses dados， para que as equipes de negócios e insights posam aprender com eles， analisando toda a jornada online para off-line do cliente.

作为equipes de negócios e insights podem conversar com o CJA， fazer perguntas e obter repostas em tempo real com a interface do usuário de arrastar e soltar， apontar e clicar e fácil de usar do Analysis Workspace.

![演示](./images/cja-adv-analysis1.png)

## 4.1.2主要受益者

Os tres principais benefícios para os clients sao：

- A capacidade de disponibilizar insights para todos (ou seja， democratizal o acesso aos dados)。
- A capacidade de ver cliente em uma jornada context(ou seja， os dados podem ser visualizados sequencialmente， abrangendo múltiplos canais online e-line)。
- 一个必要的能力(ou seja， permite que indivíduos usem dados para descloquear insights e análises profundas para ativação de marketing)。

## 4.1.3 ## 4.1.3 Por que escolher oCustomer Journey Analytics？

O CJA nao se destina supplicativo de BI autoal， comoPower BI， Microstrategy， Locker ou Tableau. O objetivo设计applicativos de BI é visualizar dados para criar painéis corporativos para que todos em uma organização possam ver métricas importantes rapidamente。 O objetivo do CJA é traser poder de análise para as equipes de Marketing e Negócios， tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente， os applicativos de BI tem sido incapazes de permitir a verdadeira intelligencia do cliente：

- Eles nao podem fazer atribuicao e nao fazem análises de jornada do cliente.
- Os applicativos de BI precisam saber a pergunta com antecedencia
- 作为达多斯银行的跨部门顾问
- Habilidades de SQL sao necessárias.
- Os applicativo de BI nao permitem que voce pergunte o motivo de um acontecimento.
- Os applicativos de BI nao tem conexao direta com os pontos de contato do cliente。

Portanto， usuários de negócios e analistas chegam a becos sem saída quase imediatamente， tornando a análise cara， lenta， inflexível e desconectada dos sistemas de acao.

Com o CJA voce pode ter uma visao completa da jornada do cliente， usando dados offline e online， com as ferramentas certas para reduzir o tempo de insight， tornando os usuários de negócios independents para entender por que algo aconteceu e como responder a isso.

![演示](./images/cja-use-case.png)

## 4.1.4Customer Journey Analytics通济隆银行

Adobe Experience Platform关于如何运用运用这些理论和方法，我们提出了以下建议： 我们来做个查默斯·德·特拉巴略·德·特拉巴略。 Vamos验证器：

![演示](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima， nao se esqueca da etapa 0， que é compender os dados que estão disponíveis na Adobe Experience Platform.

**倒垃圾，倒垃圾。** Voce deve ter uma ideia clara de quais dados estao disponíveis e como os esquemas na Adobe Experience Platform sao configurados. 以科伊萨为名的Adobe Experience Platform法西利塔拉、科伊萨为名的nao só na parte de conexão de dados、mas também na hora de construir visualizacoes e fazer análises。

## 4.1.5 Etapa 0：Adobe Experience Platform数据集的Compender esquemas e数据集

Faca登录通过Adobe Experience Platform访问URL： [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer登录，voce irá访问página inicial da Adobe Experience Platform。

![数据获取](../uc1/images/home.png)

永恒的万年期，先有先兆 **沙盒**. 做沙箱什么的 ``Bootcamp``. 沃斯·波德·法泽尔是克利坎多·诺伊科内 **[!UICONTROL Prod]** 没有上级的迪雷伊托·达·泰拉。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu sandbox dedicado.

![数据获取](../uc1/images/sb1.png)

在Adobe Experience Platform中验证架构和数据集。

| 数据集 | 架构 |
| ----------------- |-------------| 
| 演示系统 — 网站的事件数据集(Global v1.1) | 演示系统 — 网站的事件架构(Global v1.1) |
| 演示系统 — 呼叫中心的事件数据集（全局v1.1） | 演示系统 — 呼叫中心的事件架构（全局v1.1） |
| 演示系统 — 语音助手事件数据集（全局v1.1） | 演示系统 — 语音助手的事件架构（全局v1.1） |

Certifique-se de ter verificado ao menos：

- 标识：CRMID、电话号码、ECID、电子邮件。 Quais identidades sao os identificadores primários， quais sao os identificadores secundários？

Voce pode contractor os identificadores abrindo um schema e observando o o objeto `_experienceplatform.identification.core`. 架构验证 [演示系统 — 网站的事件架构(Global v1.1)](https://experience.adobe.com/platform/schema).

![演示](./images/identity.png)

- 探索商业开发模式 [演示系统 — 网站的事件架构(Global v1.1)](https://experience.adobe.com/platform/schema).

![演示](./images/commerce.png)

- 可视化待办事项操作系统 [数据集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) 验证os dados

Agora voce está pronto para comecar a usar a interface do usuário doCustomer Journey Analytics。

埃塔帕： [4.2 Conecte datasets da Adobe Experience Platform无Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
