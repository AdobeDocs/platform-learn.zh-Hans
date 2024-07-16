---
title: Bootcamp -Customer Journey Analytics — 从见解到行动 — 巴西
description: Bootcamp -Customer Journey Analytics — 从见解到行动 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 4.6 Dos insights à acao

## 目标

- Entenda como criar um público com base em uma visao coletada无Customer Journey Analytics
- 使用esse público no CDP em tempo real no Adobe Journey Optimizer

## 4.6.1 Crie uma audiencia e publish-a

Em seu projeto， voce criou um filtro chamado **呼叫感情** e conseguiu visualizar a quantidade de usuários que tiveram suas ligacoes ao call center classificadas como **positivas**。 阿戈拉，voce poderá criar um segmento com essuários e ativacao-los em jornadas ou em canais de comunicacao.

O primeiro passo é： No painel criado no último exercício，选择a linha **1。 通话感觉 — 积极的**，点击鼠标选择一个opcao **从所选内容创建受众**：

![演示](./images/aud1.png)

Em seguida， de um nome para a sua audiencia seguindo o modelo **yourLastName - cia受众通话感觉良好**：

![演示](./images/aud2.png)

关于如何预览está sendo criada的注释：

![演示](./images/aud3.png)

部分最终化，群集&#x200B;**Publicar**：

![演示](./images/aud4.png)

## 4.6.2使用sua audiencia como parte de um segmento

Voltando para Adobe Experience Platform， vá em **区段>浏览**&#x200B;浏览会议可视化图表或查看区段无CJA打印到调度程序区段用户访问区段！

![演示](./images/aud5.png)

阿古拉之家用户区段我们的用户无Facebook之家用户！

## 4.6.3使用seu segmento na Real-Time CDP em tempo real

Na Adobe Experience Platform， vah em **区段>浏览** e encontre a audience que voce criou no CJA：

![演示](./images/aud6.png)

单击无seu段，单击em seguida，单击em **激活到目标**：

![演示](./images/aud7.png)

选择目标chamada bootcamp-facebook e， em seguida， clique em下一步：

![演示](./images/aud8.png)

Em seguida， clicue em Next novamente：

![演示](./images/aud9.png)

选择opcao **受众来源** e defina como **直接来自客户** e clique em下一步：

![演示](./images/aud10.png)

Por fim， na página **审阅** clique em完成！

![演示](./images/aud11.png)

普朗托！ 我们来看看这个Facebook的。
阿戈拉，vamos utilizar esse segmento no AJO！

## 4.6.4使用seu segmento no Adobe Journey Optimizer

一个接口da Adobe Experience Platform clique em Journey Optimizer e， em seguida，无菜单横向快捷键，clique em **历程** e comece a criar uma jornada clicando em **创建历程**：

![演示](./images/aud20.png)

![演示](./images/aud21.png)

![演示](./images/aud22.png)

Em seguida，无菜单横向电子报价单，em Eventos，选择&#x200B;**区段资格** e arraste-o até a jornada：

![演示](./images/aud23.png)

Em seguida， em **区段** clique em **编辑** para selececonar um区段：

![演示](./images/aud24.png)

选择一位受众来访问CJA e clique em **保存**：

![演示](./images/aud25.png)

普朗托！ 一个临时pode criar uma jornada para clientes que se alificam para esse segmento！

[返回用户流程4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
