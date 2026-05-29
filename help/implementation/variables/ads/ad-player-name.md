---
title: 广告播放器名称
description: 设置呈现广告的播放器的名称。 广告播放器可以不同于主内容播放器。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# 广告播放器名称

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告播放器名称**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[广告播放器名称](/help/reporting/dimensions/ad-player-name.md)。*

>[!ENDSHADEBOX]

广告播放器名称变量可识别呈现每个广告的播放器（例如，`"Freewheel"`、`"Google IMA"`）。 当服务器端广告插入服务拼合广告时，广告播放器可以不同于主内容播放器。 使用此变量可比较不同广告服务栈栈的质量和完成情况。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.playerName` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.playerName` |
| **必需** | 是 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingDetails`中设置`playerName`：

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

>[!TAB iOS]

将广告播放器名称作为元数据HashMap参数中的`MediaConstants.AdMetadataKeys.AD_PLAYER`键传递给`trackEvent(AdStart)`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

将广告播放器名称作为元数据HashMap参数中的`MediaConstants.AdMetadataKeys.AD_PLAYER`键传递给`trackEvent(AdStart)`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

为`media.adStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingDetails`中设置`playerName`：

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

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingDetails`中包含`playerName`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`ADB.Media.AdMetadataKeys.AdPlayer`在`contextData`对象中传递广告播放器名称：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

跟踪广告开始事件时，在上下文元数据对象中传递广告播放器名称：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var metadata = { "a.media.ad.playerName": "Chromecast Player" };
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, metadata);
```

>[!TAB 媒体收集API]

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

>[!ENDTABS]
