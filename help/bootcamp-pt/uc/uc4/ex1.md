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
source-wordcount: '942'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 目标

- 对CJA有兴趣
- CJA文件格式
- CJA工作流程的Entenda： da conexao de dados aos insights

## 4.1.1没有Customer Journey Analytics？

OCustomer Journey Analytics(CJA) fornece uma interface em que os times de Analytics， Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada cross-channel (online e offline)do cliente de ponta a ponta。 O CJA é capaz de fornecer contexto e clareza para essa jornada， trazendo uma visao acionável em cima das dificuldades no processo de converso e possibilitando o o planejamento de experiencias relevents e personalizadas nos pontos mais relevents.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. 一个Adobe Experience Platform é é o cérebro da comunicação e da orquestração e， com o CJA， as marcas agora podem contextualizar e visualizar todos esses dados， para que as equipies de negócios e insights posam aprender com eles， analisando toda a jornada online para off-line do cliente.

作为equipes de negócios e insights podem conversar com o CJA， fazer perguntas e obter repostas em tempo real com a interface do usuário de arrastar e soltar， apontar e clicar e fácil de usar do Analysis Workspace.

![演示](./images/cja-adv-analysis1.png)

## 4.1.2普林西比万塔根

Os tres principais benefícios para os clients sao：

- A capacidade de disponibilizar insights para todos (ou seja， democratizar o acesso aos dados)。
- A capacidade de ver cliente em uma jornada context(ou seja， os dados podem ser visualizados sequencialmente， abrangendo múltiplos canais online e-line)。
- 在市场推广方面，开发一个适合个人消费的产品(ou seja， permite que indivíduos usem dados para descloquear insights e análises profundas para ativacao de marketing)。

## 4.1.3 ## 4.1.3 Por que escolher oCustomer Journey Analytics？

O CJA nao se destinate a substituir applicativo de BI autoal， comoPower BI， Microstrategy， Locker ou Tableau. O objetivo designs applicativos de BI é visualizar dados para criar painéis corporativos para que todos em uma organizaçao possam ver métricas important rapidamente. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios， tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente，os applicativos de BI tem sido incapazes de permitir a verdadeira intelligencia do cliente：

- Eles nao podem fazer atribuicao e nao fazem análises de jornada do cliente.
- Os applicativos de BI precisam saber a pergunta com antecedencia
- 作为达多斯银行跨部门顾问
- Habilidades de SQL sao necessárias.
- OS applicativo de BI nao permitem que voce pergunte o motivo de um acontecimento.
- Os applicativos de BI nao tem conexao direta com os pontos de contato do cliente。

Portanto， usuários de negócios e analistas chegam a becos sem saída quase imediatamente， tornando a análise cara， lenta， inflexível e desconectada dos sistemas de acao.

com o CJA voce pode ter uma visao completa da jornada do cliente， usando dados offline e online， com as ferramentas certas para reduzir o tempo de insight， tornando os usuários de negócios independents para entender por que algo aconteceu e como responder a isso.

![演示](./images/cja-use-case.png)

## 4.1.4特拉巴略Customer Journey Analytics概观

Antes de iniciar os próximos exercícios， é é essencial compender quais etapas sao necessárias para trados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights profunds. 我们来做个查默斯·德·特拉巴略·德·查默斯。 瓦莫斯验证：

![演示](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima， nao se esqueca da etapa 0， que é compender os dados que estão disponíveis na Adobe Experience Platform.

**垃圾输入，垃圾输出。** Voce deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform sao configurados. 以coisas为身份的Adobe Experience Platform工厂管理者，nao só na parte de conexao de dados， mas também na hora de construir visualizacaes e fazer análises。

## 4.1.5 Etapa 0：Adobe Experience Platform的Compender esquemas e数据集

Faca登录至Adobe Experience Platform访问URL： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

德波伊斯·德·法泽尔登入后，我去Adobe Experience Platform的帕吉娜。

![数据获取](../uc1/images/home.png)

Antes de continuar， voce precisa selectionar um **沙盒**。 你不要做沙盒，你选择的是``Bootcamp``。 Voce pode fazer isso clicando no ícone **[!UICONTROL Prod]**&#x200B;没有上级direito da tela。 以适当的方式选择沙箱，以备不时之需。

![数据获取](../uc1/images/sb1.png)

在Adobe Experience Platform中验证架构和数据集。

| 数据集 | 架构 |
| ----------------- |-------------| 
| 演示系统 — 网站的事件数据集(Global v1.1) | 演示系统 — 网站的事件架构(Global v1.1) |
| 演示系统 — 呼叫中心的事件数据集(Global v1.1) | 演示系统 — 呼叫中心的事件架构(Global v1.1) |
| 演示系统 — 语音助手的事件数据集(Global v1.1) | 演示系统 — 语音助手的事件架构（全局v1.1） |

梅诺斯的认证机构：

- 标识：CRMID、phoneNumber、ECID、电子邮件。 Quais identidades sao os identificadores primários， quais sao os identificadores secundários？

Voce pode contract os identificadores abrindo um schema e observando o o objeto `_experienceplatform.identification.core`。 验证架构[演示系统 — 网站的事件架构(Global v1.1)](https://experience.adobe.com/platform/schema)。

![演示](./images/identity.png)

- 浏览到comércio dentro do schema [演示系统 — 网站的事件架构(Global v1.1)](https://experience.adobe.com/platform/schema)。

![演示](./images/commerce.png)

- 可视化待办事项os [数据集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e验证待办事项os dados

Agora voce está pronto para comecar a usar a interface do usuário doCustomer Journey Analytics。

Próxima etapa： [4.2 Conecte数据集da Adobe Experience Platform无Customer Journey Analytics](./ex2.md)

[Retornar para fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
