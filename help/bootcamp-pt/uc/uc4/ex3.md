---
title: Bootcamp -Customer Journey Analytics — 创建数据视图 — 巴西
description: Customer Journey Analytics — 创建数据视图 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 3%

---

# 4.3 Crie uma Visualização de Dados

## 目标

- Entenda a UI de Visualização de Dados
- Compreenda as configuracoes básicas de definicao de visita
- Compreenda a atribuicao e a Persistencia em uma Visualização de

## 4.3.1达多斯可视化图表

Agora， com sua conexao concleída， é possível progredir para influenciar a visualização. Uma diferenca entre o Adobe Analytics e o CJA é que o CJA precia de uma visualização de dados para limpar e preparar os dados antes da visualizaçao.

Uma Visualização de Dados é semelhante ao conceito de Virtual Report Suites no Adobe Analytics， onde voce establete as definicoes de visita com reconnecesimento de contexto， filtragem e também como os componentes sao chamados.

塞拉·内塞萨里奥， no mínimo， uma Visualização de Dados por conexao. 没有entanto， para alguns casos de uso， é ótimo ter múltiplas Visualizacoes de Dados para mesma conexao， com o objetvo de fornecer insights differentities para equipes distinas. 我们非常希望能够适应这样的环境。 Alguns示例：

- Métricas de UX apenas para a equipe de UX Design
- 使用os mesmos nomes para KPIs e métricas para oGoogle Analyticse para oCustomer Journey Analytics，para quipe de análise digital fale apenas 1 idioma。
- Visualização de Dados filtrada para mostrar， por explo， dados para apenas um mercado， ou uma marca， ou apenas para dispostivos móveis.

Na tela de **连接**&#x200B;标记了caixa de seleção da conexao que voce acabou de criar。 单击em **创建数据视图**。

![演示](./images/exta.png)

Voce será redirecionado para o fluxo de trabalho **创建数据视图**&#x200B;工作流。

![演示](./images/0-v2.png)

## 4.3.2达多斯可视化定义

Agora voce pode configurar as definicoes básicas para sua Visualização de dados.

![演示](./images/0-v2.png)

**连接**&#x200B;没有前面的练习。 Sua conexao se chama `yourLastName – Omnichannel Data Connection`。

![演示](./images/ext5.png)

Em seguida， de um nome à sua visualização de Dados seguindo este modelo de nomenclatura： `yourLastName – Omnichannel Data View`。

Insira o mesmo valor para descrição： `yourLastName – Omnichannel Data View`。

| 名称 | 描述 |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![演示](./images/1-v2.png)

para **时区**，选择fuso horário **Berlim， Estocolmo， Roma， Berna， Bruxelas， Viena， Amsterda GMT+01:00**。 Este é um cenário realmente interessante， pois algumas empresas operam em diferences países e geografias. Alocar o fuso horário certo para cada país evitará erros típicos de dados， como， por exemplo， acreditar que a maioria das pessoas compra camisetas as 4h no Peru.

![演示](./images/ext7.png)

Voce também pode modificar a nomenclatura das métricas principais(Pessão， Sessao e Evento)。 Isso nao é obrigatório， mas alguns clientes gostam de usar Pessoas， Visitas e Acessos em vez de Pessão， Sessao e Eventos (convencao de nomenclatura padrao do Customer Journey Analytics)。

Agora voce device as seguintes configuracoes definidas：

![演示](./images/1-v2.png)

单击&#x200B;**保存并继续**。

![演示](./images/12-v2.png)

## 4.3.3达多斯可视化图表组件

Neste excício， voce irá configurar os components contessários para analisar os dados e visualizá-los usando o o Analysis Workspace. 内斯塔·尤说：

- Lado esquerdo： Components disponíveis dos datasets selectionados
- Meio：Visualização de Dados的组件
- Lado directo：配置组件功能

![演示](./images/2-v2.png)

>[!IMPORTANT]
>
>在此`Contains data` foi removido de sua visualização de dados. 卡索康塔里奥，不包括坎波。
>
>![演示](./images/2-v2a.png)

Agora voce precisa arrastar e soltar os components necessários para análise nos **已添加组件**。 我愿意，选择各式各样的菜肴，但无菜肴。

Vamos comecar com o primeiro组件： **名称(web.webPageDetails.name)**。 请问组件如何排列 — 如何单独 — 如何排列。

![演示](./images/3-v2.png)

