---
title: Workfront快速入门
description: Workfront快速入门
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# 2.2.1 Workfront快速入门

登录到Adobe Workfront，方法是转到[https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}。

然后您会看到此内容。

![WF](./images/wfb1.png)

## 2.2.1.1配置您的AEM Assets集成

单击9个圆点&#x200B;**汉堡包**&#x200B;图标，然后选择&#x200B;**设置**。

![WF](./images/wfb2.png)

在左侧菜单中，向下滚动到&#x200B;**文档**，然后单击&#x200B;**Experience Manager Assets**。

![WF](./images/wfb3.png)

单击&#x200B;**+添加Experience Manager集成**。

![WF](./images/wfb4.png)

对于集成的名称，请使用`--aepUserLdap-- - Citi Signal AEM`。

打开&#x200B;**Experience Manager存储库**&#x200B;下拉列表并选择您的AEM CS实例，该实例的名称应为`--aepUserLdap-- - Citi Signal`。

![WF](./images/wfb5.png)

在&#x200B;**元数据**&#x200B;下，配置以下映射：

| Workfront字段 | Experience Manager Assets字段 |
| --------------- | ------------------------------ | 
| **文档** > **名称** | **wm：documentName** |
| **项目** > **描述** | **wm：projectDescription** |
| **任务** > **名称** | **wm：taskName** |
| **任务** > **描述** | **wm：taskDescription** |

为&#x200B;**同步对象元数据**&#x200B;启用开关。

单击&#x200B;**保存**。

![WF](./images/wfb6.png)

Workfront与AEM Assets CS之间的集成现已配置完成。

![WF](./images/wfb7.png)

## 2.2.1.2配置您的AEM Sites集成

>[!NOTE]
>
>此插件当前处于&#x200B;**早期访问**&#x200B;模式，尚未正式提供。
>
>该插件可能已安装在您使用的Workfront实例中。 如果已安装，您可以查看以下说明，但无需更改配置中的任何内容。

转到[https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}。

确保将此插件的&#x200B;**切换**&#x200B;设置为&#x200B;**已启用**。 然后，单击&#x200B;**齿轮**&#x200B;图标。

![WF](./images/wfb8.png)

您会看到&#x200B;**扩展配置**&#x200B;弹出窗口。 配置以下字段以使用此插件。

| 键 | 值 |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **生产** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;： true， &quot;publishUrl&quot;： true}&#39;** |

单击&#x200B;**保存**。

![WF](./images/wfb8.png)

返回您的Workfront UI，然后单击9个圆点&#x200B;**汉堡包**&#x200B;图标。 选择&#x200B;**设置**。

![WF](./images/wfb9.png)

在左侧菜单中，转到&#x200B;**自定义Forms**&#x200B;并选择&#x200B;**表单**。 单击&#x200B;**+新建自定义表单**。

![WF](./images/wfb10.png)

选择&#x200B;**任务**&#x200B;并单击&#x200B;**继续**。

![WF](./images/wfb11.png)

然后，您将看到空的自定义表单。 输入表单名称`Content Fragment & Integration ID`。

![WF](./images/wfb12.png)

将新的&#x200B;**单行文本**&#x200B;字段拖放到画布上。

![WF](./images/wfb13.png)

配置新字段，如下所示：

- **标签**： **内容片段**
- **名称**： **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

将新的&#x200B;**单行文本**&#x200B;字段添加到画布上，并配置新字段，如下所示：

- **标签**： **集成ID**
- **名称**： **`aem_workfront_integration_id`**

单击&#x200B;**应用**。

![WF](./images/wfb15.png)

您现在需要配置第二个自定义表单。 单击&#x200B;**+新建自定义表单**。

![WF](./images/wfb10.png)

选择&#x200B;**任务**&#x200B;并单击&#x200B;**继续**。

![WF](./images/wfb11.png)

然后，您将看到空的自定义表单。 输入表单名称`Preview & Publish URL`。

![WF](./images/wfb16.png)

将新的&#x200B;**单行文本**&#x200B;字段拖放到画布上。

![WF](./images/wfb17.png)

配置新字段，如下所示：

- **标签**： **预览URL**
- **名称**： **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

将新的&#x200B;**单行文本**&#x200B;字段添加到画布上，并配置新字段，如下所示：

- **标签**： **Publish URL**
- **名称**： **`aem_workfront_integration_publish_url`**

单击&#x200B;**应用**。

![WF](./images/wfb19.png)

然后，您应该有2个可用的自定义表单。

![WF](./images/wfb20.png)

[返回模块2.2](./workfront.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
