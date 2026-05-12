---
title: 开始时间
description: 设置播放器的启动时间（以毫秒为单位），以便后端可以报告时间到第一帧质量。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 12%

---


# 开始时间

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**开始时间**变量的数据收集。 有关相应的报表维度和量度，请参阅[开始时间](/help/reporting/dimensions/time-to-start.md)。*

>[!ENDSHADEBOX]

开始时间变量是播放器启动播放与第一个帧渲染之间经过的时间，以毫秒为单位。 在会话开始事件触发之前在QoE对象上设置它。 Adobe以秒为单位存储和报告值；传递毫秒，Adobe在摄取时转换。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.qoe.timeToStart` |
| **XDM集合字段** | [`mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **必需** | 否 |
| **发送条件** | 会话开始，会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`media.sessionStart`的`mediaCollection.qoeDataDetails`中设置`timeToStart`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

将启动时间作为第二个参数(`startupTime`)传递给`createQoEObject`。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

调用`createMediaSession`时，在`media.sessionStart`的`mediaCollection.qoeDataDetails`中设置`timeToStart`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用`mediaCollection.qoeDataDetails`中包含`timeToStart`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

将开始时间作为第二个参数传递给`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## 媒体收集 API

在`sessionStart`上的`params`对象中包括`media.qoe.timeToStart`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
