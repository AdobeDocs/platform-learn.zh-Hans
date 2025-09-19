---
title: 将ACCS连接到AEM Assets CS
description: 将ACCS连接到AEM Assets CS
kt: 5342
doc-type: tutorial
source-git-commit: 16229700449660a085549a37013e015a5e20ba9e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 1.5.3将ACCS连接到AEM Assets CS

>[!IMPORTANT]
>
>要完成此练习，您需要有权访问有效的AEM Sites和具有EDS环境的Assets CS 。
>
>如果您还没有这样的环境，请转到练习[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照上面的说明进行操作，您将有权访问此类环境。

>[!IMPORTANT]
>
>如果您之前已使用AEM Sites和AEM CS环境配置了Assets CS项目，则可能是您的AEM CS沙盒已休眠。 鉴于解除此类沙盒的休眠需要10-15分钟，最好现在就启动解除休眠过程，这样以后就不必等待它。

![ACCS+AEM Assets](./images/accsaemassets1.png)


## 1.5.3.4更新config.json

在第6 `"ac-environment-id":XXX`行下添加以下代码片段：

```json
 "commerce-assets-enabled": "true",
```



下一步：[摘要和优点](./summary.md){target="_blank"}

返回[Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
