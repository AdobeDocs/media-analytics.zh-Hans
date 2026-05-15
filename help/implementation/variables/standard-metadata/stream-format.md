---
title: 流格式
description: 设置流格式以标识质量层（HD、SD或您的投放管道使用的其他标签）。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# 流格式

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**流格式**&#x200B;变量的数据收集。 查看相应报表维度的[流格式](/help/reporting/dimensions/stream-format.md)。*

>[!ENDSHADEBOX]

流格式变量标识流的质量层（通常为`"HD"`或`"SD"`，但可接受任何字符串）。 当您要按交付质量层划分参与、完成或质量时，请设置它。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.format` |
| **XDM集合字段** | [`mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.format` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.sessionDetails`中设置`streamFormat`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

将流格式作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`在`sessionDetails`中设置`streamFormat`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用`mediaCollection.sessionDetails`中包含`streamFormat`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "channel": "Sports",
          "streamFormat": "HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.StreamFormat`在`contextData`对象中传递流格式：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## 媒体收集 API

在`sessionStart` POST请求的`params`对象中包括`media.streamFormat`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