Esse componente é o nome da página， como voce pode derivar da leitura do campo do schema `(web.webPageDetails.name)`。

没有结尾，usar **名称**&#x200B;名称为任何名称的melhor convencao de nomenclatura para um usuário corporativo compreender rapidamente essa dimensao。

Vamos mudar o nome para **页面名称**。 无组件或renomeie na area **组件设置**。

![演示](./images/3-0-v2.png)

作为Configuracoes de persistencia sao **持久性设置**。 在CJA上操作的conceitos de eVars e prop nao existem，将作为configuracoes de Persistencia possibilitam um comportamento semelhante。

![演示](./images/3-0-v21.png)

Se voce nao alterar essas configuracoes， o CJA irá interpretar a dimensão como um **Prop** (nível de ocorrencia)。 Além disso， podemos alterar a Persistencia para tornar a dimensauma **eVar** (persistir o valor ao longo da jornada)。

Seo nao estiver familiarizado com eVars e Props，[leia mais sobre isso na documentacao](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

Vamos deixar o Nome da Página como Prop. Dessa forma， voce nao precisa alterar nenhuma **持久性设置**。

| 要搜索的组件名称 | 新名称 | 持久性设置 |
| ----------------- |-------------| --------------------| 
| 名称(web.webPageDetails.name) | 页面名称 |          |

Em seguida， escolha a dimensao **phoneNumber** e solte-a na tela。 o novo nome device ser **电话号码**。

![演示](./images/3-1-v2.png)

我愿意，变身为Configuracoes de persistencia，Poi o Numero do Celular deve persising no nível do usuário。

Para alteran a Persistencia， role para baixo no menu à direita e abra a aba **持久性**：

![演示](./images/5-v2.png)

将caixa de seleção para modificar作为configuracoes de persistencia。 选择一个&#x200B;**最近** e o escopo **人员（报告窗口）**， pois nos preocupamos apenas com o último número de celular da pessoa。 我们来看看那些未来探访的贵族们，看看他们是否真心诚意。

![演示](./images/6-v2.png)

| 要搜索的组件名称 | 新名称 | 持久性设置 |
| ----------------- |-------------| --------------------| 
| phonenumber | 电话号码 | 最近，人员（报告窗口） |

`web.webPageDetails.pageViews.value`的próximo组件。

无菜单esquerda，请预留`web.webPageDetails.pageViews.value`。 我们很荣幸地来到这里。

在&#x200B;**组件设置**&#x200B;下，替代名称部分&#x200B;**页面查看次数**。

| 要搜索的组件名称 | 新名称 | 归因设置 |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |         |

![演示](./images/7-v2.png)

Para as configuracoes de atribuicao， deixaremos em branco.

Observação： As configuracoes de persistencia nas métricas também podem ser alteradas no Analysis Workspace. Em alguns casos， voce pode optar por configurá-las aqui para eviitar que os usuários de negócios tenham que pensar qual é melhor modelo de persistencia.

我愿意，我愿意，我愿意。

### 尺寸

| 要搜索的组件名称 | 新名称 | 持久性设置 |
| ----------------- |-------------| --------------------| 
| brandName | 品牌名称 | 最近，会话 |
| callfeeling | 通话感觉 |          |
| 呼叫ID | 呼叫交互类型 |          |
| callTopic | 调用主题 | 最近，会话 |
| ecid | ECID | 最近，人员（报告窗口） |
| 电子邮件 | 电子邮件ID | 最近，人员（报告窗口） |
| 付款类型 | 付款类型 |          |
| 产品添加方法 | 产品添加方法 | 最近，会话 |
| 事件类型 | 事件类型 |         |
| 名称(productListItems.name) | 产品名称 |         |
| SKU | SKU（会话） | 最近，会话 |
| Transaction ID | Transaction ID |         |
| URL (web.webPageDetails.URL) | URL |         |
| 用户代理 | 用户代理 | 最近，会话 |

### 梅特里卡

| 要搜索的组件名称 | 新名称 | 归因设置 |
| ----------------- |-------------| --------------------| 
| 数量 | 数量 |          |
| commerce.order.priceTotal | 收入 |         |

Sua configuração deve ser semelhante ao seguinte：

![演示](./images/11-v2.png)

Nao se esqueca de Salvar sua Visualização de Dados. Entao clique em **保存**。

![演示](./images/12-v2s.png)

## 4.3.4梅特里卡斯计算器

Embora tenhamos organizado todo os components na Visualização de dados， voce ainda deve adaptar alguns deles para que usuários de negócios estejam prontos para iniciar suas análises.

Sue voce se lembra， nao trouxemos specificamente Métricas como Adicionar ao Carrinho， Visualização do producto ou Compras para a Visualização de dados. 无entanto，temo uma dimensao chamada： **事件类型**。 Entao， vamos derivar esses tipos de interacao criando 3 métricas calculadas.

Vamos comecar com a primeira Métrica： **产品查看次数**。

没有lado esquerdo，请预留&#x200B;**事件类型**&#x200B;以选择一个维度。 Em seguida， arraste-o e solte-o na tela **包含的组件**。

![演示](./images/calcmetr1.png)

新墨西哥州&#x200B;**事件类型**&#x200B;的群集para selecionar。

![演示](./images/calcmetr2.png)

Agora altere o name e a descrição do componente para os seguintes valores：

| 组件名称 | 组件说明 |
| ----------------- |-------------| 
| 产品查看次数 | 产品查看次数 |

![演示](./images/calcmetr3.png)

Agora vamos contar apenas eventos de **产品查看次数**。 Para fazer isso， role para baixo em **组件设置** até ver Valores de **包含排除值**。 Certifique-se de habilitar a opcao **设置包括/排除值**。

![演示](./images/calcmetr4.png)

Como queremos contar apenas **产品视图**，特别是&#x200B;**commerce.productViews** nos critérios。

![演示](./images/calcmetr5.png)

真是个不错的玩意儿！

Em seguida， repita o mesmo processo para os eventos **添加到购物车** e **购买**。

### 添加到购物车

Primeiro， arraste e solte a mesma dimensao **事件类型**。

![演示](./images/calcmetr1.png)

在杜比里卡多坎普的音乐节上，我们来听听mesma variável。 仍要单击em **添加**：

![演示](./images/calcmetr6.png)

Agora， siga o mesmo processo que fizemos para a métrica Visualizacoes de producto：
- Primeiro altere或称我为descrição。
- Por fim， adicione **commerce.productListAdds** como critério para contar apenas Add To Cart

| 名称 | 描述 | 标准 |
| ----------------- |-------------| -------------|
| 添加到购物车 | 添加到购物车 | commerce.productListAdds |

![演示](./images/calcmetr6a.png)

### 购买次数

Primeiro， arraste e solte a mesma dimensao **事件类型** como fizemos para as duas méticas anteriores.

![演示](./images/calcmetr1.png)

在杜比里卡多坎普的音乐节上，我们来听听mesma variável。 仍要单击em **添加**：

![演示](./images/calcmetr7.png)

Agora， siga o mesmo processo que fizemos para as métricas产品视图e添加到购物车：
- Primeiro altere或称我为descrição。
- Por fim， adicione **commerce.purchases** como critérios para conbilizar apenas as Compras

| 名称 | 描述 | 标准 |
| ----------------- |-------------| -------------|
| 购买次数 | 购买次数 | commerce.purchases |

![演示](./images/calcmetr7a.png)

苏阿组态最后精灵塞梅兰特·奥塞甘特。 单击&#x200B;**保存并继续**。

![演示](./images/calcmetr8.png)

## 4.3.5 Configuração de Dados组件

敬请您重定向：

![演示](./images/8-v2.png)

Nesta aba， voce pode modificar algumas configuracoes important para alterate a forma como os dados sao processados. Vamos comecar定义&#x200B;**会话超时**&#x200B;通信30分钟。 Gracas ao registro de data e hora de cada evento de experiencia， voce pode estender o conceito de uma sessão em todos os canais. 您是来访问现场的呼叫中心的联系人吗？ Usando Tempos Limite de Sessao personalizados，请问是否灵活决定。

![演示](./images/ext8.png)

Nesta aba voce pode modificar outtras coisas como filtrar os dados usando um segmento/filtro. Voce nao precisará fazer isso nest excício.

![演示](./images/10-v2.png)

Quando终端，单击&#x200B;**保存并完成**。

![演示](./images/13-v2.png)

>[!NOTE]
>
>Voce pode voltar a esta Visualização de dados posteriormente e alterar as configuracoes e os components a qualquery momento. 在圣莫斯特拉多斯历史上。

Agora voce pode continuar com parte de visualização e análise！

Próxima etapa： [4.4 Preparacao de dados emCustomer Journey Analytics](./ex4.md)

[Retornar para fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·雷托纳尔](./../../overview.md)
