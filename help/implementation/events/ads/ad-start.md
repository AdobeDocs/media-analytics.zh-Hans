---
title: 广告开始
description: 表示单个广告开始播放。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 6%
---

# 广告开始

广告开始事件表示单个广告开始播放。 它必须出现在[广告时间开始](ad-break-start.md) / [广告时间结束](ad-break-complete.md)对中。

* **先决条件**： [会话开始](../session/session-start.md)，[广告时间开始](ad-break-start.md)
* **关联的量度**：[[!UICONTROL 广告开始]](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>此事件必须由`adBreakStart`和`adBreakComplete`书档包围，即使播放了单个广告也是如此。 如果没有这些书挡，广告事件将被忽略，广告持续时间将被计为主内容持续时间。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.adStart"`和所需的`advertisingDetails`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

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

将广告名称、ID、面板位置和长度传递给`createAdObject`，然后调用`trackEvent`。

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

将广告名称、ID、面板位置和长度传递给`createAdObject`，然后调用`trackEvent`。

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

使用`eventType: "media.adStart"`和所需的`advertisingDetails`调用`sendMediaEvent`：

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

使用所需的`advertisingDetails`调用[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

将广告名称、ID、位置和长度传递给`ADB.Media.createAdObject`：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

>[!TAB Chromecast]

将广告名称、ID、位置和长度传递给`ADBMobile.media.createAdObject`：

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

使用`adb_media_init_adinfo`生成广告对象，然后跟踪该事件。 面板中的广告位置是从1开始的。

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 15.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒体收集API]

向[事件终结点](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)发送`adStart`帖子：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```

>[!ENDTABS]
