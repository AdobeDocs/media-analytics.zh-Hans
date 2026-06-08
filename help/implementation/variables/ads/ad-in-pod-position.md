---
title: 面板中的广告位置
description: 将广告的索引位置设置在其父广告时间内。 第一个广告的索引为0。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# 面板中的广告位置

>[!BEGINSHADEBOX]

*本页介绍面板位置&#x200B;**变量中的**广告的数据收集。 查看面板位置](/help/reporting/dimensions/ad-in-pod-position.md)中的[广告以了解相应的报表维度。*

>[!ENDSHADEBOX]

pod position变量中的广告是广告在其父广告时间内的零索引位置。 面板中的第一个广告具有索引`0`，第二个具有索引`1`，依此类推。 使用维度可按广告时间内的位置比较参与和完成情况。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.podPosition` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.podPosition` |
| **必需** | 是 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingDetails`中设置`podPosition`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将位置作为第三个参数传递给`createAdObject`。

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

将位置作为第三个参数传递给`createAdObject`。

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

为`media.adStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingDetails`中设置`podPosition`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "podPosition": 0,
                "length": 15,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingDetails`中包含`podPosition`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

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

将位置作为第三个参数传递给`ADB.Media.createAdObject`：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

将位置作为第三个参数传递给`ADBMobile.media.createAdObject`：

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

将位置作为第三个参数传递给`adb_media_init_adinfo`。 面板中的广告位置是从1开始的：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.ad.podPosition`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.podPosition": 0
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
