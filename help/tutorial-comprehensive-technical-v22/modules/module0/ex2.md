---
title: 快速入门 — 使用设置Launch资产旁边的演示系统
description: 快速入门 — 使用设置Launch资产旁边的演示系统
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 9c0eddf5-bfd7-4e7a-a8e2-ccd55ccd966d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 0.2使用“演示系统”旁边的“设置Adobe Experience Platform数据收集客户端属性”

注册Adobe Experience Platform的全面技术教程后，会有一个自动化的过程，通过该过程，您可以访问演示系统，以便能够访问和运行以下配置。

获得演示系统的访问权限后，请继续执行以下步骤。

转到 [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/). 选择您的沙盒并单击 **快速设置**.

![DSN](./images/dsnh1.png)

您将看到：

![DSN](./images/dsnhome.png)

在 **常规** - **环境**，选择您的Adobe Experience Platform实例和沙盒，在本例中为：

- **Experience Platform国际**
- **aepenablementfy22**
- 配置：请选择 **全局v2.0**

![DSN](./images/dsn1.png)

接下来，选择预设 **启用用户** 单击 **开始**.

![DSN](./images/dsn2.png)

在弹出窗口中，输入数据收集属性的名称。 请使用此命名约定： **演示系统(DD/MM/YYYY)**. 答：您的LDAP将自动附加，您无需自行添加。

单击&#x200B;**开始**。

![DSN](./images/dsn3.png)

然后，您将看到此弹出窗口，其中显示了创建网站和移动设备应用程序项目以及数据收集属性时的进度。

![DSN](./images/dsn4.png)

快速设置过程完成后，您将拥有：

- 1个Web Retail项目，通过该项目，可以将演示网站与Luma演示品牌结合使用
- 1个移动零售项目，该项目允许将演示移动应用程序与Luma演示品牌结合使用
- 1个CX App Retail项目，使用呼叫中心和客服应用程序与Luma演示品牌成为可能
- 1 Web数据收集属性，用于从网站收集数据
- 1用于移动设备的数据收集属性，用于从移动设备应用程序收集数据

![DSN](./images/dsn5.png)

在后续步骤中，根据需要保持此屏幕处于打开状态。

下一步： [0.3创建数据流](./ex3.md)

[返回模块0](./getting-started.md)

[返回到所有模块](./../../overview.md)
