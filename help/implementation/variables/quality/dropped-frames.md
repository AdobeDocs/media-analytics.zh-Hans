---
title: 丢帧
description: 设置QoE对象上丢帧的运行计数，以便后端可以报告丢帧质量。
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 9%

---


# 丢帧

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**丢帧**变量的数据收集。 查看相应报表维度和量度的[丢帧](/help/reporting/dimensions/dropped-frames.md)。*

>[!ENDSHADEBOX]

dropped frames变量是播放器在会话期间丢帧的运行计数。 在QoE对象中设置此参数，并在播放器报告新流量骤减时更新值。 会话关闭时，后端会报告最新值。

>[!NOTE]
>
>始终传递截至该时间点的整个会话的丢帧总数&#x200B;**累计**，而不是按时间间隔的增量。 如果在更新之间将该值重置为`0`，则后端将接收`0`作为最终值，并报告会话的零丢帧，而不考虑之前实际丢帧的情况。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.qoe.droppedFrameCount` |
| **XDM集合字段** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **必需** | 否 |
| **发送条件** | 质量事件（[比特率更改](/help/implementation/events/playback/bitrate-change.md)，[缓冲开始](/help/implementation/events/playback/buffer-start.md)，[错误](/help/implementation/events/error.md)），会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.qoeDataDetails`中设置`droppedFrames`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

将丢帧作为第四个参数传递给`createQoEObject`。 在触发任何质量事件之前更新跟踪器。

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

调用`sendMediaEvent`时，在`mediaCollection.qoeDataDetails`中设置`droppedFrames`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

调用`mediaCollection.qoeDataDetails`中包含`droppedFrames`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

将丢帧作为第四个参数传递给`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## 媒体收集 API

在`params`对象中包括`media.qoe.droppedFrames`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
