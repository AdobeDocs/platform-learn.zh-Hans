---
title: 替换SDK — 将移动应用程序中的Adobe Target实施迁移到Offer Decisioning和Target扩展
description: 了解在从SDK迁移到Offer Decisioning和Adobe Target Mobile扩展时如何替换Target。
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

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
> * **优化SDK**&#x200B;实现&#x200B;**Offer Decisioning和Target扩展**

## 更新依赖项

+++Android示例

>[!BEGINTABS]

>[!TAB 优化SDK]

迁移后的`build.gradle`依赖项

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:optimize'
```


>[!TAB 定位SDK]

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


>[!ENDTABS]

+++

+++ iOS示例

>[!BEGINTABS]


>[!TAB 优化SDK]

迁移后的`Podfile`依赖项

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB 定位SDK]

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

+++

## 更新导入和代码

+++ Android示例

>[!BEGINTABS]

>[!TAB 优化SDK]

迁移后的Java初始化代码

```Java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;
 
public class MainApp extends Application {
 
  private final String ENVIRONMENT_FILE_ID = "YOUR_APP_ENVIRONMENT_ID";
 
    @Override
    public void onCreate() {
        super.onCreate();
 
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID(ENVIRONMENT_FILE_ID);
 
        MobileCore.registerExtensions(
            Arrays.asList(Edge.EXTENSION, Identity.EXTENSION, Optimize.EXTENSION),
            o -> Log.d("MainApp", "Offer Decisioning and Target Mobile SDK was initialized.")
        );
    }
}
```

>[!TAB 定位SDK]

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

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB 优化SDK]

迁移后的Swift初始化代码

```Swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize
 
@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
 
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {
 
      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }
 
      return true
  }
}
```

>[!TAB 定位SDK]

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

+++

## API比较

许多Target扩展API都具有使用下表所述的Offer Decisioning和Target扩展的等效方法。 有关[函数](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/)的更多详细信息，请参阅API参考。

| 目标扩展 | Offer Decisioning和Target扩展 | 注释 |
| --- | --- | --- | 
| [prefetchContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#prefetchcontent){target=_blank} | [updatePropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#updatepropositionswithcompletionhandlerandtimeout){target=_blank} |  |
| [retrieveLocationContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [getPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#getpropositionswithtimeout){target=_blank} | 使用`getPropositions` API时，不会进行远程调用以获取SDK中未缓存的作用域。 |
| [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [选件 — >已显示()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | 此外，`generateDisplayInteractionXdm`选件方法可用于为项目显示生成XDM。 随后，Edge网络SDK的sendEvent API可用于附加其他XDM自由格式数据并将体验事件发送到远程。 |
| [clickedLocation](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [选件 — >已点按()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | 此外，`generateTapInteractionXdm`选件方法可用于为项目点按生成XDM。 随后，Edge网络SDK的sendEvent API可用于附加其他XDM自由格式数据并将体验事件发送到远程。 |
| [clearPrefetchCache](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [clearCachedPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} |  |
| [重置体验](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#resetexperience){target=_blank} | 不适用 | 为SDK使用[removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity){target=_blank} API from Identity for Edge Network扩展停止将访客标识符发送到Edge网络。 有关详细信息，请参阅[removeIdentity API文档](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)。 <br><br>注意： Mobile Core的`resetIdentities` API清除了SDK中所有存储的身份，包括Experience Cloud ID (ECID)，应谨慎使用它！ |
| [getSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getsessionid){target=_blank} | 不适用 | `state:store`响应句柄包含与会话相关的信息。 Edge network extension可将未过期状态存储区项目附加到后续请求，从而帮助管理它。 |
| [setSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setsessionid){target=_blank} | 不适用 | `state:store`响应句柄包含与会话相关的信息。 Edge network extension可将未过期状态存储区项目附加到后续请求，从而帮助管理它。 |
| [getThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getthirdpartyid){target=_blank} | 不适用 | 使用Identity for Edge Network扩展中的updateIdentities API提供第三方ID值。 然后，在数据流中配置第三方ID命名空间。 有关更多详细信息，请参阅[Target第三方ID移动设备文档](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| [setThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setthirdpartyid){target=_blank} | 不适用 | 使用Identity for Edge Network扩展中的updateIdentities API提供第三方ID值。 然后，在数据流中配置第三方ID命名空间。 有关更多详细信息，请参阅[Target第三方ID移动设备文档](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| [getTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | 不适用 | `locationHint:result`响应句柄包含Target位置提示信息。 假设Target Edge将与Experience Edge位于同一位置。<br> <br>Edge网络扩展使用EdgeNetwork位置提示来确定要将请求发送到的Edge网络群集。 要跨SDK（混合应用程序）共享Edge网络位置提示，请使用Edge Network扩展中的`getLocationHint`和`setLocationHint` API。 有关更多详细信息，请参阅[`getLocationHint` API文档](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |
| [setTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | 不适用 | [locationHint：result](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#setlocationhint){target=_blank}响应句柄包含Target位置提示信息。 假设Target Edge将与Experience Edge位于同一位置。<br> <br>Edge网络扩展使用EdgeNetwork位置提示来确定要将请求发送到的Edge网络群集。 要跨SDK（混合应用程序）共享Edge网络位置提示，请使用Edge Network扩展中的`getLocationHint`和`setLocationHint` API。 有关更多详细信息，请参阅[`getLocationHint` API文档](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |


接下来，了解如何[请求并将活动](retrieve-activities.md)渲染到页面。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Offer Decisioning和Target扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=zh-Hans#M625)中发帖让我们知道。
