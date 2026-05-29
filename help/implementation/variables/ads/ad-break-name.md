---
title: 广告时间名称
description: 设置父广告时间的友好名称。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 6%

---


# 广告时间名称

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告时间名称**变量的数据收集。 有关相应的报表维度，请参阅[面板名称](/help/reporting/dimensions/pod-name.md)。*

>[!ENDSHADEBOX]

广告时间名称变量是广告时间的友好名称（例如，`"pre-roll"`、`"mid-roll-1"`、`"post-roll"`）。 该值在广告时间对象中设置，而不是在单个广告中设置。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.podFriendlyName` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.podFriendlyName` |
| **必需** | 是(Mobile SDK)；否（Edge、媒体收集API） |
| **发送条件** | [广告时间开始](/help/implementation/events/ads/ad-break-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

为`media.adBreakStart`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingPodDetails`中设置`friendlyName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将广告时间名称作为第一个(`name`)参数传递给`createAdBreakObject`，然后在广告开始事件之前跟踪广告时间开始事件。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

将广告时间名称作为第一个(`name`)参数传递给`createAdBreakObject`，然后在广告开始事件之前跟踪广告时间开始事件。

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

为`media.adBreakStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingPodDetails`中设置`friendlyName`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingPodDetails`中包含`friendlyName`的[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

将广告时间名称作为第一个参数传递给`ADB.Media.createAdBreakObject`：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

将广告时间名称作为第一个参数传递给`ADBMobile.media.createAdBreakObject`：

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",
  1,
  0
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB 媒体收集API]

在`adBreakStart` POST请求的`params`对象中包括`media.ad.podFriendlyName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
