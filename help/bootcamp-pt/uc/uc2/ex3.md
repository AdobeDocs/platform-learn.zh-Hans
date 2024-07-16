---
title: Bootcamp - Journey Optimizer创建您的旅程和电子邮件 — 巴西
description: Bootcamp - Journey Optimizer创建您的旅程和电子邮件 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# 2.3 Crie sua jornada e mensagem de email

Neste exercício， voce irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstração.

Faca登录无Adobe Journey Optimizer访问[Adobe Experience Cloud](https://experience.adobe.com)。 单击&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **Home** no Journey Optimizer。 Primeiro，验证一下Sandbox Correto。 不要做沙盒来开发用户`Bootcamp`。 Para alternar de um sandbox para outtro，click em **Prod**&#x200B;选择沙盒类型。 Neste示例，**Bootcamp**&#x200B;中没有sandbox。 Voce estará na visualização da **Home**&#x200B;执行seu沙盒`Bootcamp`。

![ACOP](./images/acoptriglp.png)

## 2.3.1玉米酱

无菜单à esquerda，请单击em **历程**。 Em seguida，单击em **创建历程** para criar nova jornada。

![ACOP](./images/createjourney.png)

我们来看看吧。

![ACOP](./images/journeyempty.png)

前方没有练习，新录制了&#x200B;**活动**。 将事件`seuSobrenomeAccountCreationEvent`替换为`seuSobrenome` pelo seu sobrenome。 Este foi o resultado da criação do Evento：

![ACOP](./images/eventdone.png)

Agora voce deve consider este evento como o o início desta Jornada. Voce pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

选择seuo evento， arraste e solte o evento na tela de Jornada。 苏亚·乔纳达·阿古拉德夫的塞梅兰特·奥·塞甘特：

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada， voce deve adicionar uma etapa curta de **等待**。 Vá para o lado esquerdo da tela até a secao **编排** para contract isso。 你这身打扮得真不容易。

![ACOP](./images/journeywait.png)

苏亚·乔纳达·阿古拉·德韦塞梅兰特·奥·塞甘特。 没有lado direito da tela voce precisa configurar或tempo de espera。 Defina como 1分钟。 我心里想着如何改变你的心意。

![ACOP](./images/journeywait1.png)

单击em **确定** para salvar例如alteracoes。

Como terceira etapa da jornada， voce deve adicionar ação **电子邮件**。 Vá para o lado esquerdo da tela para **操作**，选择a acao **电子邮件** e arraste solte a acao no segundo nó da sua jornada。 我再说一遍。

![ACOP](./images/journeyactions.png)

定义&#x200B;**类别**&#x200B;组合&#x200B;**营销** e选择一个uma **电子邮件表面** que permita o envio de email。 Nesse caso，**电子邮件表面**&#x200B;用户选择电子邮件。 Certifique-se de que as caixas de seleção **电子邮件点击** e **电子邮件打开** estejam marcadas。

![ACOP](./images/journeyactions1.png)

这是门萨吉姆的秘密。 段落，单击&#x200B;**编辑内容**。

![ACOP](./images/journeyactions2.png)

## 2.3.2编写手册

段落模板sua mensagem，单击em **编辑内容**。

![ACOP](./images/journeyactions2.png)

再说吧。

![ACOP](./images/journeyactions3.png)

群集无campo de texto **主题行**。

![Journey Optimizer](./images/msg5.png)

Na área de texto， comece **奥拉**

![Journey Optimizer](./images/msg6.png)

我是个爱因达·娜奥·艾斯塔·普朗塔。 Em seguida， voce precisa trazer o token de personalização para o **名字** qestá armazenado em `profile.person.name.firstName`。 没有esquerda菜单，role para baixo para encontract或elemento **人员** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontre o elemento **全名** e clique na seta para visualizar mais campos。

![Journey Optimizer](./images/msg8.png)

Por fim，本地化campo **名字** e clique no símbolo **+** ao lado dele。 无论何时何地，您都可以享受无坎波de texto的个人化服务。

![Journey Optimizer](./images/msg9.png)

阿姆·塞吉达，**阿格拉德塞莫斯·阿苏亚内克里考！**&#x200B;的问题。单击&#x200B;**保存**。

![Journey Optimizer](./images/msg10.png)

恩陶，请回音。 单击em **向Designer发送电子邮件** para criar o conteúdo电子邮件。

![Journey Optimizer](./images/msg11.png)

Na próxima tela， será solicitado que voce forneca o conteúdo e email através de 3 métodos diferentes：

- **从头开始设计**： Comece com uma tela em branco e使用编辑器WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo email。
- **自己编写代码**： Crie seu próprio modelo de email codificando usandoHTML
- **导入HTML**：导入um modeloHTML存在，que voce poderá编辑。

单击&#x200B;**导入HTML**。

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**， que voce pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip)。 小集团汇入。

![Journey Optimizer](./images/msg13.png)

Voce verá este modelo de email padrao：

![Journey Optimizer](./images/msg14.png)

电子邮件的Vamos个性化。 Clique ao lado do texto **Olá** e， em seguida， clique no ícone **添加Personalization**。

![Journey Optimizer](./images/msg35.png)

Em seguida， voce precisa trazer o token de personalização **First name** que está armazenado em `profile.person.name.firstName`。 无菜单，本地化&#x200B;**人员**，faca uma busca detalhada no elemento **全名** e clique no ícone **+** para adicionar o campo **名字** ao编辑器。

单击&#x200B;**保存**。

![Journey Optimizer](./images/msg36.png)

Agora voce verá como campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

单击em **保存** para salvar sua mensagem。

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora voce得出以下结论： craacao do seu email de cadastro. 小团体没有上级的手法，以备不时之需。

![Journey Optimizer](./images/msg57.png)

单击&#x200B;**确定**。

![Journey Optimizer](./images/msg57a.png)

## 2.3.3苏丹共和国

我先问你说，你说，你说。 Voce pode fazer isso clicando no ícone **属性**&#x200B;没有上级direito da tela。

![ACOP](./images/journeyname.png)

Voce pode fazer isso clicando no item clicar no item &quot;Name&quot; e inserindo o seguinte name `yourLastName - Account Creation Journey`. 单击em **OK** para salvar as mudancas。

![ACOP](./images/journeyname1.png)

Agora voce pode publicar sua jornada clicando em **Publish**。

![ACOP](./images/publishjourney.png)

单击em **Publish** novamente。

![ACOP](./images/publish1.png)

我们向大家介绍一下我们的情况。

![ACOP](./images/published.png)

你可真够操心的。

Próxima etapa： [2.4 Teste sua jornada](./ex4.md)

[乌苏亚里奥二号酒庄酒庄酒庄酒庄酒庄酒庄](./uc2.md)

[莫杜洛斯·托多斯·雷托纳尔](../../overview.md)
