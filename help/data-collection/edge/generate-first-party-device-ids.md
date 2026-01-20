---
title: 生成第一方设备Id
description: 了解如何生成第一方设备 ID
feature: Web SDK
level: Experienced
jira: KT-9728
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: fe848fe7376fbeb54fb53ee0947a9f8284fcef61
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# 生成第一方设备Id

Adobe Experience Cloud应用程序传统上会使用不同的技术生成Cookie以存储设备ID，包括：

1. 第三方Cookie
1. Adobe服务器使用域名的CNAME配置设置的第一方Cookie
1. JavaScript设置的第一方Cookie

最近的浏览器更改限制了这类Cookie的持续时间。 在使用客户拥有的服务器（使用DNS A/AAAA记录而非DNS CNAME）设置第一方Cookie时，它们最有效。 [第一方设备ID (FPID)功能](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/identity/first-party-device-ids)允许实施Adobe Experience Platform Web SDK的客户在使用DNS A/AAAA记录的服务器中的Cookie中使用设备ID。 然后，可以将这些ID发送到Adobe并用作生成Experience Cloud ID (ECID)的种子，该ID仍是Adobe Experience Cloud应用程序中的主要标识符。

以下是有关该功能的工作原理的简短示例：

![第一方设备ID (FPID)和Experience Cloud ID (ECID)](../assets/kt-9728.png)

1. 最终用户的浏览器从客户的Web服务器或CDN请求网页。
1. 客户在其Web服务器或CDN上生成设备ID (FPID)（Web服务器应绑定到域名的DNS A/AAAA-record）。
1. 客户设置第一方Cookie以将FPID存储在最终用户的浏览器中。
1. 客户的Adobe Experience Platform Web SDK实施会向Platform Edge Network发出请求，并且：
   1. 在标识映射中包含FPID。
   1. 为其Web SDK请求配置CNAME，并使用其FPID Cookie的名称配置其数据流。
1. Experience Platform Edge Network接收FPID并使用它生成Experience Cloud ID (ECID)。
1. Platform Web SDK响应会将ECID发送回最终用户的浏览器。
1. 如果`idMigrationEnabled=true`，Platform Web SDK使用JavaScript将ECID存储为最终用户浏览器中的`AMCV_` Cookie。
1. 如果`AMCV_` Cookie过期，进程将自行重复。 只要有相同的第一方设备ID可用，就会使用与之前相同的ECID值创建一个新的`AMCV_` Cookie。

>[!NOTE]
>
>无需将`idMigrationEnabled`设置为`true`即可使用FPID。 但使用`idMigrationEnabled=false`时，您可能无法看到`AMCV_` Cookie，因此需要在网络响应中查找ECID值。


在本教程中，使用了一个使用PHP脚本语言的特定示例来说明如何：

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
>身份映射中使用的身份命名空间符号必须称为`FPID`。
>
> `FPID`是保留的身份命名空间，在身份命名空间的接口列表中不可见。


## 验证ECID生成

通过确认从第一方设备ID生成相同的ECID来验证实施：

1. 生成FPID Cookie。
1. 使用Platform Web SDK向Platform Edge Network发送请求。
1. 生成格式为`AMCV_<IMSORGID@AdobeOrg>`的Cookie。 此Cookie包含ECID。
1. 记下生成的Cookie值，然后删除网站的所有Cookie（`FPID` Cookie除外）。
1. 向Platform Edge Network发送另一个请求。
1. 确认`AMCV_<IMSORGID@AdobeOrg>` Cookie中的值与已删除的`ECID` Cookie中的值相同`AMCV_`。 如果给定FPID的Cookie值相同，则ECID的设定种子过程成功。

有关此功能的详细信息，请参阅[文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html)。
