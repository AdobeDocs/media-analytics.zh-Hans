---
title: 比特率更改
description: 表示播放比特率已更改的信号。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# 比特率更改

比特率更改事件表示播放器协商了新的播放比特率。 每当播放期间比特率发生更改时发送该数据包。 在QoE数据中包含新的比特率值，以便后端可以计算[[!UICONTROL 平均比特率]](/help/reporting/metrics/average-bitrate.md)和每比特率存储桶维度。

* **先决条件**： [会话开始](../session/session-start.md)
* **关联的量度**： [[!UICONTROL 比特率更改]](/help/reporting/metrics/bitrate-changes.md)

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.bitrateChange"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)并在`qoeDataDetails`中使用新比特率：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

使用新比特率创建一个QoE对象，并在触发比特率更改事件之前更新跟踪器。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

使用新比特率创建一个QoE对象，并在触发比特率更改事件之前更新跟踪器。

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku]

在`qoeDataDetails`中使用`eventType: "media.bitrateChange"`和新比特率调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

在`qoeDataDetails`中使用新比特率调用[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
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

使用新比特率创建QoE对象并更新跟踪器：

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

更新`getQoSObject`委托返回的QoS对象，然后跟踪该事件：

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB 媒体收集API]

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`bitrateChange`个POST，新比特率位于`qoeData`中：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```

>[!ENDTABS]
