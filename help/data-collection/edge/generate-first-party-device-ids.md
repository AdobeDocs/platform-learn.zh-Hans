---
title: 生成第一方设备 ID
description: 了解如何生成第一方设备 ID
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---

# 生成第一方设备 ID

Adobe Experience Cloud应用程序传统上会使用不同的技术生成Cookie以存储设备ID，包括：

1. 第三方 Cookie
1. Adobe服务器使用域名的CNAME配置设置的第一方Cookie
1. JavaScript设置的第一方Cookie

最近的浏览器更改限制了这类Cookie的持续时间。 在使用客户拥有的服务器（使用DNS A/AAAA记录而非DNS CNAME）设置第一方Cookie时，它们最有效。 第一方设备ID (FPID)功能允许实施Adobe Experience Platform Web SDK的客户使用DNS A/AAAA-records在来自服务器的Cookie中使用设备ID。 然后，可以将这些ID发送到Adobe，并用作种子来生成Experience CloudID (ECID)，这仍然是Adobe Experience Cloud应用程序中的主要标识符。

以下是有关该功能的工作原理的简短示例：

![第一方设备ID (FPID)和Experience CloudID (ECID)](../assets/kt-9728.png)

1. 最终用户的浏览器从客户的Web服务器或CDN请求网页。
1. 客户在其Web服务器或CDN上生成设备ID (FPID)（Web服务器应绑定到域名的DNS A/AAAA-record）。
1. 客户设置第一方Cookie以将FPID存储在最终用户的浏览器中。
1. 客户的Adobe Experience Platform Web SDK实施会向Platform Edge Network发出请求，包括标识映射中的FPID。
1. Experience Platform边缘网络接收FPID并使用它生成Experience CloudID (ECID)。
1. Platform Web SDK响应会将ECID发送回最终用户的浏览器。
1. 如果 `idMigrationEnabled=true`， Platform Web SDK使用JavaScript将ECID存储为 `AMCV_` 最终用户浏览器中的Cookie 。
1. 如果 `AMCV_` Cookie过期，该过程将自行重复。 只要相同的第一方设备ID可用，就会有一个新的 `AMCV_` 创建的Cookie与之前的ECID值相同。

>[!NOTE]
>
>此 `idMigrationEnabled` 不需要设置为 `true` 以使用FPID。 替换为 `idMigrationEnabled=false` 您可能看不到 `AMCV_` 但是，和Cookie将需要在网络响应中查找ECID值。


在本教程中，我们使用了一个使用PHP脚本语言的特定示例来说明如何：

* 生成UUIDv4
* 将UUIDv4值写入Cookie
* 在身份映射中包含Cookie值
* 验证ECID生成

在产品文档中可找到与第一方设备ID相关的其他文档。

## 生成UUIDv4

PHP没有用于生成UUID的本地库，因此这些代码示例比使用其他编程语言时可能需要的代码示例更加广泛。 PHP之所以选择用于此示例，是因为它是一种广泛支持的服务器端语言。


调用以下函数时，会生成一个随机的UUID版本4：

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## 将UUIDv4值写入Cookie

以下代码会向上述函数发出请求以生成UUID。 然后，它会设置由您的组织决定的Cookie标记。 如果已生成Cookie，则会延长到期时间。

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>包含第一方设备ID的Cookie可以具有任何名称。

## 在身份映射中包含Cookie值

最后一步是使用PHP将Cookie值回显到Identity Map。


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>必须调用身份映射中使用的身份命名空间符号 `FPID`.
>
> `FPID` 是保留的身份命名空间，在身份命名空间的接口列表中不可见。


## 验证ECID生成

通过确认从第一方设备ID生成相同的ECID来验证实施：

1. 生成FPID Cookie。
1. 使用Platform Web SDK向Platform Edge Network发送请求。
1. 格式为的cookie `AMCV_<IMSORGID@AdobeOrg>` 生成。 此Cookie包含ECID。
1. 记下生成的Cookie值，然后删除网站的所有Cookie，但以下内容除外 `FPID` Cookie。
1. 向Platform Edge Network发送另一个请求。
1. 在中确认值 `AMCV_<IMSORGID@AdobeOrg>` Cookie是相同的 `ECID` 值，如下所示 `AMCV_` 已删除的Cookie。 如果给定FPID的Cookie值相同，则ECID的设定种子过程成功。

有关此功能的详细信息，请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
