---
title: 广告时间开始时间
description: 在内容中设置广告时间的开始时间（偏移）（以秒为单位）。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 7%

---


# 广告时间开始时间

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告时间开始时间**变量的数据收集。 查看相应报表维度的[面板位置](/help/reporting/dimensions/pod-position.md)。*

>[!ENDSHADEBOX]

广告时间开始时间变量是广告时间在内容中的偏移，以秒为单位。 对于前置滚动，值为`0`；对于中置滚动，值是播放头开始的位置。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.podSecond` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.podSecond` |
| **必需** | 是 |
| **发送条件** | [广告时间开始](/help/implementation/events/ads/ad-break-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingPodDetails`中设置`offset`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将开始时间（以秒为单位）作为第三个参数传递给`createAdBreakObject`。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

将开始时间（以秒为单位）作为第三个参数传递给`createAdBreakObject`。

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

为`media.adBreakStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingPodDetails`中设置`offset`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingPodDetails`中包含`offset`的[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

将开始时间作为第三个参数传递给`ADB.Media.createAdBreakObject`：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

将开始时间（以秒为单位）作为第三个参数传递给`ADBMobile.media.createAdBreakObject`：

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB 媒体收集API]

在`adBreakStart` POST请求的`params`对象中包括`media.ad.podSecond`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
