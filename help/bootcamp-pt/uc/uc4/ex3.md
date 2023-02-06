---
title: Bootcamp -Customer Journey Analytics — 创建数据视图 — 巴西
description: Customer Journey Analytics — 创建数据视图 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 072179998d19c32589280defdb257a86d8728fea
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 2%

---

# 4.3 《达多斯可视化图表》

## 奥别蒂沃斯

- 了解可视化图表的UI
- Fropenda as configações básicas de definitição de visita
- Comprenda a atribuição e a Persistência em uma Visualização de

## 4.3.1可视化图表

Agora， com sua conexão censulída， y possivel progredir para influenciar a visualização. Uma diferença entre o Adobe Analytics e o CJA e que o CJA precisa de uma visualização de dados para limpar e prepar a os dados andes da visualização.

Uma Visualização de Dadosé semelhante ao conceito de Virtual Report Suites no Adobe Analytics, onde você estelece as definitções de visita com reconhecimento de contexto， filtargm e também como os componentes são chamados。

Será nequário， no mínimo， uma Visualização de Dados por conexão. 没有entanto， para alguns casos de uso， eótimo ter múltiplas Visualizações de Dados para a mesma conexão， com o objetivo de fornecer insights diferents para equipinitas distintas。 我们可以用você deseja que sua empresa seja orientada por dados， deve adaptar a forma como são vistos em cada equipe。 Alguns执行员：

- UX Métricas de UX apenas para a equipe de UX设计
- 使用mesmos nomes para KPIs e métricas para oGoogle Analyticspara oCustomer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma。
- Visualização de Dados filtrada para mostrar， por smadeo， dados para apenas um mercado， ou uma marca， ou apenas para Dispositivos móveis。

Na tela de **连接** marque a caixa de seleção da conexão que você abou de criar. 团  **创建数据视图**.

![演示](./images/exta.png)

Você será redirecionado para o fluxo de trabalho **创建数据视图** 工作流。

![演示](./images/0-v2.png)

## 4.3.2 《可视化图表》

Agora você pode配置为definitions básicas para sua Visualização de dados。

![演示](./images/0-v2.png)

A **连接** 不行动，就是前身。 沙马 `yourLastName – Omnichannel Data Connection`.

![演示](./images/ext5.png)

