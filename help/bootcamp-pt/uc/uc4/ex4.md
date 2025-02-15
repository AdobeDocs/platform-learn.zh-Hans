---
title: Bootcamp - Customer Journey Analytics - Analysis Workspace中的数据准备 — 巴西
description: Bootcamp - Customer Journey Analytics - Analysis Workspace中的数据准备 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## 目标

- Analysis Workspace的CJA
- Entenda os conceitos de preparação de dados no Analysis Workspace
- 阿普伦达·卡库洛斯·达多斯

## 4.4.1 UI do Analysis Workspace无CJA

OAnalysis Workspace删除作为limitacoes típicas de um único relatório do Analytics的标记。 Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizacoes e components(dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Criação instantana de avarias e segmentos， criação de cortes para análise， criação de alertas， comparação de segmentos， análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. 我建议你先走几步：

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on&enablevpops)

请向Analysis Workspace的祖先致敬，并建议：

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on&enablevpops)

### 赤星专案

我们很希望看到一个非常好的项目。 我们做了一个项目。 单击&#x200B;**新建**。

![演示](./images/prmenu.png)

塞吉达，敬请光临。 选择一个&#x200B;**空白项目** entao clique em **创建**。

![演示](./images/prmenu1.png)

我愿意，愿意。

![演示](./images/premptyprojects.png)

Primeiro， certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste示例，一个Visualização de dados a ser selectionada é `vangeluwe - Omnichannel Data View`。

![演示](./images/prdv.png)

塞吉达，我愿意。 Voce pode usar o seguinte comando para salvar：

| 操作系统 | 捷径 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

语音留言弹出窗口：

![演示](./images/prsave.png)

使用este modelo de nomenclatura：

| 名称 | 描述 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida，单击em **保存**。

![演示](./images/prsave2.png)

## 4.4.2梅特里卡斯计算器

Embora tenhamos organizado todo os components na Visualização de dados， voce ainda deve adaptar alguns deles para que usuários de negócios estejam prontos para iniciar suas análises. Além disso， durante qualquer processo de analytics， voce pode criar métricas calculadas para profundar a descoberta de insights.

Como示例， criaremos uma taxa de conversão calculada usando a metric/evento Compras que definimos na Visualização de dados.

## 转化塔克萨

Vamos comecar a abrir o construtor de métricas calculadas. 在Analysis Workspace上单击em **+** para criar sua primeira Métrica calculada。

![演示](./images/pradd.png)

O **计算量度生成器** irá aparecer：

![演示](./images/prbuilder.png)

进入&#x200B;**购买** na lista de métricas no menu do lado esquerdo。 全局&#x200B;**量度**&#x200B;群组&#x200B;**显示全部**

![演示](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **购买** na definicao da métrica calculada。

![演示](./images/calcbuildercr2.png)

Normalmente， taxa de conversão signifa **转化/会话**。 恩陶，我们来做些什么吧。 进入媒体&#x200B;**会话** e arraste e solte-a no criador de definicao，无事件&#x200B;**购买**。

![演示](./images/calcbuildercr3.png)

观察操作员是否自动选择。

![演示](./images/calcbuildercr4.png)

一个并行分类代表一个并行的procentada。 Entao， vamos mudar o formato para porcentagem e seleciconar 2 casas decismais.

![演示](./images/calcbuildercr5.png)

最后，更改计算指标的名称和描述：

| 标题 | 描述 |
| ----------------- |-------------| 
| 转化率 | 转化率 |

请稍等，我们来做个计算：

![演示](./images/calcbuildercr6.png)

Nao se esqueca de **Salvar** a Métrica计算。

![演示](./images/pr9.png)

## 4.4.3维度计算器：Filtros (segmentacao)e intervalos de data

### 过滤器：维度计算

我们来做些事情。 Antes de iniciar qualquer análise， também é interessante criar algumas **计算维度**。 Adobe Analytics上的&#x200B;**区段**&#x200B;很重要， essencialmente。 无Customer Journey Analytics，esses segmentos sao chamados de **筛选器**。

![演示](./images/prfilters.png)

一个用于分析com算法的criação de filtros ajudará os usuários de negócios维度计算值。 伊索·伊拉自动化了阿尔戈马斯·塔雷法斯，阿莱姆·德·阿朱达尔·纳·帕特·德·阿多卡奥。 Abaixo estao算法示例：

1. 米迪亚·普洛普利亚，米迪亚·帕加，
2. Visitas novas x recorrentes
3. 客户公司放弃购买

埃塞斯·费特罗·波德姆·塞克雷多斯·安特斯(ou durante a parte de análise) (o que voce fará no próximo exercício)。

### 数据间隔：时间计算维度

作为维度de tempo sao outtro tipo de dimensoes计算。 Alguns já foram criados， mas voce também pode criar suas próprias Dimensoes de tempo personalizadas na fase de preparação de dados.

Essas Dimensoes de tempo calculado ajudarao analistas e usuários de negócios a lembrar datas e usá-las para filtrar e alterar o tempo de relatório. 佩尔贡塔斯·图维达斯·提皮卡斯·坎多·法泽莫斯·阿纳利塞斯：

- 全岛黑人星期五要吃肉吗？ 进入操作系统21 e 29？
- 全都veiculamos aquela campanha de TV em dezembro？
- De quando a quando fizemos as vendas de verão de 2018？ Quero comparar com 2019. 2019年演讲人？

![演示](./images/timedimensions.png)

Agora voce concluisiu o excício de preparação de dados usando o o Analysis Workspace do CJA.

Próxima etapa： [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Retornar para fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·雷托纳尔](./../../overview.md)
