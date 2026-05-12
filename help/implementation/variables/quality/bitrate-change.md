---
title: 比特率更改
description: 每当播放器切换到其他比特率时，触发比特率更改事件。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# 比特率更改

>[!BEGINSHADEBOX]

*本页介绍如何实施比特率更改事件。 查看相应报表变量的[比特率更改（维度）](/help/reporting/dimensions/bitrate-changes.md)和[比特率更改（量度）](/help/reporting/metrics/bitrate-changes.md)。*

>[!ENDSHADEBOX]

比特率变化事件表示播放器已切换到不同的比特率。 首先更新QoE对象上的[比特率](/help/implementation/variables/quality/bitrate.md)值，然后触发比特率更改事件。 后端会使用这些事件的计数来计算比特率更改维度和量度，生成的比特率值将馈送平均比特率。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | （无 — 由后端计数） |
| **XDM事件类型** | `media.bitrateChange` |
| **必需** | 否 |
| **发送条件** | 每当播放器切换比特率时 |

## Web SDK

使用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)发送具有新比特率的`media.bitrateChange`事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## Mobile SDK

使用新比特率更新QoE对象，然后触发比特率更改事件。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

使用带`media.bitrateChange`的`sendMediaEvent`表示比特率更改。 在`qoeDataDetails`中包含新比特率：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## Media Edge API

使用更新的`qoeDataDetails`调用[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## Media SDK

更新QoE对象并触发事件：

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## 媒体收集 API

使用新比特率发送`bitrateChange` POST请求：

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
