---
title: Bootcamp - Journey Optimizer创建您的旅程和电子邮件 — 巴西
description: Bootcamp - Journey Optimizer创建您的旅程和电子邮件 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 3%

---

# 2.3 Crie sua jornada e mensagem de电子邮件

Neste exercício， voce irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstração.

Faca登录无Adobe Journey Optimizer访问权限 [Adobe Experience Cloud](https://experience.adobe.com). 小团体 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **主页**  没有Journey Optimizer。 Primeiro，验证一下Está对Sandbox Correto的评价。 我做沙盒也行 `Bootcamp`. Para alternar de um sandbox para outtro， clique em **Prod** 选择沙盒和沙盒。 Neste示例，不要做沙盒 **Bootcamp**. 达维斯达拉之家 **主页** 执行seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1朱尔纳达

没有菜单，小朋友们 **历程**. 塞吉达，小集团 **创建历程** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

我们来看看吧。

![ACOP](./images/journeyempty.png)

前方没有锻炼，前方没有锻炼 **事件**. Voce nomeou o evento `seuSobrenomeAccountCreationEvent` e替代 `seuSobrenome` 佩洛·塞乌·索布雷诺姆。 Este foi o resultado da criação do Evento：

![ACOP](./images/eventdone.png)

Agora voce deve考虑了este evento como o o início desta Jornada。 Voce pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

选择selecione seu evento， arraste e solte o evento na tela de Jornada。 Sua Jornada agora deve ser semelhante ao seguinte：

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada， voce deve adicionar uma etapa curta de **等待**. Vá para o lado esquerdo da tela até a secao **编排** para encontract isso. Voce usará atributos de perfil e precisará garantir que ejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

苏亚·乔纳达·阿古拉·德韦斯为塞梅尔汗特·奥·塞甘特效力。 没有lado direito da tela voce precisa configurar o tempo de espera。 Defina como 1分钟。 我敢说巴斯坦的节奏，违背了你的心愿。

![ACOP](./images/journeywait1.png)

小团体 **确定** 如变体。

Como terceira etapa da jornada， voce deve adicionar uma açao **电子邮件**. Vá para o lado esquerdo da tela para **操作**，选择a acao **电子邮件** 我绝对不会罢休。 我再说一遍。

![ACOP](./images/journeyactions.png)

定义a **类别** como **营销** e选择器uma **电子邮件表面** 电子邮件允许范围。 Nesse caso，a **电子邮件表面** 一个电邮选手。 作为凯哈斯·德·塞莱索的证书 **电子邮件的点击次数** e **电子邮件打开次数** 埃斯特贾姆·马尔卡达斯。

![ACOP](./images/journeyactions1.png)

这是门萨盖姆的戒指。 帕拉伊索，小集团 **编辑内容**.

![ACOP](./images/journeyactions2.png)

## 2.3.2基本概念

小团体，关于孟沙加姆的段子 **编辑内容**.

![ACOP](./images/journeyactions2.png)

再说一遍。

![ACOP](./images/journeyactions3.png)

小团体无坎波·德特克斯托 **主题行**.

![Journey Optimizer](./images/msg5.png)

我叫科米斯 **奥拉**

![Journey Optimizer](./images/msg6.png)

一个爱因达·娜欧·艾斯塔·普朗塔。 Em seguida， voce precisa trazer o token de personalização para **名字** 我是个阿玛泽纳多人 `profile.person.name.firstName`. 没有esquerda菜单，role para baixo para contract o elemento **人员** 我们为视觉化的mais campos建立社区

![Journey Optimizer](./images/msg7.png)

Agora entry o elemento **全名** 我们为那些视觉化的mais campos建立小团体。

![Journey Optimizer](./images/msg8.png)

Por fim，本地化到campo **名字** 无辛博罗集团 **+**  是拉多·德勒。 无论如何都不要用坎波·德特克斯托来表示个人化。

![Journey Optimizer](./images/msg9.png)

塞吉达，阿迪西奥和特克托， **阿格拉德塞莫斯是你的灵魂！**&#x200B;的问题。小团体 **保存**.

![Journey Optimizer](./images/msg10.png)

恩陶，听我说，我回过头来。 小团体 **电子邮件设计工具**  欢迎您发送电子邮件。

![Journey Optimizer](./images/msg11.png)

Na próxima tela， será solicitado que voce forneca o conteúdo do email através de 3 métodos diferentes：

- **从头开始设计**：Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estructura e os componentes de conteúdo para criar visualmente o conteúdo email.
- **自己编写代码**：Crie seu próprio modelo de email codificando usandoHTML
- **导入HTML**：汇入um modeloHTML存在，que voce poderá editar。

小团体 **导入HTML**.

![Journey Optimizer](./images/msg12.png)

阿拉斯特·索尔特·奥基沃 **mailtemplatebootcamp.html**，我叫沃斯·波德·拜克萨 [阿基](../../assets/html/mailtemplatebootcamp.html.zip). 小圈子是进口的。

![Journey Optimizer](./images/msg13.png)

Voce verá este modelo de email padrao：

![Journey Optimizer](./images/msg14.png)

电子邮件个性化设置。 小集团拉多多德克斯托 **奥拉** 埃姆·塞吉达，伊科内集团 **添加个性化**.

![Journey Optimizer](./images/msg35.png)

Em seguida， voce precisa trazer o token de personalização **名字** 我是个阿玛泽纳多人 `profile.person.name.firstName`. 无菜单，本地化元素 **人员**，法玛·布卡·德塔尔哈达没有元素 **全名** 没有伊科内的集团 **+** 露营的伴侣 **名字** ao编辑。

小团体 **保存**.

![Journey Optimizer](./images/msg36.png)

Agora voce verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

小团体 **保存** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo。

![Journey Optimizer](./images/msg56.png)

Agora voce得出以下结论： criação do seu email de cadastro. 小团体不能作为上级的陪审团。

![Journey Optimizer](./images/msg57.png)

小团体 **确定**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3若尔纳达公共

我们来做个前科吧。 沃斯·波德·法泽尔是克利坎多·诺伊科内 **属性** 没有上级的迪雷伊托·达·泰拉。

![ACOP](./images/journeyname.png)

Voce pode fazer isso clicando no item clicar no item &quot;Name&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. 小团体 **确定** para salvar as mudancas.

![ACOP](./images/journeyname1.png)

Agora voce pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

小团体 **Publish**  诺瓦门特。

![ACOP](./images/publish1.png)

西班牙公共事业部向游客提供咨询。

![ACOP](./images/published.png)

沃斯·特米努埃斯特·艾希西奥。

埃塔帕： [2.4乔尔纳达测验](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[莫杜洛斯·托多斯·托诺纳尔](../../overview.md)
