---
title: 使用Workfront校对
description: 使用Workfront校对
kt: 5342
doc-type: tutorial
source-git-commit: 246bb91496104818f357848f41b79523b7771638
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 2.2.2 Workfront校对

## 2.2.2.1创建新的审批流程

转到[https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}。

单击9个点&#x200B;**汉堡包**&#x200B;图标并选择&#x200B;**校对**。

![WF](./images/wfp1.png)

转到&#x200B;**工作流**，单击&#x200B;**+新建**，然后选择&#x200B;**新建模板**。

![WF](./images/wfp2.png)

将&#x200B;**模板名称**&#x200B;设置为`--aepUserLdap-- - Approval Workflow`并将&#x200B;**模板所有者**&#x200B;设置为您自己。

![WF](./images/wfp3.png)

向下滚动，在&#x200B;**阶段** > **阶段1**&#x200B;下，添加&#x200B;**Wouter Van Galuwe**，其角色为&#x200B;**，审批者为**，审批者为&#x200B;**。**

单击&#x200B;**创建**。

![WF](./images/wfp4.png)

您的基本审批工作流现已准备就绪，可供使用。

![WF](./images/wfp5.png)

## 2.2.2.2创建新项目

从Workfront主页中，在&#x200B;**我的项目**&#x200B;选项卡中单击&#x200B;**新建**。 选择&#x200B;**空白项目**。

![WF](./images/wfp6.png)

您应该会看到此内容。 将名称更改为`--aepUserLdap-- - CitiSignal Fiber Launch`。

![WF](./images/wfp6a.png)

您的项目现已创建。

![WF](./images/wfp7.png)

## 2.2.2.3创建新任务

为您的任务输入此名称： **为Fiber营销活动创建资产**。 单击&#x200B;**创建任务**。

![WF](./images/wfp8.png)

您应该会看到此内容。

![WF](./images/wfp9.png)

## 2.2.2.4向Task添加新文档并完成批准流程

单击&#x200B;**+添加新**，然后选择&#x200B;**文档**。

![WF](./images/wfp10.png)

将[此文件](./images/2048x2048.png)下载到桌面。

![WF](./images/2048x2048.png){width="50px" align="left"}

选择文件&#x200B;**2048x2048.png**，然后单击&#x200B;**打开**。

![WF](./images/wfp12.png)

然后您应该拥有此项。 单击&#x200B;**创建验证**，然后选择&#x200B;**高级验证**。

![WF](./images/wfp13.png)

在&#x200B;**新验证**&#x200B;窗口中，选择您之前创建的工作流模板，该模板应命名为`--aepuserLdap-- - Approval Workflow`。 单击&#x200B;**创建校对**。

![WF](./images/wfp14.png)

然后你就可以回到你的任务中了。 单击&#x200B;**分配给**&#x200B;按钮并选择&#x200B;**分配给我**。

![WF](./images/wfp15.png)

单击&#x200B;**保存**。

![WF](./images/wfp16.png)

单击&#x200B;**处理它**。

![WF](./images/wfp17.png)

单击&#x200B;**打开校对**

![WF](./images/wfp18.png)

您现在可以查看证明。 选择&#x200B;**添加注释**&#x200B;以添加需要更改文档的注释。

![WF](./images/wfp19.png)

输入您的评论并单击&#x200B;**发布**。 单击&#x200B;**关闭**。

![WF](./images/wfp20.png)

接下来，您需要将您的角色从&#x200B;**审阅者**&#x200B;更改为&#x200B;**审阅者和批准者**。 为此，请返回任务并单击&#x200B;**校对工作流**。

![WF](./images/wfp21.png)

将您的角色从&#x200B;**审阅者**&#x200B;更改为&#x200B;**审阅者和批准者**。

![WF](./images/wfp22.png)

返回您的任务，然后再次打开验证。 您现在看到一个新按钮，**做出决定**。 单击它。

![WF](./images/wfp23.png)

选择&#x200B;**所需的更改**&#x200B;并单击&#x200B;**做出决定**。

![WF](./images/wfp24.png)

那你就该回到这里来。 现在，您需要上传第二个图像，该图像会考虑您提供的评论。

![WF](./images/wfp25.png)

将[此文件](./images/2048x2048_buynow.png)下载到桌面。

![此文件](./images/2048x2048_buynow.png){width="50px" align="left"}

在“任务”视图中，选择未批准的旧图像文件。 然后，单击“**+新增**”，选择“**版本**”，然后选择“**文档**”。

![WF](./images/wfp26.png)

选择文件&#x200B;**2048x2048_buynow.png**，然后单击&#x200B;**打开**。

![WF](./images/wfp27.png)

然后您应该拥有此项。 单击&#x200B;**创建验证**，然后再次选择&#x200B;**高级验证**。

![WF](./images/wfp28.png)

你会看到这个。 **工作流模板**&#x200B;现已预选，因为Workfront假定以前的审批工作流仍然有效。 单击&#x200B;**创建校对**。

![WF](./images/wfp29.png)

选择&#x200B;**打开校对**。

![WF](./images/wfp30.png)

现在，您可以在其旁边看到文件的2个版本。

![WF](./images/wfp31.png)

单击&#x200B;**做出决定**，选择&#x200B;**已批准**，然后单击&#x200B;**再次做出决定**。

![WF](./images/wfp32.png)

关闭验证预览。

![WF](./images/wfp33.png)

然后，您将带着批准的资源返回到“任务”视图。 现在，需要向AEM Assets共享此资源。

![WF](./images/wfp34.png)

单击&#x200B;**共享箭头**&#x200B;图标并选择您的应命名为`--aepUserLdap-- - Citi Signal AEM`的AEM Assets集成。

![WF](./images/wfp35.png)

双击您之前创建的文件夹，该文件夹应名为`--aepUserLdap-- - Workfront Assets`。

![WF](./images/wfp36.png)

单击&#x200B;**选择文件夹**。

![WF](./images/wfp37.png)

1-2分钟后，您的文档将发布到AEM Assets中。 您将在文档名称旁边看到AEM图标。

![WF](./images/wfp37a.png)

单击&#x200B;**打开摘要**。

![WF](./images/wfp38.png)

转到&#x200B;**元数据**，您应该会看到以下内容：

![WF](./images/wfp39.png)

转到&#x200B;**概述**&#x200B;并单击&#x200B;**+添加**&#x200B;添加说明。

![WF](./images/wfp40.png)

输入您的说明。 您的验证和文档设置现已完成。

![WF](./images/wfp41.png)

## 2.2.2.5在AEM Assets中查看文件

转到AEM Assets中名为`--aepUserLdap - Workfront Assets`的文件夹。

![WF](./images/wfppaem1.png)

单击图像下面的3个圆点，然后选择&#x200B;**详细信息**。

![WF](./images/wfppaem2.png)

然后，您将看到之前创建的元数据表单，其中值已由Workfront与AEM Assets之间的集成自动填充。

![WF](./images/wfppaem3.png)

[返回模块2.2](./workfront.md){target="_blank"}

[返回所有模块](./../../../overview.md){target="_blank"}
