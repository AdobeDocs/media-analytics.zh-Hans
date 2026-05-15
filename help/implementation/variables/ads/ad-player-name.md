---
title: 广告播放器名称
description: 设置呈现广告的播放器的名称。 广告播放器可以不同于主内容播放器。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 11%

---


# 广告播放器名称

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告播放器名称**变量的数据收集。 有关相应的报表维度，请参阅[广告播放器名称](/help/reporting/dimensions/ad-player-name.md)。*

>[!ENDSHADEBOX]

广告播放器名称变量可识别呈现每个广告的播放器（例如，`"Freewheel"`、`"Google IMA"`）。 当服务器端广告插入服务拼合广告时，广告播放器可以不同于主内容播放器。 使用此变量可比较不同广告服务栈栈的质量和完成情况。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.playerName` |
| **XDM集合字段** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.playerName` |
| **必需** | 是 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.advertisingDetails`中设置`playerName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

将广告播放器名称作为元数据HashMap参数中的`MediaConstants.AdMetadataKeys.AD_PLAYER`键传递给`trackEvent(AdStart)`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

为`media.adStart`调用`sendMediaEvent`时，在`mediaCollection.advertisingDetails`中设置`playerName`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用`mediaCollection.advertisingDetails`中包含`playerName`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.AdMetadataKeys.AdPlayer`在`contextData`对象中传递广告播放器名称：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## 媒体收集 API

在`adStart` POST请求的`params`对象中包括`media.ad.playerName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
