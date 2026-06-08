---
title: 广告 ID
description: 唯一地标识广告。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 9%

---


# 广告 ID

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告ID**变量的数据收集。 有关相应的报表维度，请参阅[广告](/help/reporting/dimensions/ad.md)。*

>[!ENDSHADEBOX]

广告ID变量可唯一标识每个广告。 您的播放器跟踪的每个广告都需要使用此参数。 在每个`media.adStart`事件上设置它。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.name` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.name` |
| **必需** | 是 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

为`media.adStart`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingDetails`中设置`name`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将广告ID作为`adId`参数传递给`createAdObject`。 第一个参数(`name`)是友好名称；第二个参数是ID。

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

将广告ID作为`adId`参数传递给`createAdObject`。 第一个参数(`name`)是友好名称；第二个参数是ID。

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

为`media.adStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingDetails`中设置`name`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingDetails`中包含`name`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

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

将广告ID作为第二个参数传递给`ADB.Media.createAdObject`：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",   // name (friendly name)
  "ad-2125",      // ad ID
  0,              // position in pod
  15              // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

将广告ID作为第二个参数传递给`ADBMobile.media.createAdObject`：

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",
  "ad-2125",
  1,
  30
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

将广告ID作为第二个参数传递给`adb_media_init_adinfo`：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒体收集API]

在`adStart` POST请求的`params`对象中包括`media.ad.id`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
