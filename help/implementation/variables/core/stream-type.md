---
title: 流类型
description: 设置流类型以标识媒体流是音频还是视频内容。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 10%

---


# 流类型

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**流类型**&#x200B;变量的数据收集。 查看相应报表维度的[流类型](/help/reporting/dimensions/stream-type.md)。*

>[!ENDSHADEBOX]

流类型变量标识媒体流是音频还是视频内容。 所有流媒体实施都需要它，并且必须在每个媒体会话开始时设置。

正确设置流类型是流媒体报表的基础。 它启用Adobe Analytics中的内置&#x200B;**媒体流类型**&#x200B;区段（所有媒体、仅限音频、仅限视频），并在Customer Journey Analytics中驱动单独的音频和视频报表。 它还确保在整个媒体分析管道中对会话数据进行正确分类。 在下游报表中，流类型未设置或无效的会话可能会被取消分组或错误分类。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.streamType` |
| **XDM集合字段** | [`mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.streamType` |
| **必需** | 是 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.sessionDetails`中设置`streamType`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

将`Media.MediaType.Video`或`Media.MediaType.Audio`作为`mediaType`参数传递给`createMediaObject`。 请注意，`createMediaObject`中的`streamType`参数控制内容类型变量（VOD、Live等），而不是此变量。

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

调用`createMediaSession`时，在`mediaCollection.sessionDetails`中设置`streamType`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用`mediaCollection.sessionDetails`中包含`streamType`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "streamType": "video"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

将`ADB.Media.MediaType.Video`或`ADB.Media.MediaType.Audio`作为第五个参数传递给`Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## 媒体收集 API

在`sessionStart` POST请求的`params`对象中包括`media.streamType`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

有关完整请求结构和所有必填字段，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