Em seguida， dê um nome à sua Visualização de Dados seguindo este modelo de nomenclatura: `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a descrição: `yourLastName – Omnichannel Data View`.

| 名称 | 描述 |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![演示](./images/1-v2.png)

段 **时区**，选择一男 **贝利姆、埃斯托科尔莫、罗马、贝尔纳、布鲁克塞拉斯、维耶纳、阿姆斯特丹GMT+01:00**. 我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标是，我们的目标。 在秘鲁，Alocar o fuso horário certo para cada país evitará erros típicos de dados， como， por smadeo， a a maioria das pessoas compra camisetasàs 4h。

![演示](./images/ext7.png)

Você também pode modificar a nomentcula das métricas principais(Pessoa， Sessão e Evento)。 Isso não e obrigatório， mas alguns clientes gostam de usar Pessoas， Visitas e Acessos em vez de Pessoa， Sessão e Eventos(convenção de nomenclatura padrão doCustomer Journey Analytics)。

Agora você deve ter as seguintes configurações definidas:

![演示](./images/1-v2.png)

团 **保存并继续**.

![演示](./images/12-v2.png)

## 4.3.3 Visualização de Dados的组件

Neste extrecício， você irá configur os components， analyisar os dados e visualizá-los usando o Analysis Workspace。 Nesta IU，há três areas principais:

- 拉多·埃斯凯多：组件disponíveis dos数据集选择者
- 媒体：Visualização de Dados组件
- 拉多·迪雷托：Configurações do componente

![演示](./images/2-v2.png)

>[!IMPORTANT]
>
>我们可以在坎波市 `Contains data` foi removido de sua visualização de dados. 卡索·孔塔里奥，我们的鲜花。
>
>![演示](./images/2-v2a.png)

Agora você preisa arrastar e soltar os components a nos **添加的组件**. Para isso， você deve selecionar os components no menu esquerda e arrastá-los e soltá-los na tela no meio.

Vamos começar com o primeiro componente: **名称(web.webPageDetails.name)**. Pesquise componente e arraste-o e solte-o na tela。

![演示](./images/3-v2.png)

Esse componente e o nome da página， como vice pode derivar da leitura do campo do schema `(web.webPageDetails.name)`.

没有恩坦托，乌萨尔 **名称** como o nome não a melhor convenção de nomenclatura para uário corativo compreander rapadamente essa dimensão

《吸血鬼》 **页面名称**. Cligue no componente e o renomeie na area **组件设置**.

![演示](./images/3-0-v2.png)

佩西斯特恩西亚城 **持久性设置**. Os conceitos de eVars e prop não is existem no CJA， mas as configurações de Persstência possibilitam um comportamento semelhante.

![演示](./images/3-0-v21.png)

请参阅você não alterar essas configurações， o CJA irá interpreta a dimenssão como um **Prop** (nível de ocorência)。 Além disso， podemos a Persistência para tornar a dimensãouma **eVar** (persistir o valor ao longo da jornada)。

她在《家庭福利》中， [莉娅·玛斯·索布尔·伊索·娜·多古塔桑](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

去吧，去吧，去吧。 Dessa备考， você não precisa alterar nenhuma **持久性设置**.

| 要搜索的组件名称 | 新名称 | 持久性设置 |
| ----------------- |-------------| --------------------| 
| 名称(web.webPageDetails.name) | 页面名称 |  |

Em seguida， escolha a dimensão **phoneNumber** 我的日子。 从头开始 **电话号码**.

![演示](./images/3-1-v2.png)

Por fim， vamos alterar as Configurações de persistência， pois o Número do Celular deve persistir no nível do uusário.

Para altera a Persistência，角色是pabaxo no menu a direita e abra a aba **持久性**:

![演示](./images/5-v2.png)

Marque a caixa de seleção para modificar as configurações de persistência。 选择项 **最近** e o escopo **人员（报告窗口）**, pois nos preocupamos apenas com oúltimo número de celular da pessoa. 请参加cliente não preencher o celular em visitas futuras， você ainda verá esse valor preenchido。

![演示](./images/6-v2.png)

| 要搜索的组件名称 | 新名称 | 持久性设置 |
| ----------------- |-------------| --------------------| 
| phoneNumber | 电话号码 | 最近，人员（报告窗口） |

O próximo componente `web.webPageDetails.pageViews.value`.

没有菜单，蛋酱 `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela。

Altere o nome para **页面查看次数** 下 **组件设置**.

| 要搜索的组件名称 | 新名称 | 归因设置 |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |  |

![演示](./images/7-v2.png)

Para as configurações de atribuição， deixaremos em branco.

Observação:As configurações de persistência nas métricas também podem ser alteradas no Analysis Workspace。 Am alguns casos， você pode optar por configá-las aqui para evitar que os usuários de negócios tenham que pensar qual e o melhor modelo de persistência。

Em seguida， você terá que configur várias várias Dimensões e Métricas， conforme indicado na tabela abaixo.

### 维森斯

| 要搜索的组件名称 | 新名称 | 持久性设置 |
| ----------------- |-------------| --------------------| 
| brandName | 品牌名称 | 最近，会话 |
| 冷眼 | 通话感觉 |  |
| 调用ID | 调用交互类型 |  |
| callTopic | 调用主题 | 最近，会话 |
| ecid | ECID | 最近，人员（报告窗口） |
| 电子邮件 | 电子邮件ID | 最近，人员（报告窗口） |
| 付款类型 | 付款类型 |  |
| 产品添加方法 | 产品添加方法 | 最近，会话 |
| 事件类型 | 事件类型 |  |
| 名称(productListItems.name) | 产品名称 |  |
| SKU | SKU（会话） | 最近，会话 |
| Transaction ID | Transaction ID |  |
| URL(web.webPageDetails.URL) | URL |  |
| 用户代理 | 用户代理 | 最近，会话 |

### 美特里察

| 要搜索的组件名称 | 新名称 | 归因设置 |
| ----------------- |-------------| --------------------| 
| 数量 | 数量 |  |
| commerce.order.priceTotal | 收入 |  |

Sua configuração deve semelhante ao seguinte:

![演示](./images/11-v2.png)

Não se esqueça de Salvar sua Visualização de Dados。 恩唐团 **保存**.

![演示](./images/12-v2s.png)

## 4.3.4 Métricas calculadas

Embora tenhamos organizado todos os components na Visualização de dados， você ainda deve adaptar alguns deles para que os usuarios de negócios estejam prontos para iniciar suas analises。

