---
title: Bootcamp — 实时CDP — 构建区段并采取操作 — 将您的区段发送到Adobe Target — 巴西
description: Bootcamp — 实时CDP — 构建区段并采取操作 — 将您的区段发送到Adobe Target — 巴西
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 1.4阿桑：恩维埃·塞门托·帕拉·Adobe Target

阿塞斯 [Adobe Experience Platform](https://experience.adobe.com/platform). 登录后，我会在Adobe Experience Platform。

![数据获取](./images/home.png)

连续性，职业是选择者 **沙盒**. 没人会跟一个选手做沙箱。 É posível fazer isso clicando no texto **[!UICONTROL 生产产品]** na linha azul na parte superior da tela。 在沙箱里自行选择 [!UICONTROL 沙盒] 专门的。

![数据获取](./images/sb1.png)

## 1.4.1 《Adobe Target》

Adobe Target，我们的节奏真实。 Para configurar sua integração com o Adobe Target, acesse **目标** e **目录**.

团 **个性化** 无菜单 **类别**. 卡唐·德斯蒂诺 **Adobe Target**. 团 **激活区段**.

![AT](./images/atdest1.png)

选择目标 ``Bootcamp Target`` e集团 **下一个**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis，selecione o segmento que criem [1.3 Crie um segmento](./ex3.md),com o nome `yourLastName - Interest in Real-Time CDP`. 阿姆·塞吉达，小团 **下一个**.

![AT](./images/atdest8.png)

小朋友 **下一个**.

![AT](./images/atdest9.png)

团 **完成**.

![AT](./images/atdest10.png)

她是Adobe Target。

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até mu hora para que o destino seja ativado。 Este e mpo de esperaúnico devido à definição da configuração de back-end. Depois que o tempo de espera initial de 1 hora e a configuração do back-end forem gentidos， os segmentos de borda recém-adicionados que são enviados destino do Adobe Target estarão disponíveis para segmentação tempo real。

## 1.4.2配置sua atividade baseada em formulario do Adobe Target

Agora que seu segmento Real-Time CDP está configurado para enviado ao Adobe Target,é posível configurar sua atividade de Segmentação por experincia no Adobe Target。 Neste expericio， você irá configurar uma atividade baseada no Visual Experience Composer。

我是Adobe Experience Cloud人 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 团 **Target** 帕拉·阿卜里尔。

![RTCDP](./images/excl.png)

在 **Adobe Target** 主页，您将看到所有现有活动。
单击 **+创建活动** 创建新活动。
真正的 **Adobe Target**无言无语的存在。
团 **+创建活动** 新阿提维达德。

![RTCDP](./images/exclatov.png)

选择项 **体验定位**.

![RTCDP](./images/exclatcrxt.png)

选择项 **可视** e定义a **活动URL** 科科 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`在01e30中替代XXpor umreo entre 01e30。

>[!IMPORTANT]
>
>Cada参与者：da capaciação deve usar uma página da Web separada para evitar a colisão de várias experincias do Adobe Target。 É postível escolher uma página da Web发布了一个URL帐户： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por smadeo， o participante 1 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，参与者30使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

选择工作区 **AT Bootcamp**.

团 **下一个**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer（Agora você está不能使用可视化体验编辑器）。 20 Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

阿图尔门特，圣普布利科教区 **所有访客**. 团 **3点** 奥拉多德 **所有访客** e团 **更改受众**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis， e o segmento da Adobe Experience Platform qu e você criou anteriormente e enviou a Adobe Target agora faz parte dessa lista。 选择一段时间，我们要在Adobe Experience Platform。 团 **分配受众**.

![RTCDP](./images/exclatvecchaud.png)

塞格门托·达Adobe Experience Platform·阿戈拉·帕特·德萨·阿提维达德·德·塞格门塔桑·波尔·恩比西亚。

![RTCDP](./images/atform4.png)

一位神像主管，那位主管 **允许全部** 无Cookie横幅。

Para isso， vá para **浏览**

![RTCDP](./images/cook1.png)

阿姆·塞吉达，小团 **允许全部**.

![RTCDP](./images/cook2.png)

Em seguida， rethern para **撰写**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal initial do site. Cligue na imagem principal padrão no site， cligue em **替换内容** e selecione **图像**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. 选择一个e团 **保存**.

![RTCDP](./images/atform6.png)

Você verá a nova experiencia com a nova imagem para o seu Público selecionado

![RTCDP](./images/atform7.png)

Cligue no título da sua atividade no canto superesquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

段，使用：

- `yourLastName - RTCDP - XT (VEC)`

团 **下一个**.

![RTCDP](./images/atform8.png)

团 **下一个**.

![RTCDP](./images/atform8a.png)

帕金娜 **目标和设置**, acesse **目标量度**.

![RTCDP](./images/atform9.png)

定义元主体como **参与度** - **网站逗留时间**. 团 **保存并关闭**.

![RTCDP](./images/vec3.png)

阿戈拉·沃克斯塔娜·帕吉娜 **活动概述**. 维奇·安达是阿提瓦·苏阿·阿提维达德的前身。

![RTCDP](./images/atform10.png)

坎波团 **不活动** e selecione **激活**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visua sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada，站点do bootcamp。

Se agora você voltar ao seu site de dedoção e visitar a página do produto para **Real-Time CDP**, você se qualificará instaneamente para o segmento qu criou e verá a aatividade do Adobe Target exibida na página intifial im tempo real。

>[!IMPORTANT]
>
>Cada参与者：da capaciação deve usar uma página da Web separada para evitar a colisão de várias experincias do Adobe Target。 É postível escolher uma página da Web会提供一个URL acessando ao链接： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por smadeo， o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，参与者30使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

埃塔帕： [1.5采取行动：将区段发送到Facebook](./ex5.md)

[乌萨里奥1号河畔](./uc1.md)

[托多斯 — 莫杜洛斯](../../overview.md)
