---
title: 创建编排的营销活动
description: 创建编排的营销活动
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 53be5cf34db144e346f9810359b583072743382f
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---

# 3.8.2创建编排的营销活动

## 3.8.2.1创建您的编排活动

转到&#x200B;**营销活动**。 单击&#x200B;**创建营销活动**。

![AJO OC](./images/ajooc1.png)

选择&#x200B;**业务流程 — 营销**，然后单击&#x200B;**确认**。

![AJO OC](./images/ajooc2.png)

输入营销活动名称： `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign`，然后单击&#x200B;**保存**。

![AJO OC](./images/ajooc3.png)

您应该会看到此内容。 单击&#x200B;**+**&#x200B;图标。

![AJO OC](./images/ajooc4.png)

选择&#x200B;**分支**。

![AJO OC](./images/ajooc5.png)

### 构建受众1

单击&#x200B;**+**&#x200B;图标，然后选择&#x200B;**生成受众**。

![AJO OC](./images/ajooc6.png)

单击以打开&#x200B;**定向维度**&#x200B;的文件夹。

![AJO OC](./images/ajooc7.png)

选择&#x200B;**`--aepUserLdap--_citisignal_recipients`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc8.png)

单击&#x200B;**创建受众**。

![AJO OC](./images/ajooc9.png)

单击&#x200B;**添加条件**。

![AJO OC](./images/ajooc10.png)

选择&#x200B;**recipient_type**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc11.png)

在&#x200B;**`account_holder`**&#x200B;值&#x200B;**字段中输入**&#x200B;并单击&#x200B;**计算**。

![AJO OC](./images/ajooc12.png)

然后，您应该会看到&#x200B;**定向的用户档案**&#x200B;的数字。 单击灰色区域中的某个位置，如所示。

![AJO OC](./images/ajooc13.png)

单击&#x200B;**添加条件**。

![AJO OC](./images/ajooc14.png)

深入到&#x200B;**`citisignal_accounts`**。

![AJO OC](./images/ajooc15.png)

选择&#x200B;**`account_status`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc16.png)

在&#x200B;**`active`**&#x200B;值&#x200B;**字段中输入**。 然后，按指示单击灰色区域中的某个位置。

![AJO OC](./images/ajooc17.png)

单击&#x200B;**添加条件**。

![AJO OC](./images/ajooc18.png)

深入到&#x200B;**`citisignal_mobile_subscriptions`**。

![AJO OC](./images/ajooc19.png)

选择&#x200B;**`subscription_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc20.png)

为&#x200B;**聚合数据**&#x200B;启用切换器。 然后选择以下选项：

- **聚合函数**：**计数**
- **运算符**： **大于或等于**
- **值**： **1**

单击&#x200B;**确认**。

![AJO OC](./images/ajooc21.png)

您应该会看到此内容。 单击&#x200B;**确认**。

![AJO OC](./images/ajooc22.png)

### 构建受众2

单击另一路径中下一个节点上的&#x200B;**+**&#x200B;图标。

![AJO OC](./images/ajooc23.png)

选择&#x200B;**生成受众**。

![AJO OC](./images/ajooc24.png)

单击以打开&#x200B;**定向维度**&#x200B;的文件夹。

![AJO OC](./images/ajooc25.png)

选择&#x200B;**`--aepUserLdap--_mobile_subscriptions`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc26.png)

单击&#x200B;**创建受众**。

![AJO OC](./images/ajooc27.png)

单击&#x200B;**添加条件**。

![AJO OC](./images/ajooc28.png)

选择&#x200B;**subscription_status**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc29.png)

在&#x200B;**`active`**&#x200B;值&#x200B;**字段中输入**。 然后，单击&#x200B;**添加条件**。

![AJO OC](./images/ajooc30.png)

选择&#x200B;**`is_upgrade_eligible`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc31.png)

将&#x200B;**值**&#x200B;设置为&#x200B;**true**

![AJO OC](./images/ajooc32.png)

单击&#x200B;**计算**&#x200B;查看符合此受众条件的配置文件估算值。 然后单击&#x200B;**确认**

![AJO OC](./images/ajooc33.png)

### 拆分

单击&#x200B;**+**&#x200B;图标，然后选择&#x200B;**拆分**。

![AJO OC](./images/ajooc34.png)

将字段&#x200B;**Label**&#x200B;更改为&#x200B;**90/10 Treatment vs Control**。 单击以打开对象&#x200B;**子集**。

![AJO OC](./images/ajooc35.png)

为&#x200B;**启用Limit**&#x200B;启用切换器，并将&#x200B;**Limit size**&#x200B;设置为&#x200B;**10 perecent**。

![AJO OC](./images/ajooc36.png)

