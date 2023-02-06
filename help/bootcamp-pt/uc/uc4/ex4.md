---
title: Bootcamp -Customer Journey Analytics-Analysis Workspace的数据准备 — 巴西
description: Bootcamp -Customer Journey Analytics-Analysis Workspace的数据准备 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4准备Customer Journey Analytics

## 奥别蒂沃斯

- 关于UO的Analysis Workspace CJA
- 为达多斯而建立的Analysis Workspace
- 阿普伦达的卡库洛斯德达多斯

## 4.4.1 UI用于Analysis Workspace no CJA

O Analysis Workspace将todas作为limitações típicas de umúnico relatório do Analytics删除。 Ele fore uma tela hobusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizações e componentes(dimensões， métricas， segmentos e gralearidades de tempo)para um projeto。 Criação instantânea de avarias e segmentos， criação de cortes para análise， criação de alertas， compatorção de segmentos， análise de fluxo e falhas e relatrios de curadoria e a agendamento para compartilhar com qualquer pessssoem seu negócio。

OCustomer Journey Analyticstraz essa solução além dos dados da plataforma. É altamente recommendável assistia a vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

她不是Analysis Workspace人，是我推荐的。

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 克里·苏·普罗耶托

Agora de criar seu primeiro projeto do CJA. 在CJA中，Vá para a aba de projetos dentro do CJA. 团 **新建**.

![演示](./images/prmenu.png)

她的话，我就是个空话。 选择项 **空白项目** então gliea em **创建**.

![演示](./images/prmenu1.png)

那是我的天。

![演示](./images/premptyprojects.png)

Primeiro， certifique-se de selecionar a Visualização de dados correta no canto super direito da tela。 Neste smadeo， a Visualização de dados a serselectionadaé `vangeluwe - Omnichannel Data View`.

![演示](./images/prdv.png)

我们要去救我。 Você pode usar o seguinte comando para salvar:

| 操作系统 | 短切 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

以前的弹出窗口是：

![演示](./images/prsave.png)

使用este modelo de nomenclataura:

| 名称 | 描述 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

阿姆·塞吉达，小团 **保存**.

![演示](./images/prsave2.png)

## 4.4.2梅特里卡斯计算器

Embora tenhamos organizado todos os components na Visualização de dados， você ainda deve adaptar alguns deles para que os usuarios de negócios estejam prontos para iniciar suas analises。 Além disso， durante qualquer processo de analytics， você pode criar métricas calculadas para profundar a descoberta de insights.

以Como为例， Criaremos Taxa de conversão calcuada usando a métrica/evento Compras que definitios na Visualização de dados。

## 转化税

我们是个建筑师。 团 **+** Para criar sua primeira Métrica calcuda no Analysis Workspace

![演示](./images/pradd.png)

O **计算量度生成器** 伊拉·阿帕雷克：

![演示](./images/prbuilder.png)

恩康特 **购买** 不吃菜的，就是拉多·埃斯凯多。 Em **量度** 团 **显示全部**

![演示](./images/calcbuildercr1.png)

美国人 **购买** 那就算是计算。

![演示](./images/calcbuildercr2.png)

Normalmente， taxa de conversão ampila **转化/会话**. Então， vamos fazer o mesmo cálculo na de definitição de métrica calculada. 美国 **会话** e arraste e solte a no criador de definitição， no evento **购买**.

![演示](./images/calcbuildercr3.png)

观察divisãoé selecionado automaticamente的操作员。

![演示](./images/calcbuildercr4.png)

一个代表porcentagem的taxa de conversãoé comumente。 Então， vamos mudar o formato para porcentagem e selecionar 2 casas decimais。

![演示](./images/calcbuildercr5.png)

最后，更改计算量度的名称和描述：

| 标题 | 描述 |
| ----------------- |-------------| 
| 转化率 | 转化率 |

Por fim， altere o nome e a descrição da métrica calculada:

![演示](./images/calcbuildercr6.png)

昂塞什凯萨德 **萨尔瓦尔** 一个美国的计算器。

![演示](./images/pr9.png)

## 4.4.3维度计算：Filtros(segmentação)e intervalos de datas

### 过滤器：维森斯计算器

卡尔库洛斯·诺·德韦纳斯·帕拉·梅特里卡斯。 Antes de iniciar qualquer análise， também e intersante criar algumas **计算Dimension**. 意义重大，也很加安全， **区段** 不，Adobe Analytics。 没有Customer Journey Analytics，塞门托斯圣查马多斯 **过滤器**.

![演示](./images/prfilters.png)

criação de filtros ajudará os usários de negócios a iniciar o analytics com algumas dimensionsões calculadas valiosas。 Isso irá automatizar algumas tarefas， além de ajudar na parte de adoção. Abaixo estão alguns exemplois:

1. Mídia Própria， Mídia Paga，
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Ses filtros podem ser criados ou durante a parte de análise(você fará no próximo excrecio)。

### 数据间隔：节奏计算器

就象dimensøes de tempo são outro tipo de dimensøes calculadas。 Alguns já foram criados， mas você também pode criar suas próprias Dimensões dempo personalizadas na fase de preparição de dados。

Essas Dimensões de tempo calculado ajudarão analistas e uuários de negócios a lembrar datas importantes e usá-las para filtrar e alterar o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análises:

- 凡多有黑色的星期五吗？ 恩特雷奥斯21 e29?
- 坎多·维卡莫斯·阿奎拉·坎帕尼亚·德桑布罗电视节目？
- 2018年的旺达斯·德凡多·德·凡多·菲泽莫斯？ 查询比较网2019。 2019年，我是个好人？

![演示](./images/timedimensions.png)

Agora você总结了为Analysis Workspace争取和平而努力的经验。

埃塔帕： [4.5 Visualização usandoCustomer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Uuário 4](./uc4.md)

[托多斯 — 莫杜洛斯](./../../overview.md)
