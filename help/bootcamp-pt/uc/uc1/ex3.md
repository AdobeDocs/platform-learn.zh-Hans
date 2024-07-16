---
title: Bootcamp — 实时客户个人资料 — 创建区段 — UI — 巴西
description: Bootcamp — 实时客户个人资料 — 创建区段 — UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 1.3核心区段 — UI

Neste excício， voce irá criar um segmento usando o o Construtor de Segmentos da Adobe Experience Platform.

## 史托里亚

访问[Adobe Experience Platform](https://experience.adobe.com/platform)。 德波伊斯·德·法泽尔登入后，我去Adobe Experience Platform的帕吉娜。

![数据获取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙盒**。 你不要做沙盒，你选择的是``Bootcamp``。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙盒] dedicado。

![数据获取](./images/sb1.png)

无针对调查问卷的菜单，访问&#x200B;**区段**。 Nesta página， voce tem uma visao geral de todos os segmentos exists. 小集团无波涛和克里尔区段将新克里尔区段分开。

![区段](./images/menuseg.png)

Quando estiver no novo construtor de segmentos， voce irá perceber imediatamente a opcao de menu **属性** e a referencia do **XDM个人资料**。

![区段](./images/segmentationui.png)

XDM是一种语言或体验工具，XDM团队是构建分段的基础工具。 Todos os dados ingeridos na platforma devem ser mapeados em relação XDM e， portanto， todos os dados se tornam parte do mesmo modelo de dados， independentemente da origem desies dados. Isso oferece uma grande vantagem ao criar segmentos， pois a partitir dessa interface do usuário do construtor de segmento， é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos crados no Construtor de segmentos podem ser envirados para solutions como Adobe Target， Adobe Campaign e Adobe Audience Manager para ativacao.

Agora voce precisa criar um segmento de todos os clientes que visualizaram o producto **Real-Time CDP**。

建筑物的节段，节日前的节奏。 Voce pode encontracr todos os Eventos de experiencia clicando no ícone **事件** na barra de menu **字段**。

![区段](./images/findee.png)

Em seguida， voce verá o nó **XDM ExperienceEvents** do nível superior. 单击em **XDM ExperienceEvent**。

![区段](./images/see.png)

访问&#x200B;**产品列表项**。

![区段](./images/plitems.png)

选择一个&#x200B;**名称** e arraste e solte o objeto **名称** do menu à esquerda na tela do construtor de segmentos na secao **活动**。 塞吉达：

![区段](./images/eewebpdtlname.png)

O parametro de comparação deve ser **等于** e，无campo de entrada，insira **实时CDP**。

![区段](./images/pv.png)

Sempre que adicionar um elemento ao construtor de segmentos， voce pode clicar no botao **刷新估计** para obter uma nova estimativa da populaçao em seu segmento。

![区段](./images/refreshest.png)

Para **评估方法**，选择&#x200B;**Edge**。

![区段](./images/evedge.png)

我愿意，你愿意。

Como modelo de nomenclatura，使用：

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida， clique no botao **保存并关闭**&#x200B;段为已保存的会话。

![区段](./images/segmentname.png)

Agora voce irá retornar à página de visão geral do segmento， onde verá uma visualização de amostra dos perfis de clientes que se qualificam para o seu segmento.

![区段](./images/savedsegment.png)

Agora voce pode continuar no próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa： [1.4 Acao： envie seu segmento para o Adobe Target](./ex4.md)

[乌苏亚里奥酒庄酒庄酒庄酒庄1号](./uc1.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