单击&#x200B;**添加区段**，然后您应该会看到正在添加的&#x200B;**结果**&#x200B;对象。

单击&#x200B;**保存**。

![AJO OC](./images/ajooc37.png)

### 保存受众

单击&#x200B;**+**&#x200B;图标，然后选择&#x200B;**保存受众**。

![AJO OC](./images/ajooc38.png)

将字段&#x200B;**受众标签**&#x200B;设置为&#x200B;**`--aepUserLdap-- - Control Group`**。 单击&#x200B;**添加受众映射**。

![AJO OC](./images/ajooc39.png)

深入到&#x200B;**定向维度**。

![AJO OC](./images/ajooc40.png)

选择&#x200B;**`account_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc41.png)

### 扩充： Internet订阅

单击&#x200B;**+**&#x200B;图标。

![AJO OC](./images/ajooc42.png)

选择&#x200B;**扩充**。

![AJO OC](./images/ajooc43.png)

您应该会看到此内容。 单击&#x200B;**添加扩充数据**。

![AJO OC](./images/ajooc44.png)

深入到&#x200B;**`Targeting dimension`**。

![AJO OC](./images/ajooc44a.png)

深入到&#x200B;**`citisignal_accounts`**。

![AJO OC](./images/ajooc45.png)

深入到&#x200B;**`citisignal_internet_subscriptions`**。

![AJO OC](./images/ajooc45a.png)

选择&#x200B;**`account_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc46.png)

您应该会看到此内容。 单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc47.png)

选择&#x200B;**`subscription_status`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc48.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc49.png)

选择&#x200B;**`connection_type`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc50.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc51.png)

选择&#x200B;**`service_city`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc52.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc53.png)

选择&#x200B;**`avg_dowload_usage_gb`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc54.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc55.png)

选择&#x200B;**`data_cap_gb`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc56.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc57.png)

选择&#x200B;**`advertised_speed_mbps`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc58.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc59.png)

选择&#x200B;**`monthly_recurring_charge`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc60.png)

单击&#x200B;**保存**。

![AJO OC](./images/ajooc61.png)

向上滚动并将字段&#x200B;**标签**&#x200B;更改为`Enrichment: Internet Subscription`。

![AJO OC](./images/ajooc61a.png)

### 扩充：移动设备订阅

单击下一个节点上的&#x200B;**+**&#x200B;图标，然后选择&#x200B;**扩充**。

![AJO OC](./images/ajooc62.png)

将字段&#x200B;**标签**&#x200B;更改为`Enrichment: Mobile Devices Subscription`，然后单击&#x200B;**添加扩充数据**。

![AJO OC](./images/ajooc63.png)

深入到&#x200B;**定向维度**。

![AJO OC](./images/ajooc64.png)

深入到&#x200B;**`citisignal_mobile_subscriptions`**。

![AJO OC](./images/ajooc65.png)

选择&#x200B;**`account_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc66.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc67.png)

选择&#x200B;**`subscription_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc68.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc69.png)

选择&#x200B;**`phone_number`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc70.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc71.png)

选择&#x200B;**`renewal_eligibility_date`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc72.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc73.png)

选择&#x200B;**`line_user_recipient_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc74.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc75.png)

选择&#x200B;**`is_upgrade_eligible`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc76.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc77.png)

选择&#x200B;**`current_device_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc78.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc79.png)

选择&#x200B;**`contract_start_date`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc80.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc81.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc82.png)

选择&#x200B;**`model`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc83.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc86.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc87.png)

选择&#x200B;**`manufacturer`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc88.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc89.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc90.png)

选择&#x200B;**`device_age_months`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc91.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc92.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc93.png)

选择&#x200B;**`is_upgrade_eligible`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc94.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc95.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc96.png)

选择&#x200B;**`recommended_upgrade_product_id`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc97.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc98.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc99.png)

选择&#x200B;**`monthly_payment`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc100.png)

单击&#x200B;**添加属性**。

![AJO OC](./images/ajooc101.png)

深入到&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc102.png)

为&#x200B;**启用排序**&#x200B;启用开关。 单击&#x200B;**编辑**&#x200B;图标。

![AJO OC](./images/ajooc103.png)

选择&#x200B;**`phone_number`**&#x200B;并单击&#x200B;**确认**。

![AJO OC](./images/ajooc104.png)

然后您应该拥有此项。

![AJO OC](./images/ajooc105.png)




然后您应该拥有此项。 单击&#x200B;**保存**。

![AJO OC](./images/ajooc80a.png)














![AJO OC](./images/ajooc103.png)


## 后续步骤

返回至[Adobe Journey Optimizer：编排的营销活动](./ajocampaigns.md){target="_blank"}

返回[所有模块](./../../../../overview.md){target="_blank"}
