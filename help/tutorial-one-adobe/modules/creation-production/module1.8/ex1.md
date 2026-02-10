---
title: Workfront、Frame.io和ESM快速入门
description: Workfront、Frame.io和ESM快速入门
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2f9a3eef-16ef-497c-97f7-377ff9ed2f82
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# 1.8.1 Workfront、Frame.io和ESM快速入门

## 1.8.1.1 Workfront工作流术语

以下是主要的Workfront对象和概念：

| 名称 | 上次更新 |
| ---------------------- | ------------ | 
| 组合 | 具有统一特性的项目集合。 这些项目通常会争夺相同的资源、预算或时限。 |
| 项目 | 项目组合中的子集，可将相似的项目组合在一起，以实现明确定义的收益。 |
| 项目 | 必须在特定时间框架内完成的大量工作，且必须使用特定预算和特定资源数量。 为了使项目易于管理，您可以将项目划分为一系列任务。 完成所有任务即完成项目。 |
| 项目模板 | 您可以使用项目模板捕获与组织中项目关联的大多数可重复流程、信息和设置。 创建模板后，您可以将其附加到现有项目，或者使用它们构建新项目。 |
| 任务 | 作为实现最终目标（完成项目）的步骤而必须执行的活动。 任务永远不可能独立存在。 它们始终是项目的一部分。 |
| 指定任务 | 分配给问题或任务的用户、工作角色或团队。 项目、项目组合或项目群不能具有分配。 |
| 文档/版本 | 附加到Workfront中对象的任何文件。 每次将同一文档上载到同一对象时，都会为其分配一个版本号。 用户可以查看和更改文档早期版本的多个选项。 |
| 审批 | 给定工作项，如任务、文档或时间表，可能要求主管或其他用户签发该工作项。 此注销过程称为批准。 |


