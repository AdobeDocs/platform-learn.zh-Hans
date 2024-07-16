---
title: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics的Adobe Experience Platform数据集 — 巴西
description: Bootcamp -Customer Journey Analytics — 连接Customer Journey Analytics的Adobe Experience Platform数据集 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2连接数据集达Adobe Experience Platform无Customer Journey Analytics

## 目标

- Compreenda UI da conexao de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessore e a compilação de dados
- Aprenda o conceipt de streaming de dados no客户历程

## 4.2.1科内克索

访问[analytics.adobe.com](https://analytics.adobe.com) para acessar或Customer Journey Analytics。

Na página inicial doCustomer Journey Analytics，访问&#x200B;**连接**。

![演示](./images/cja2.png)

在CJA e a Plataforma中，Aqui voce pode ver todas作为区分的组合节日。 在Adobe Analytics的mesmo objetivo dos conjuntos de relatórios中，Essas的共管对象。 没关系，这可是完美差异的典范。 dados dados vem de datasets da Adobe Experience Platform.

我们只能用这种方法。 单击em **创建新连接**。

![演示](./images/cja4.png)

验证一个UI **创建连接** UI。

![演示](./images/cja5.png)

阿古拉·沃斯·波德·达尔·诺姆·阿苏阿·科内克索。

使用este modelo de nomenclatura： `yourLastName – Omnichannel Data Connection`。

示例： `vangeluw - Omnichannel Data Connection`

我们向沙箱和沙箱进行选择。 没有菜单沙盒，请选择一个seu沙盒，查询开发器`Bootcamp`。 Neste示例， o沙盒为&#x200B;**Bootcamp**&#x200B;的使用者。 **平均每日事件数**&#x200B;到&#x200B;**小于100万**。

![演示](./images/cjasb.png)

Após selecionar seu sandbox， voce pode comecar a adicionar datasets a esta conexao. 单击&#x200B;**添加数据集**。

![演示](./images/cjasb1.png)

## 4.2.2在Adobe Experience Platform中选择一个数据集

对数据集`Demo System - Event Dataset for Website (Global v1.1)`进行预览。 单击em **+**&#x200B;作为数据集的adicionar或esta conexao。

![演示](./images/cja7.png)

Agora pesquise e marque as caixas de selecao `Demo System - Event Dataset for Voice Assistants (Global v1.1)`和`Demo System - Event Dataset for Call Center (Global v1.1)`。

塞吉达，敬请光临。 单击&#x200B;**下一步**。

![演示](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID比索

要观察数据集的集锦。 Para cada数据集seleconado， voce verá um campo chamado **人员ID**。 Cada数据集tem seu próprio campo de ID de pessoa。

![演示](./images/cja11.png)

Comoo voce pode ver，一个可以自动进行选择的少年。 我是Adobe Experience Platform的首席律师。 Como示例， aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`， onde voce pode ver que o Identificador Primário está definido como `phoneNumber`。

![演示](./images/cja13.png)

没有entando，voce ainda pode influenciar qual identificator será usado para compilar datasets para sua conexao。 Voce pode usar qualquer identificator configurado no esquema vinculado ao seu dataset. 群集无菜单暂停para explorar os ID分配代码数据集。

![演示](./images/cja14.png)

Conforme mencionado， voce pode definir不同IDs de pessoa para cada数据集。 Isso permite reunir不同于CJA中的múltiplas数据集。 想象一下trazer NPS ou dados de pesquisa que seriam muito interessants e úteis para compredents o contexto motivo de um acontecimento。

不重要，不重要，不重要。 Digamos que temos `email` em数据集e `emailAddress` em外部数据集definido como ID da pessoa。 在campo ID da pessoa em ambos数据集上使用`delaigle@adobe.com` tiver o mesmo valor para o CJA poderá compilar os dados。

Autualmente，存在超出限制的算法，comportamento anonimo para conhecido. 以Perguntas Frequentes Aqui身份咨询： [常见问题解答](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html)。


### Compilando os dados usando o o ID da pessoa

Agora que voce compende o conceito de compilar datasets usando o ID da pessoa， vamos escolher `email` como ID da pessoa para cada dataset.

![演示](./images/cja15.png)

访问ID为pessoa的cada数据集参数。

![演示](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` na lista suspensa。

![演示](./images/cja17.png)

Depois de compilar os tres datasets， estamos prontos para continuous.

| 数据集 | 人员 ID |
| ----------------- |-------------| 
| 演示系统 — 网站的事件数据集(Global v1.1) | 电子邮件 |
| 演示系统 — 语音助手的事件数据集(Global v1.1) | 电子邮件 |
| 演示系统 — 呼叫中心的事件数据集(Global v1.1) | 电子邮件 |

Voce também precisa garantir que， para cada dataset， essas ocoes estejam habilitadas：

- Importar todos os novos dados
- Preencher操作现有DADOS
- Preencher tipo de fonte de dados com “其他”
- 准备用于消息名称和数据集的descrição com

单击&#x200B;**添加数据集**。

![演示](./images/cja16.png)

单击&#x200B;**保存** e vá para o próximo exercício。 Depois de criar sua **连接**， pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![演示](./images/cja20.png)

Próxima etapa： [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para fluxo de Usuário 4](./uc4.md)

[莫杜洛斯·托多斯·雷托纳尔](./../../overview.md)