Se você se lembra， não trouxemos sedificamente Métricas como Adicionar ao Carrinho， Visualização do produto ou Compras para a Visualização de dados。 没有entanto，temos uma dimensão chamada: **事件类型**. Então， vamos derivar seses tipos de interção criando 3 métricas calculadas。

Vamos começar com a primeira Métrica: **产品查看**.

不要拉多·埃斯凯多，佩斯奎斯 **事件类型** 选择维度。 阿姆·塞吉达，阿拉斯特 — o e solte-o na tela **包含的组件**.

![演示](./images/calcmetr1.png)

新墨西哥 **事件类型**.

![演示](./images/calcmetr2.png)

Agora altere o nome e a descrição do componente para os seguintes valores:

| 组件名称 | 组件描述 |
| ----------------- |-------------| 
| 产品查看次数 | 产品查看次数 |

![演示](./images/calcmetr3.png)

爱鬼魔鬼夜总会 **产品查看**. Para fazer isso， para baixo em **组件设置** 瓦洛雷斯河 **包含排除值**. 奥普桑河 **设置包含/排除值**.

![演示](./images/calcmetr4.png)

Como queremos contar apenas **产品查看**，特别是 **commerce.productViews** 克里特里奥斯号。

![演示](./images/calcmetr5.png)

我的脑子真够劲！

Em seguida， repita o mesmo processo para os eventos **添加到购物车** e **购买**.

### 添加到购物车

Primeiro， arraste e solte a mesma dimensão **事件类型**.

![演示](./images/calcmetr1.png)

Você verá um alerta poup de um Campo Duplicado， pois estamos usando a mesma variavel. 团 **仍添加**:

![演示](./images/calcmetr6.png)

Agora， siga o mesmo processo que fizemos para a métrica Visualizações de produto:
- Primeiro altere o nome e a descrição.
- 波菲姆，阿迪西奥内 **commerce.productListAdds** como critério para contar apenas Add To Cart

| 名称 | 描述 | 标准 |
| ----------------- |-------------| -------------|
| 添加到购物车 | 添加到购物车 | commerce.productListAdds |

![演示](./images/calcmetr6a.png)

### 购买

Primeiro， arraste e solte a mesma dimensão **事件类型** 我们的朋友们。

![演示](./images/calcmetr1.png)

Você verá um alerta poup de um Campo Duplicado， pois estamos usando a mesma variavel. 团 **仍添加**:

![演示](./images/calcmetr7.png)

Agora， siga o mesmo processo que fizemos para as métricas产品查看添加到购物车：
- Primeiro altere o nome e a descrição.
- 波菲姆，阿迪西奥内 **commerce.purches** 科莫·克里里奥斯·帕拉·康帕尼亚斯

| 名称 | 描述 | 标准 |
| ----------------- |-------------| -------------|
| 购买 | 购买 | commerce.purchases |

![演示](./images/calcmetr7a.png)

Sua configuração final deve semelhante ao seguinte. 团 **保存并继续**.

![演示](./images/calcmetr8.png)

## 4.3.5 Configuração de Dados组件

Você deve ser redirecionado para tela:

![演示](./images/8-v2.png)

Nesta aba， você po de modificar algumas configurações importantes para alterar a forma como os dados são processados。 《魔鬼》 **会话超时** 30分钟。 Graças ao registro de data e hora de cada evento de experiencia， você pode esteno o conceito de uma sessão em todos os canais。 Por smadeo， o que acontece se um cliente ligar para o call center depois de visitar o site? Usando Tempos Limite de Sessão personalizados， você tem muita flibilidade para decidir o que u ma sessão e como sessão irá mesclar os dados。

![演示](./images/ext8.png)

Nesta aba ba você pode modificar outras coisas como filtrar os dados usando um segmento/filtro. 不过，我不会去训练。

![演示](./images/10-v2.png)

干多·塔玛尔，小伙 **保存并完成**.

![演示](./images/13-v2.png)

>[!NOTE]
>
>Você pode voltar a esta Visualização de dados asterar as configurações e os componentes a qualquer momento. 如alterações afetarão a forma como os dados históricos são mostrados。

Agora você pode continuar com a parte de visualização e análise!

埃塔帕： [4.4准备Customer Journey Analytics](./ex4.md)

[Retornar para Fluxo de Uuário 4](./uc4.md)

[托多斯 — 莫杜洛斯](./../../overview.md)
