---
title: Bootcamp — 实时客户个人资料 — 创建区段 — UI — 巴西
description: Bootcamp — 实时客户个人资料 — 创建区段 — UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 Crie um segmento - UI

Neste exercício， voce irá criar um segmento usando o o Construtor de Segmentos da Adobe Experience Platform.

## 史托里亚

访问 [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer登录，voce irá访问página inicial da Adobe Experience Platform。

![数据获取](./images/home.png)

永恒的万年期，先有先兆 **沙盒**. 做沙箱什么的 ``Bootcamp``. 你这小嘴真不赖啊 **[!UICONTROL 生产产品]** 娜丽莎·阿苏尔·娜帕特·苏必利尔·达·泰拉。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙盒] 奉献精神。

![数据获取](./images/sb1.png)

无菜单，访问 **区段**. Nesta página， voce tem uma visão geral de todos os segmentos exists. 小团体no botao + Criar segmento para comecar a criar um novo segmento。

![区段](./images/menuseg.png)

Quando estiver no novo constructor de segmentos， voce irá perceber imente a opcao de menu **属性** 我们来做个参考 **XDM个人资料**.

![区段](./images/segmentationui.png)

XDM是一种语言，是一种经验性的语言，XDM术语是一种构造分段的基础。 Todos os dados ingeridos na platforma devem ser mapeados em relacao XDM e， portanto， todos os dados se tornam parte do mesmo modelo de dados， independentemente da origem desies dados. Isso oferece uma grande vantagem ao criar segmentos， pois a partir dessa interface do usuário do constructor de segmento， é posível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser envirados para solucoes como Adobe Target， Adobe Campaign e Adobe Audience Manager para ativacao.

Agora voce precisa criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

建筑工程分段，装饰装饰物前的装饰物。 Voce pode contrados os Eventos de experiencia clicando no ícone **事件** na barra de menu **字段**.

![区段](./images/findee.png)

埃姆塞吉达，敬请上台 **XDM ExperienceEvents** 别太上流了。 小团体 **XDM ExperienceEvent**.

![区段](./images/see.png)

访问 **产品列表项**.

![区段](./images/plitems.png)

选择器 **名称** 我绝对要做个目标 **名称** 做菜单à esquerda na tela do constructor de segmentos na secao **事件**. Em seguida， o seguinte será exibido：

![区段](./images/eewebpdtlname.png)

用于比较的参数的装置 **等于** E，意大利安西拉没有坎波 **Real-time CDP**.

![区段](./images/pv.png)

Sempre que adicionar um elemento ao constructor de segmentos， voce pode clicar no botao **刷新估计** para obter uma nova estimativa da população em seu segmento.

![区段](./images/refreshest.png)

段落 **评估方法**，选择器 **Edge**.

![区段](./images/evedge.png)

我愿意，你愿意，愿意。

Como modelo de nomenclatura，使用：

- `seuSobrenome - Interest in Real-Time CDP`

塞吉达，小圈子 **保存并关闭** para salvar seu segmento.

![区段](./images/segmentname.png)

Agora voce irá retornar à página de visão geral do segmento， onde verá uma visualização de amostra dos perfis de clientes que se qualificam para o seu segmento.

![区段](./images/savedsegment.png)

Agora voce pode continuar no próximo exercício e usar seu segmento com o Adobe Target.

埃塔帕： [1.4 Açao：Adobe Target环境工作分类法](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
