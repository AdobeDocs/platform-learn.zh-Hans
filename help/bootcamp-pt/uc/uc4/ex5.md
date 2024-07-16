---
title: Bootcamp -Customer Journey Analytics — 使用Customer Journey Analytics的可视化图表 — 巴西
description: Bootcamp -Customer Journey Analytics — 使用Customer Journey Analytics的可视化图表 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5乌桑多Customer Journey Analytics可视化图表

## 目标

- Analysis Workspace的Entenda a UI
- Analysis Workspace陶的歌声也不同。
- 对Analysis Workspace的CJA usando进行分析

## Contexto

Neste excício， voce usará o Analysis Workspace no CJA para analisar visualizacoes de produtos， funis de produtos， rotatividade等。

Vamos usar o projeto que voce criou em [4.4 Preparação de dados no Analysis Workspace](./ex4.md)， entao acesse [https://analytics.adobe.com](https://analytics.adobe.com)。

![演示](./images/prohome.png)

Abra seu项目`yourLastName - Omnichannel Analysis`。

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado， voce está pronto para comecar a construir suas primeiras visualizacoes.

![演示](./images/prodataView1.png)

## 广达可视化图表显示产品目录？

Em primeiro lugar， precisamos seleconar as datas certas para analisar os dados. 在菜单上用悬浮物来做日程安排，用拉多来做直菜。 为数据传递选择小团体。

>[!IMPORTANT]
>
>选择&#x200B;**本周** **本月**。 Os dados disponíveis mais recentes foram absorvidos em 19 de setembro de 2022.

![演示](./images/pro1.png)
没有菜单do lado esquerdo (área de componentes)，作为métricas calculadas **产品查看次数**&#x200B;进入。 选择 — 作为e arraste e solte na tela，没有上级direito da tabela de forma livre。

![演示](./images/pro2.png)

自动调整维度&#x200B;**天** será adicionada para criar sua primeira tabela。 Agora voce pode ver sua pergunta respondida imediatamente.

![演示](./images/pro3.png)

塞吉达，点击鼠标后不再复活。

![演示](./images/pro4.png)

单击em **可视化** e选择一个&#x200B;**行** como visualizaçao。

![演示](./images/pro5.png)

声音就像视觉化一样，产生声音。

![演示](./images/pro6.png)

Voce pode alterar o escopo de tempo para o dia clicando em **设置** na visualização。

![演示](./images/pro7.png)

单击no ponto ao lado de **行** e **管理数据Source**。

![演示](./images/pro7a.png)

Em seguida，单击em **锁定选择** e选择项&#x200B;**选定项** para bloquear esta visualizacao para que ela sempre exiba uma linha do tempo de Visualizacoes de produtos。

![演示](./images/pro7b.png)

## 5种麦斯维斯山产碱菌

Quais sao os 5产品是mais vistos？

Lembre-se de salvar o projeto de tempos em tempos.

| 操作系统 | 捷径 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

Vamos comecar a encontrar os 5 productos mais vistos. 没有菜单do lado esquerdo，请输入Nome do produto - Dimensao。

![演示](./images/pro8.png)

Agora arraste e solte **产品名称** para替代维度&#x200B;**天**：

再来一次吧。

![演示](./images/pro10a.png)

塞吉达，是马卡岛上生产产品的温特迪尔。 请将&#x200B;**brandName**&#x200B;设置为baixo do primeiro nome do produto的序列。

![演示](./images/pro13.png)

Em seguida， faca um detalhamento usando o o Agente de usuário. 请假定&#x200B;**用户代理**&#x200B;在白名单中排名。

![演示](./images/pro15.png)

塞吉达：

![演示](./images/pro15a.png)

亲切的朋友，亲切的朋友。 没有lado esquerdo， em visualizacoes， pesquise `Donut`。 Pegue `Donut`， arraste e solte na tela sob a visualização **行** 

![演示](./images/pro18.png)

接下来，在表中，从我们在&#x200B;**Google Pixel XL 32GB Black Smartphone** > **Citi Signal**&#x200B;下执行的划分中选择前5个&#x200B;**用户代理**&#x200B;行。 在选择5行时，按住&#x200B;**CTRL**&#x200B;按钮（在Windows上）或&#x200B;**Command**&#x200B;按钮(在Mac上)。

Em seguida， na Tabela，选择as primeiras 5 linhas de **用户代理**&#x200B;执行详细的fizemos em **Google Pixel XL 32GB黑色智能手机** > **花旗信号**。 Ao selecionar as 5 linhas，选择o botao **CTRL** （无Windows） ou botao **Command** (无Mac)。

![演示](./images/pro20.png)

总之你别说了：

![演示](./images/pro21.png)

Voce pode até adaptar o design para ser mais legível， tornando o o gráfico de **行** e o gráfico de **圆环形** um pouco menor para que sejam exibidos lado a lado：

![演示](./images/pro22.png)

Clique no ponto ao lado de *Donut** para **管理数据Source**。 Em seguida， clique em **锁定选择** para bloquear essa visualização paraque ela sempre exiba uma linha do tempo de Visualizacoes de produto。

![演示](./images/pro22b.png)

Saiba mais sobre visualizacoes usando o o Analysis Workspace em：

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto， da visualização à compra

现有的多音符格式，可解析为questão。 Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **流失可视化图表**。 Vamos usar o último， pois queremos visualizar e analisar ao mesmo tempo.

用油漆涂鸦木豆做成品：

![演示](./images/pro23.png)

Agora adicione um novo painel em branco clicando em **+添加空白面板**。

![演示](./images/pro24.png)

单击&#x200B;**Fallout**&#x200B;的Clique na visualização de 。

![演示](./images/pro25.png)

选择前方的mesmo intervalo de datas do excício。

![演示](./images/prodatef.png)

埃姆·塞吉达，弗拉：

![演示](./images/prodatefa.png)

输入维度&#x200B;**事件类型** nos组件无lado esquerdo：

![演示](./images/pro26.png)

一个维度上的小团体：

![演示](./images/pro27.png)

总之我们总算有这么多。

![演示](./images/pro28.png)

选择项目&#x200B;**commerce.productViews** e arraste eSolte-o no campo **添加接触点** dentro da **流失可视化图表**。

![演示](./images/pro29.png)

Faca o mesmo com **commerce.productListAdds**&#x200B;和&#x200B;**commerce.purchases** e solte-os no campo **添加接触点** dentro da **流失可视化图表**。 苏亚可视化图表图表图表图表图表图表图表图表图表图表图表：

![演示](./images/props1.png)

Voce pode fazer muitas coisas aqui. Alguns示例： comparar ao longo do tempo， comparar cada passo por disposittivo ou comparar por fidelidade. 无内涵， see quisermos analisar coisas interessantes como porque os clientes nao compram depois de adicionar um item ao carrinho， podemos usar a melhor ferramenta do CJA： clicar com o botao direito.

Clique com o botao direito do mouse没有接触点&#x200B;**commerce.productListAdds**。 Em seguida，在此接触点单击em **故障流失**。

![演示](./images/pro32.png)

Uma nova tabela de formato livre criada para analisar o que as pessoas fizeram se nao compraram.

![演示](./images/pro33.png)

由&#x200B;**Page Name**&#x200B;进行的&#x200B;**事件类型**&#x200B;的替代，新生tabela de formato livre， para ver em quais páginas eles estao indo， em vez da Página de confirmacao de compra。

![演示](./images/pro34.png)

## 难道没有场地，象帕吉娜·坎塞拉服务员那样吗？

诺瓦曼特，你这算现实主义的吧。 Vamos usar a análise de fluxo para iniciar parte da descoberta.

用油漆涂鸦木豆做成品：

![演示](./images/pro0.png)

Agora adicione um novo painel em branco clicando em **+添加空白面板**。

![演示](./images/pro0a.png)

小团体&#x200B;**流**。

![演示](./images/pro35.png)

塞吉达：

![演示](./images/pro351.png)

选择前方的mesmo intervalo de datas do excício。

![演示](./images/pro0b.png)

输入维度&#x200B;**页面名称** nos组件无lado esquerdo：

![演示](./images/pro36.png)

一个维度上的小团体：

![演示](./images/pro37.png)

声音以平吉纳斯的身份出现。 输入密码名： **取消服务**。
Arraste e solte **取消服务** na Visualização de fluxo no campo do meio：

![演示](./images/pro38.png)

塞吉达：

![演示](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **取消服务**&#x200B;没有站点também ligaram para o呼叫中心e qual foi o resultado。

Nas维度，请返回Tipo de interação de chamada。 自动确定&#x200B;**调用交互类型** para替代直接的primeira interacao à direita em **流可视化**。

![演示](./images/pro43.png)

Agora voce visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **取消服务**。

![演示](./images/pro44.png)

Em seguida， nas dimensoes，获取&#x200B;**呼叫感觉**。 以替代为目的的Arraste e solte para substitures a primeira interacao à direita na visualização de fluxo。

![演示](./images/pro46.png)

塞吉达：

![演示](./images/flow.png)

Como pode ver， executamos uma análise omnicchannel usando a visualização de fluxo. Gracas a isso， descobrimos que alguns clientes que estavam pensando em cancelar o servico tiveram uma avaliação positiva depois de ligar para o呼叫中心。 塔维兹·滕哈莫斯·穆达多·德·艾迪亚·科玛·普罗莫卡奥？

## 如何删除客户端包含呼叫中心Positivo em relação aos principais KPI？

Primeiramente， vamos segmentar os dados para obter apenas usuários com chamadas **正面**。 没有CJA，没有Segmentos sao chamados de Filtros。 Acesse para filtros na área de componentes （无lado esquerdo）e clique em **+**。

![演示](./images/pro58.png)

Dentro do Construtor de filtro， de um nome ao filtro

| 名称 | 描述 |
| ----------------- |-------------| 
| 通话感觉 — 积极 | 通话感觉 — 积极 |

![演示](./images/pro47.png)

Nos组件(dentro do Construtor de filtro)，输入&#x200B;**Call Feeling** e arraste solte na Definicao do construtor de filtro。

![演示](./images/pro48.png)

Agora选择器&#x200B;**正值**&#x200B;组合值或筛选。

![演示](./images/pro49.png)

替代&#x200B;**人员**。

![演示](./images/pro50.png)

Para最终化，Basta单击em **保存**。

![演示](./images/pro51.png)

恩陶，请回音。 我先去吃干酪，再去吃干酪。

![演示](./images/pro0c.png)

Agora adicione um novo painel em branco clicando em **+添加空白面板**。

![演示](./images/pro24c.png)

选择前方的mesmo intervalo de datas do excício。

![演示](./images/pro24d.png)

单击&#x200B;**自由格式表**。

![演示](./images/pro52.png)

我们来看看你的声音。

![演示](./images/pro53.png)

魔法藻类。 Comece com **产品视图**。 我只能这样生活了。 Voce também pode excluir a métrica **活动**。

![演示](./images/pro54.png)

Faca o mesmo com **人员**，**添加到购物车** e **购买**。 Voce vai acabar com uma tabela como a seguinte.

![演示](./images/pro55.png)

Gracas à primeira análise de fluxo， uma nova pergunta surgiu. Entao decisimos criar esta tabela e verificar alguns KPIem um segmento para responder a essa pergunta。 Como voce pode ver， o tempo de insight é muito mais rápido do que usar SQL ou usar outtras solutions de BI.

## Analysis WorkspaceCustomer Journey Analytics简介

OAnalysis Workspace删除作为limitacoes típicas de um relatório do Analytics的toda。 Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizacoes e components(dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Voce pode criar de forma instantanea filtros e analises， gráficos de coorte， alertas， segmentos， análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa： [4.6 De insights a acao](./ex6.md)

[Retornar para fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·雷托纳尔](./../../overview.md)