转到[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 单击以打开&#x200B;**Workfront**。

![Workfront计划](./images/wfpl1.png)

你会看到这个。

![WF](./images/wfb1.png)

## 1.8.1.2启用Workfront Blueprint

在下一步中，您将使用模板创建新项目。 Adobe Workfront提供了许多只需激活即可使用的蓝图。

对于CitiSignal的使用案例，您需要使用&#x200B;**集成营销活动执行**&#x200B;蓝图。

要安装该Blueprint，请打开菜单并选择&#x200B;**Blueprint**。

![WF](./images/blueprint1.png)

选择过滤器&#x200B;**Marketing**，然后向下滚动以查找Blueprint **集成营销活动执行**。 单击&#x200B;**安装**。

![WF](./images/blueprint2.png)

单击&#x200B;**继续**。

![WF](./images/blueprint3.png)

将&#x200B;**项目模板名称**&#x200B;更改为`--aepUserLdap-- - Integrated Campaign Execution`。

单击&#x200B;**安装Blueprint**。

![WF](./images/blueprint4.png)

几分钟后，将安装Blueprint。

![WF](./images/blueprint6.png)

## 1.8.1.3创建新项目

打开&#x200B;**菜单**&#x200B;并转到&#x200B;**Porftolios**。

![WF](./images/wfp6a.png)

单击&#x200B;**+新建Portfolio**。

![WF](./images/wfpfolio1.png)

输入项目组合名称`--aepUserLdap-- - CitiSignal`。

![WF](./images/wfpfolio2.png)

转到&#x200B;**程序**&#x200B;并单击&#x200B;**+新建程序**。 选择&#x200B;**新程序**。

![WF](./images/wfnp1.png)

输入项目名称： `--aepUserLdap-- - CitiSignal Fiber Launch`。

![WF](./images/wfp6b.png)

在您的项目中，转到&#x200B;**项目**。 单击&#x200B;**+新建项目**，然后选择&#x200B;**从模板新建项目**。

![WF](./images/wfp6.png)

选择模板`--aepUserLdap-- - Integrated Campaign Execution`并单击&#x200B;**使用模板**。

![WF](./images/wfp6g.png)

您应该会看到此内容。 将名称更改为`--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026`并单击&#x200B;**创建项目**。

![WF](./images/wfp6c.png)

您的项目现已创建。 转到&#x200B;**项目详细信息**。

![WF](./images/wfp6h.png)

转到&#x200B;**项目详细信息**。 单击以选择&#x200B;**描述**&#x200B;下的当前文本。

将描述设置为`The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

单击&#x200B;**保存更改**。

![WF](./images/wfp6e.png)

您的项目现已准备就绪，可供使用。

![WF](./images/wfp7.png)

项目中的任务和依赖项是根据您选择的模板创建的，并且您已被设置为。 项目的所有者。 项目的状态已设置为&#x200B;**计划**。 您可以通过选择列表中的其他值来更改项目的状态。

![WF](./images/wfp7z.png)

## Frame.io中的1.8.1.4项目视图

转到[https://next.frame.io/](https://next.frame.io/){target="_blank"}。 登录并选择要使用的实例，在此示例中&#x200B;**Experience Platform International ESM**。 您会注意到Frame.io中已存在您刚刚创建的项目的文件夹。 该文件夹以您之前输入的项目名称命名。

这是Enterprise Storage Management的一项功能，它是一种基于云的存储解决方案，可作为Adobe企业产品(包括Workfront和Frame.io)中资产的中央存储库。

Adobe企业存储的主要优势包括：

- 用于创意和工作管理资产的统一存储层
- 通过Adobe Identity Management system (IMS)集中管理权限以实现安全访问控制
- 跨Workfront和Frame.io的端到端资源可见性
- 满足企业需求的可扩展存储和配额管理

![WF](./images/fio1.png)

## 1.8.1.5创建新任务

快回到Workfront。 转到&#x200B;**任务**，将鼠标悬停在任务&#x200B;**开始创建设计模板**&#x200B;上，然后单击3个点&#x200B;**...**。

![WF](./images/wfp7a.png)

选择选项&#x200B;**在下方插入任务**。

![WF](./images/wfp7x.png)

为您的任务输入此名称： `Create layout using approved assets and copy`。

将字段&#x200B;**工作**&#x200B;设置为角色&#x200B;**Designer**。
将字段&#x200B;**持续时间**&#x200B;设置为&#x200B;**5天**。
将字段前置任务设置为&#x200B;**9**。
为&#x200B;**开始日期**&#x200B;和&#x200B;**到期日期**&#x200B;字段输入日期（此任务的开始日期应安排在上一个任务的结束日期之后）。

单击屏幕中的其他位置以保存新任务。

![WF](./images/wfp8.png)

您应该会看到此内容。 单击任务以将其打开。

![WF](./images/wfp9.png)

转到&#x200B;**任务详细信息**&#x200B;并将字段&#x200B;**描述**&#x200B;设置为： `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

单击&#x200B;**保存更改**。

![WF](./images/wfp9a.png)

您应该会看到此内容。 单击&#x200B;**分配**&#x200B;字段并选择&#x200B;**分配给我**。

![WF](./images/wfpwlb7.png)

单击&#x200B;**保存**。

![WF](./images/wfpwlb8.png)

单击&#x200B;**处理它**。

![WF](./images/wfpwlb9.png)

您应该会看到此内容。

![WF](./images/wfpwlb10.png)

作为此任务的一部分，需要创建新资源。 在下一步中，首先您要在Workfront中提供参考图像，以便设计人员知道需要什么。 然后，您将更改为Designer的角色，并使用Adobe Express自行创建该资源。

## 1.8.1.6上传参考图像

将参考图像[此处](./assets/reference_images.zip)下载到您的桌面并解压缩。

![WF](./images/wfrefimg1.png)

在Workfront中，导航到&#x200B;**项目**&#x200B;级别。

![WF](./images/wfrefimg2.png)

转到&#x200B;**文档**，单击&#x200B;**+添加新**，然后选择&#x200B;**文档**。

![WF](./images/wfrefimg3.png)

导航到您下载的包含参考图像的文件夹。 选择所有图像并单击&#x200B;**打开**。

![WF](./images/wfrefimg4.png)

几分钟后，所有图像都将上传并附加到项目。

![WF](./images/wfrefimg5.png)

设置好参考图像后，设计人员现在即可为此营销活动创建新资源。

## 后续步骤

下一步：[创建新资源并审阅和批准它](./ex2.md){target="_blank"}

返回[使用Workfront、Frame.io和企业存储管理进行统一审查和批准](./esm.md){target="_blank"}

返回[所有模块](./../../../overview.md){target="_blank"}
