---
title: 会话开始
description: 发出媒体会话开始的信号，并获取所有后续事件所需的会话ID。
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 10%

---


# 会话开始

会话开始事件会打开一个媒体跟踪会话。 它必须是任何播放发送的第一个事件。 响应将返回一个会话ID，同一会话的所有后续事件必须包含该ID。

如果&#x200B;**在10分钟内未收到任何事件**，或者&#x200B;**在30分钟内未移动播放头**，则会话将自动过期。 如果会话过期，则必须调用会话重新开始以获取新的会话ID。

* **先决条件**：无；始终为第一个事件
* **关联的量度**： [媒体开始](/help/reporting/metrics/media-starts.md)

## Web SDK

使用`eventType: "media.sessionStart"`和所需的`sessionDetails`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)。 响应包含`handle[].payload[].sessionId`中的会话ID （类型`media-analytics:new-session`）。 存储此值并在所有后续事件中将其作为`sessionID`传递。

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
      playhead: 0
    }
  }
});
```

## Mobile SDK

使用媒体对象和可选元数据调用`trackSessionStart`。

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku (BrightScript)

使用所需的会话详细信息调用`createMediaSession`：

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
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点。 响应包含`handle[].payload[].sessionId`中的会话ID （类型`media-analytics:new-session`）。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## Media SDK

使用使用`ADB.Media.createMediaObject`创建的媒体对象调用`trackSessionStart`：

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## 媒体收集 API

向[会话终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)发送`sessionStart`帖子。 响应`Location`标头包含要在所有后续事件请求中使用的会话ID。

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
