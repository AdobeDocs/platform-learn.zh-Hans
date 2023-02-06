---
title: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics中的Adobe Experience Platform数据集 — 巴西
description: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics中的Adobe Experience Platform数据集 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 2%

---

# 4.2连接数据集da Adobe Experience Platform无Customer Journey Analytics

## 奥别蒂沃斯

- 全面的UI da conexão de dados
- 《Adobe Experience Platform行动》
- 了解ID da pessoa e compilação de dados
- Aprenda o conceito de streaming de dados no Customer历程

## 4.2.1科内桑

阿塞斯 [analytics.adobe.com](https://analytics.adobe.com) Customer Journey Analytics。

我们的Customer Journey Analytics **连接**.

![演示](./images/cja2.png)

Aqui você ver todas as diferentes conexões feitas entre o CJA e a Plataforma. Essas conexöes têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics。 不能做，不能做完。 Todos os dados vêm de da Adobe Experience Platform。

来吧，来吧。 团 **创建新连接**.

![演示](./images/cja4.png)

Você verá a UI **创建连接** UI。

![演示](./images/cja5.png)

Agora você pode dar nome à conexão.

使用este modelo de nomenclataura: `yourLastName – Omnichannel Data Connection`.

样本： `vangeluw - Omnichannel Data Connection`

Você também会选择沙盒或沙盒。 无菜单沙盒，选择一个安全沙盒，请求 `Bootcamp`. 不是样本，就是沙盒 **Bootcamp**. 我的女人 **平均每日事件数** to **不到100万**.

![演示](./images/cjasb.png)

Após selecionar seu沙盒、 você pode começar a adicionar数据集a esta conexão。 团 **添加数据集**.

![演示](./images/cjasb1.png)

## 4.2.2选择数据集da Adobe Experience Platform

数据集问题 `Demo System - Event Dataset for Website (Global v1.1)`. 团 **+** para adicionar o dataset a esta conexão

![演示](./images/cja7.png)

塞莱桑的圣女 `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

她的话，我就是个空话。 团 **下一个**.

![演示](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O objetivo agora e juntar处理数据集。 Para cada数据集selectionado， você verá um campo chamado **人员ID**. Cada数据集tem seu próprio campo de ID de pessoa。

![演示](./images/cja11.png)

Como voê pode ver， a maioria detem o ID da pessoa selecionado automaticamente. Isso ocorre porque mum identification ador princialéé selecionado em cada esquema na Adobe Experience Platform。 象科莫一样，我是个好人 `Demo System - Event Schema for Call Center (Global v1.1)`在Primário está definitido como身份识别员身份识别上 `phoneNumber`.

![演示](./images/cja13.png)

没有entanto， você ainda pode influeciar qual identifiador será usado para compilar datas para sua conexão。 Você pode usar qualquer identification ador configurado no esquema vinculado seu数据集。 Cligue无菜单暂停搜索ID的搜索ID和AEM CAD数据集。

![演示](./images/cja14.png)

Conforme mencionado、você pode定义不同的ID， de pessoa para cada数据集。 Isso permite引用CJA上的múltiplas origens数据集。 想象一下NPS在达多斯·德·佩斯奎萨·克·塞里亚姆·米托的故事中，你想的是，你想想想想想想想想想想想想想想想想想想想想想想想想想想想想想，想想想想想想想想想想想就想想想想想想想想想想想，想想想想想想想想想想想想想，想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想就想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想想

O nome do campo ID da pessoa não e importante， desque o valor nos campos ID da pessoa对应。 迪加莫斯的特莫斯 `email` em um数据集 `emailAddress` em outro数据集定义como ID da pessoa。 Se `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa em ambos os数据集， o CJA poderá compilar os dados。

Atualmente，现有algumas outras limitações， compilar o comportamento anônimo para conhecido。 参考perguntas频度： [常见问题解答](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hans).


### 编辑ID da pessoa

Agora que vocke do conceinde o concei to de compilar dataset usando o ID da pessoa， vamos escolher `email` como ID da pessoa para cada数据集。

![演示](./images/cja15.png)

Acesse cada数据集para autalizar o ID da pessoa。

![演示](./images/cja12a.png)

阿戈拉·普林查·坎波ID达佩索阿·埃斯科伦多 `email` 不行。

![演示](./images/cja17.png)

Depois de compilar os três数据集， esamos prontos para continuar。

| 数据集 | 人员 ID |
| ----------------- |-------------| 
| 演示系统 — 网站事件数据集（全局v1.1） | 电子邮件 |
| 演示系统 — 语音助理事件数据集（全局v1.1） | 电子邮件 |
| 演示系统 — 呼叫中心事件数据集（全局v1.1） | 电子邮件 |

Você também precisa garantir que， para cada数据集， essa opções estejam habilitadas:

- 重要的todos os novos dados
- Preencher todos os dados存在者

团 **添加数据集**.

![演示](./images/cja16.png)

团 **保存** e vá para o próximo excreício. Depois de criar sua **连接**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![演示](./images/cja20.png)

埃塔帕： [4.3 《达多斯可视化图表》](./ex3.md)

[Retornar para Fluxo de Uuário 4](./uc4.md)

[托多斯 — 莫杜洛斯](./../../overview.md)
