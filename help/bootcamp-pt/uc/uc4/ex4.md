---
title: Bootcamp -Customer Journey Analytics- Analysis Workspace中的数据准备 — 巴西
description: Bootcamp -Customer Journey Analytics- Analysis Workspace中的数据准备 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparação de dados emCustomer Journey Analytics

## 目标

- Entenda a UO do Analysis Workspace no CJA
- Entenda os conceitos de preparação de dados no Analysis Workspace
- 阿普伦达·卡库洛斯·德·达多斯

## 4.4.1 UI do Analysis Workspace no CJA

OAnalysis Workspace移除了todas as limitacoes típicas de um único relatório do Analytics。 Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquerer número de tabelas de dados， visualizacoes e components(dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Criação instantanea de avarias e segmentos， criação de cortes para análise， criação de alertas， comparação de segmentos， análise de fluxo e de falhas e relatórios de curadoria e agendamento partilhar com qualquer pessoa em seu negócio.

OCustomer Journey Analyticstraz essa solução além dos dados da plataforma。 我建议你先走几步路：

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

在Analysis Workspace的祖先面前我们来回敬一下：

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 赤星专案

我们很荣幸地参加了CJA项目。 CJA计划的一部分。 小团体 **新建**.

![演示](./images/prmenu.png)

塞吉达，敬请光临。 选择器 **空白项目** 恩陶集团 **创建**.

![演示](./images/prmenu1.png)

我愿意，愿意。

![演示](./images/premptyprojects.png)

Primeiro， certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste范本，Visualização de dados的seseleconada é `vangeluwe - Omnichannel Data View`.

![演示](./images/prdv.png)

埃姆·塞吉达，我愿意。 Voce pode usar o seguinte comando para salvar：

| 操作系统 | 快捷键 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

Voce verá este弹出窗口：

![演示](./images/prsave.png)

使用este modelo de nomenclatura：

| 名称 | 描述 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

塞吉达，小集团 **保存**.

![演示](./images/prsave2.png)

## 4.4.2梅特里卡斯计算器

Embora tenhamos organizado todos os componentes na Visualização de dados， voce ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso， durante qualquer processo de analytics， voce pode criar métricas calculadas para profundar a descoberta de insights.

Como示例， criaremos uma taxa de converso calculada usando a metric/evento Compras que definimos na Visualização de dados.

## 转化塔克萨

Vamos comecar a abrir o constructor de métricas calculadas. 小团体 **+** 在Analysis Workspace的初级市场上。

![演示](./images/pradd.png)

O **计算指标生成器** 伊拉·阿帕雷克：

![演示](./images/prbuilder.png)

Encontre **购买** 没有菜单是拉多·埃斯奎多。 Em **量度** 小团体 **全部显示**

![演示](./images/calcbuildercr1.png)

Agora arraste e solte a metric **购买** 一个美特丽卡·科特拉达的作品。

![演示](./images/calcbuildercr2.png)

Normalmente， taxa de conversão significa **转化/会话**. Entao， vamos fazer o mesmo cálculo na tela de definicao de métrica calculada. 进入媒体 **会话** 我绝对不信你，没有事件 **购买**.

![演示](./images/calcbuildercr3.png)

自动观察操作员。

![演示](./images/calcbuildercr4.png)

一个转化类群代表一个前人。 Entao， vamos mudar o formato para porcentagem e selectionar 2 casas decimais.

![演示](./images/calcbuildercr5.png)

最后，更改计算指标的名称和描述：

| 标题 | 描述 |
| ----------------- |-------------| 
| 转化率 | 转化率 |

请认一下，再来一句“美特丽卡”计算器：

![演示](./images/calcbuildercr6.png)

Nao se esqueca de **萨尔瓦尔** 一个微型计算机。

![演示](./images/pr9.png)

## 4.4.3维度计算器：Filtros (segmentacao) e intervalos de data

### 过滤器：维度计算器

可恶的恶灵之夜。 Antes de iniciar qualquer análise， também é interessante criar algumas **计算Dimension**. 这意义重大，非常关键， **区段** 没有Adobe Analytics。 无Customer Journey Analytics，esses segmentos sao chamados de **筛选器**.

![演示](./images/prfilters.png)

分析算法维度计算值作为分析工具的criação de filtros ajudará os usuários de negócios。 Isso irá automatizar algumas tarefas， além de ajudar na parte de adocao. Abaixo estão算法示例：

1. 米迪亚·普洛普利亚，米迪亚·帕加，
2. Visitas novas x recorrentes
3. 客户公司放弃购买

埃塞斯·波德姆·塞克里多斯在阿纳利塞的床上做了一个实验。

### 数据间隔：时间计算维度

作为维度demensoes de tempo sao outro tipo de dimensoes calculadas。 Alguns já foram criados， mas voce também pode criar suas próprias Dimensoes de tempo personalizadas na fase de preparação de dados.

Essas Dimensoes de tempo calculado ajudarao analistas e usuários de negócios a lembrar datas important e usá-las para filtrar e alterar o tempo de relatório. 佩尔贡塔斯·杜维达斯·蒂皮卡斯·坎多·法泽莫斯·阿纳利塞斯：

- 宽都去过黑色星期五吗？ 输入操作系统21 e 29？
- 全都veiculamos aquela campanha de TV em dezembro？
- De quando a quando fizemos as vendas de verao de 2018？ Quero comparar com 2019年。 2019年sabe os dias exatos em？

![演示](./images/timedimensions.png)

Agora voce concluiu o exercício de preparação de dados usando o o Analysis Workspace do CJA.

埃塔帕： [4.5 Visualização usandoCustomer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·托诺纳尔](./../../overview.md)
