---
title: Bootcamp - Real-time CDP — 构建区段并采取行动 — 将区段发送到Adobe Target — 巴西
description: Bootcamp - Real-time CDP — 构建区段并采取行动 — 将区段发送到Adobe Target — 巴西
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 1.4 Açao：Adobe Target环境工作分类法

访问 [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer登录，voce irá访问página inicial da Adobe Experience Platform。

![数据获取](./images/home.png)

永恒的万年期，先有先兆 **沙盒**. 做沙箱也不行，我是布特坎普。 你这小嘴真不赖啊 **[!UICONTROL 生产产品]** 娜丽莎·阿苏尔·娜帕特·苏必利尔·达·泰拉。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙盒] 奉献精神。

![数据获取](./images/sb1.png)

## 1.4.1对Adobe Target的命运进行分段

O Adobe Target está disponível como um destino do CDP em tempo real. Para configurar sua integracao com o Adobe Target， acesse **目标** e **目录**.

小团体 **个性化** 无菜单 **类别**. 我们的目标 **Adobe Target**. 小团体 **激活区段**.

![在](./images/atdest1.png)

目标选择 ``Bootcamp Target`` 小集团 **下一个**.

![在](./images/atdest3.png)

区段选择区段划分 [1.3 Crie um段](./ex3.md)，com名称 `yourLastName - Interest in Real-Time CDP`. 塞吉达，小集团 **下一个**.

![在](./images/atdest8.png)

一个小集团，小集团 **下一个**.

![在](./images/atdest9.png)

小团体 **完成**.

![在](./images/atdest10.png)

在Adobe Target上吃甜点。

![在](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP， pode levar até uma hora para que o destino seja ativado. 我们来看看后端。 Depois que o tempo de espera inicial de 1 hora e a configuração do backend form concluídos， os segmentos de borda recém-adicionados que sao enviados ao destino do Adobe Target estarao disponíveis para segmentação em tempo real.

## 1.4.2配置sua atividade no Adobe Target

在Adobe Target上使用Real-Time CDP的配置，可以体验到Adobe Target的体验。 Neste exercício， voce irá configurar uma atividade baseada no Visual Experience Composer.

从Adobe Experience Cloud一手包办事 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 小团体 **Target** para abrir.

![RTCDP](./images/excl.png)

那个人就知道 **Adobe Target**，voce verá todas as atividades existes.
小团体 **+创建活动** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

选择器 **体验定位**.

![RTCDP](./images/exclatcrxt.png)

选择器 **可视化** 定义a **活动URL** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`，mas，antes disso，substitua XX por um numero entre 01 e 60。

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisao de várias experiencias do Adobe Target. É possível escolher uma página da Web e包含一个URL访问： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por示例，o参与1 deve usar URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`， o参与方30开发用户URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

工作区选择器 **AT Bootcamp**.

小团体 **下一个**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora voce没有可视化体验编辑器。 Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

圣帕德罗主教座堂阿图阿尔门特 **所有访客**. 小集团（未特指） **3个点** 奥拉多·德 **所有访客** 小团体 **更改受众**.

![RTCDP](./images/atform3.png)

Agora voce está vendo a lista de públicos disponíveis， e o segmento da Adobe Experience Platform que voce criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. 选择Segmento to que voce criou aniteriormente na Adobe Experience Platform。 小团体 **分配受众**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentacao por experiencia.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem主体，voce deve clicar em **全部允许** 无横幅de cookie。

Para isso， vá para **浏览**

![RTCDP](./images/cook1.png)

塞吉达，小集团 **全部允许**.

![RTCDP](./images/cook2.png)

Em seguida， retorne para **撰写**.

![RTCDP](./images/cook3.png)

Agora vamos mudar图示主要位于暗地里。 Clique na imagem principal padrao no site， clique em **替换内容** 选择器 **图像**.

![RTCDP](./images/atform5.png)

图片库 **rtcdp.png**. 选择群组 **保存**.

![RTCDP](./images/atform6.png)

Voce verá a nova experiencia com a nova imagem para o seu Público selectionado

![RTCDP](./images/atform7.png)

这个小集团没有上级的神职人员。

![RTCDP](./images/exclatvecname.png)

Para o nome，使用：

- `seuSobrenome - RTCDP - XT (VEC)`

小团体 **下一个**.

![RTCDP](./images/atform8.png)

小团体 **下一个**.

![RTCDP](./images/atform8a.png)

那帕吉纳 **目标和设置**，访问 **目标量度**.

![RTCDP](./images/atform9.png)

定义元主体组合 **参与** - **Time On Site**. 小团体 **保存并关闭**.

![RTCDP](./images/vec3.png)

阿古拉之家 **活动概述**. Voce ainda precisa activar sua Atividade.

![RTCDP](./images/atform10.png)

小团体无坎波 **不活动** 选择器 **激活**.

![RTCDP](./images/atform11.png)

Voce receberá uma confirmacau visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada网站不提供启动营。

Se agora voce voltar ao seu site de demonstracao e visitar a página do produto para **Real-Time CDP**，我们来验证一下voce se qualificará instantaneamente para o segmento que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real。

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisao de várias experiencias do Adobe Target. É possível escolher uma página da Web e包含一个URL访问链接： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por示例， o参与者1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`， o参与方30开发用户URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

埃塔帕： [1.5 Açao：Facebook环境工作分类法](./ex5.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
