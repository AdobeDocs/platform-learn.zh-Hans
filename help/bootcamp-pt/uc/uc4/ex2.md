---
title: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics的Adobe Experience Platform数据集 — 巴西
description: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics的Adobe Experience Platform数据集 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 4.2 Conecte datasets da Adobe Experience Platform无Customer Journey Analytics

## 目标

- Compreenda UI da conexao de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilacao de dados
- Aprenda o conceipt de streaming de dados no客户历程

## 4.2.1科内克索

访问 [analytics.adobe.com](https://analytics.adobe.com) 段存取或Customer Journey Analytics。

Customer Journey Analytics真不容易，小子 **连接**.

![演示](./images/cja2.png)

Aqui voce pode ver todas作为CJA e a Plataforma的区分联谊会节日。 Essas conexovo tem to mesmo objetvo dos conjuntos de relatórios no Adobe Analytics. 没有entanto，是互补的区别。 Todos os dados vem de datasets da Adobe Experience Platform。

要吃早餐，就要吃了。 小团体 **创建新连接**.

![演示](./images/cja4.png)

验证UI **创建连接** UI。

![演示](./images/cja5.png)

Agora voce pode dar um nome à sua conexao.

使用este modelo de nomenclatura： `yourLastName – Omnichannel Data Connection`.

示例： `vangeluw - Omnichannel Data Connection`

从沙盒到沙盒的声音和声音的声音。 无菜单沙盒，选择一个seu沙盒，que deve ser `Bootcamp`. Neste示例，o沙盒一个使用者é **Bootcamp**. 坦贝姆·德夫德菲尼奥 **平均每日事件数** 到 **少于100万**.

![演示](./images/cjasb.png)

Após selecionar seu sandbox， voce pode comecar a adicionar datasets a esta conexao. 小团体 **添加数据集**.

![演示](./images/cjasb1.png)

## 4.2.2Adobe Experience Platform中的选择数据集

数据集预设 `Demo System - Event Dataset for Website (Global v1.1)`. 小团体 **+** para adicionar或数据集esta conexao。

![演示](./images/cja7.png)

Agora pesquise e marque as caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

塞吉达，敬请光临。 小团体 **下一个**.

![演示](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID比索

O objetvo agora é juntar搜索数据集。 Para cada数据集selecionado， voce verá um campo chamado **人员ID**. Cada数据集tem seu próprio campo de ID de pessoa.

![演示](./images/cja11.png)

Comoo voce pode ver，一个可以自动进行ID da pessoa seleconado的少年。 我是Adobe Experience Platform的首席律师。 Como示例，aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`，您的个人身份确认书 `phoneNumber`.

![演示](./images/cja13.png)

没有entando，voce ainda pode influenciar qual identificator será usado para compilar datasets para sua conexao。 Voce pode usar qualquer identificator configurado no esquema vinculado ao seu dataset. 无菜单挂起对ID分配的para探查器em cada数据集。

![演示](./images/cja14.png)

Conforme mencionado， voce pode definir不同IDs de pessoa para cada数据集。 Isso permite reunir diferentes datasets de múltiplas origins no CJA. 想象一下trader NPS ou dados de pesquisa que seriam muito interessantes e úteis para compreender o contexto motivo de um acontecimento。

不重要campo ID da pessoa nao é important， desde que o valor nos campos ID da pessoa responderda。 迪加莫斯·克·泰莫斯 `email` em um数据集 `emailAddress` 超数据集定义共同ID da pessoa。 se `delaigle@adobe.com` Tiver o mesmo valor para o campo ID da pessoa em ambos os datasets， o CJA poderá compilar os dados.

Autualmente，现有的算法超越限制，comportamento anonimo para conhecido。 以perguntas frequentes aqui的身份咨询： [常见问题解答](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hans).


### Compilando os dados usando o o ID da pessoa

Agora que voce compreende o conceito de compilar datasets usando o o ID da pessoa， vamos escolher `email` como ID da pessoa para cada数据集。

![演示](./images/cja15.png)

访问ID为pessoa的cada数据集自动化。

![演示](./images/cja12a.png)

坎波ID da pessoa escolhendo o `email` 不吃甜食。

![演示](./images/cja17.png)

Depois de compilar os tres datasets， estamos prontos para continuar.

| 数据集 | 人员 ID |
| ----------------- |-------------| 
| 演示系统 — 网站的事件数据集(Global v1.1) | 电子邮件 |
| 演示系统 — 语音助手事件数据集（全局v1.1） | 电子邮件 |
| 演示系统 — 呼叫中心的事件数据集（全局v1.1） | 电子邮件 |

Voce também precisa garantir que， para cada dataset， essas ocoes estejam habilitadas：

- Importar todos os novos dados
- Preencher可处理现有DADOS任务
- Preencher tipo de fonte de dados com “其他”
- 预览数据集的mesmo nome do Dataset的descriçao com

小团体 **添加数据集**.

![演示](./images/cja16.png)

小团体 **保存** 我为你的锻炼做些准备。 Depois de criar sua **连接**，pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![演示](./images/cja20.png)

埃塔帕： [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·托诺纳尔](./../../overview.md)
