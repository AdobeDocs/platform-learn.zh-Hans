---
title: Bootcamp - Real-time CDP — 构建区段并采取行动 — 将您的区段发送到Adobe Target — 巴西
description: Bootcamp - Real-time CDP — 构建区段并采取行动 — 将您的区段发送到Adobe Target — 巴西
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 1.4 Açao：Adobe Target环境系统区段

访问[Adobe Experience Platform](https://experience.adobe.com/platform)。 德波伊斯·德·法泽尔登入后，我去Adobe Experience Platform的帕吉娜。

![数据获取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙盒**。 我做沙箱是你的精选。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙盒] dedicado。

![数据获取](./images/sb1.png)

## 1.4.1Adobe Target目标的SEU分段

O Adobe Target está disponível como um destino do CDP em tempo real. Para配置soa integracao com o Adobe Target，访问&#x200B;**目标** e **目录**。

单击em **Personalization**&#x200B;无菜单&#x200B;**类别**。 您可以&#x200B;**Adobe Target**。 单击&#x200B;**激活区段**。

![AT](./images/atdest1.png)

为目标``Bootcamp Target``选择群组&#x200B;**下一步**。

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis， selectione o segmento que voce criou em [1.3 Crie um segmento](./ex3.md)， com o nome `yourLastName - Interest in Real-Time CDP`。 Em seguida，单击em **下一步**。

![AT](./images/atdest8.png)

Na próxima página，单击&#x200B;**下一步**。

![AT](./images/atdest9.png)

单击&#x200B;**完成**。

![AT](./images/atdest10.png)

在Adobe Target的每一个角落。

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP， pode levar até uma hora para que o destino seja ativado. 我们来看看后端definicão da configuração是什么样子。 Depois que o tempo de espera inicial de 1 hora e a configuração do backend form concluídos， os segmentos de borda recém-adicionados que sao enviados ao destino do Adobe Target estarao disponíveis para segmentação em tempo real.

## 1.4.2在Adobe Target上配置sua atividade

阿古拉介绍Real-Time CDP的está configurado para ser enviado ao Adobe Target， é posssível configurar sua atividade de Segmentacao por experiencia no Adobe Target。 Neste excício， voce irá configurar uma atividade baseada no Visual Experience Composer.

访问página inicial da Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/)。 单击em **Target** para abrir。

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**， voce verá todas as a atividades existenes.
单击em **+创建活动** para criar uma nova atividade。

![RTCDP](./images/exclatov.png)

选择&#x200B;**体验定位**。

![RTCDP](./images/exclatcrxt.png)

选择一个&#x200B;**可视化** e定义&#x200B;**活动URL**&#x200B;组合`https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`、mas、antes disso、substitua XX por um número entre 01 e 60。

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisao de várias experiencias do Adobe Target. É possível escolher uma página da Web e包含一个URL访问：[https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html)。
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por示例， o参与方1 deve usar URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`， o参与方30 deve usar URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`。

选择工作区&#x200B;**AT Bootcamp**。

单击&#x200B;**下一步**。

![RTCDP](./images/exclatcrxtdtlform.png)

Agora没有可视化体验编辑器。 Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

Atualmente， o público padrao sao **所有访客**。 群组&#x200B;**3个点** ao lado de **所有访客**&#x200B;群组&#x200B;**更改受众**。

![RTCDP](./images/atform3.png)

Agora voce está vendo a lista de públicos disponíveis， e o segmento da Adobe Experience Platform que voce criou anteriormente e eviou ao Adobe Target agora faz parte dessa lista. 选择Segmento to que voce criou antheriormente na Adobe Experience Platform。 单击&#x200B;**分配受众**。

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiencia.

![RTCDP](./images/atform4.png)

Antes de alterar一个图像主体，voce deve clicar em **允许所有**&#x200B;没有横幅de cookie。

段落，vá para **浏览**

![RTCDP](./images/cook1.png)

Em seguida，单击em **允许全部**。

![RTCDP](./images/cook2.png)

Em seguida， retorne para **撰写**。

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. 单击na imagem主体padrao no site，单击em **替换内容** e选择一个&#x200B;**图像**。

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**。 选择单击&#x200B;**保存**。

![RTCDP](./images/atform6.png)

Voce verá a nova experiencia com a nova imagem para o seu Público selcionado

![RTCDP](./images/atform7.png)

这个小集团没有坦诚的上级。

![RTCDP](./images/exclatvecname.png)

Para o name，使用：

- `seuSobrenome - RTCDP - XT (VEC)`

单击&#x200B;**下一步**。

![RTCDP](./images/atform8.png)

单击&#x200B;**下一步**。

![RTCDP](./images/atform8a.png)

帕吉纳&#x200B;**目标和设置**，访问&#x200B;**目标量度**。

![RTCDP](./images/atform9.png)

定义元主体组合&#x200B;**参与** - **网站停留时间**。 单击&#x200B;**保存并关闭**。

![RTCDP](./images/vec3.png)

Agora voce está na página **活动概述**。 阿蒂维达德前卫。

![RTCDP](./images/atform10.png)

群集无Campo **未激活** e选择器&#x200B;**激活**。

![RTCDP](./images/atform11.png)

我们确认了我们的视觉体验。

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada站点没有启动营。

在此，您可以访问一个名为página do produto para **Real-Time CDP**&#x200B;的网站。 voce se qualificará instaneamente para o segmento que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real。

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisao de várias experiencias do Adobe Target. É possível escolher uma página da Web e包含一个URL acssando ao链接： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html)。
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por示例， o参与方1 deve使用`https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`， o参与方30 deve使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`。

![RTCDP](./images/atform12a.png)

Próxima etapa： [1.5 Acao： envie seu segmento para o Facebook](./ex5.md)

[乌苏亚里奥酒庄酒庄酒庄酒庄1号](./uc1.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
