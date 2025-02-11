---
title: 替换SDK — 从Adobe Target迁移到Adobe Journey Optimizer - Decisioning Mobile扩展
description: 了解在从SDK迁移到Adobe Journey Optimizer - Decisioning Mobile扩展时如何替换Adobe Target。
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: a928fb5c8e48e71984b75faf4eb397814caac6aa
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 将Target SDK替换为优化SDK

了解如何在移动实施中将Adobe Target SDK替换为优化SDK。 基本替换包含以下步骤：

* 更新Podfile或`build.gradle`文件中的依赖项
* 更新导入
* 更新应用程序代码

>[!INFO]
>
>在Adobe Experience Platform Mobile SDK生态系统内，扩展由导入到您的应用程序中的SDK实施，这些SDK可能具有不同的名称：
>
> * **Target SDK**&#x200B;实现&#x200B;**Adobe Target扩展**
> * **优化SDK**&#x200B;实施&#x200B;**Adobe Journey Optimizer - Decisioning扩展**

## 更新依赖项


>[!BEGINTABS]

>优化SDK-Android的[!TAB 应用程序依赖项]

迁移后的`build.gradle`依赖项

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:edgeconsent'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:assurance'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```

>优化SDK-iOS的[!TAB 应用程序依赖项]

迁移后的`Podfile`依赖项

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>Target SDK-Android的[!TAB 应用程序依赖项]

迁移前`build.gradle`个依赖项

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```

>Target SDK-iOS的[!TAB 应用程序依赖项]

迁移前`Podfile`个依赖项

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]


## 更新导入和代码

>[!BEGINTABS]

>[!TAB 优化SDK-Android]

迁移后的Java初始化代码

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Assurance;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
import com.adobe.marketing.mobile.edge.consent.Consent;
import com.adobe.marketing.mobile.edge.identity.Identity;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Consent.EXTENSION,
            com.adobe.marketing.mobile.edge.identity.Identity.EXTENSION,
            com.adobe.marketing.mobile.Identity.EXTENSION,
            Edge.EXTENSION,
            Assurance.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!TAB 优化SDK-iOS]

迁移后的Swift初始化代码

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Consent.self,
            AEPEdgeIdentity.Identity.self,
            AEPIdentity.Identity.self,
            Edge.self,
            Assurance.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!TAB 定位SDK-Android]

迁移前的Java初始化代码

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!TAB 定位SDK-iOS]

迁移前的Swift初始化代码

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]


接下来，了解如何[请求并将活动](render-activities.md)渲染到页面。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Decisioning扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中发帖让我们知道。
