---
title: 检索Target活动 — 将移动设备应用程序中的Adobe Target实施迁移到Offer Decisioning和Target扩展
description: 了解在从Adobe Target迁移到Offer Decisioning和Adobe Target移动设备扩展时如何检索Target活动。
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 检索Target活动

Target移动设备实施使用区域mbox（现在称为“范围”）从使用Target基于表单的体验编辑器的活动交付内容。 您需要更新移动应用程序以在网络调用中包含范围。

Target返回的内容（也称为“选件”）通常由文本或JSON组成，您需要将这些文本或JSON用在应用程序中才能呈现最终的客户体验。 Target中的选件通常用于：

* 在应用程序中启用功能标记
* 提供替换文本或图像

如果您的活动需要同时在Target扩展以及应用程序的Offer Decisioning和Target扩展版本中运行，请务必进行全面测试。 如果您需要对应用程序的不同版本使用不同的选件，请考虑使用界面中的定位选项将不同的选件交付给不同的版本。

请始终确保包括错误处理功能，以在错误条件下显示合适的体验。


## 按需请求和应用内容

>[!IMPORTANT]
>
>将内容应用到应用程序后，必须触发`displayed` API，以告知Target访客已查看活动中指定的替代内容或默认内容。 有关更多详细信息，请参阅[跟踪Target转化事件](track-events.md)页面。


+++ Android示例

>[!BEGINTABS]

>[!TAB 优化SDK]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ iOS示例

>[!BEGINTABS]

>[!TAB 优化SDK]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++



接下来，了解如何使用Offer Decisioning和Target扩展[传递目标参数](send-parameters.md)。

>[!NOTE]
>
>我们致力于帮助您成功将Target移动设备扩展从Target扩展迁移到Offer Decisioning和Target扩展。 如果您在迁移过程中遇到障碍或觉得本指南中缺少关键信息，请在[此社区讨论](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=zh-Hans#M625)中发帖让我们知道。
