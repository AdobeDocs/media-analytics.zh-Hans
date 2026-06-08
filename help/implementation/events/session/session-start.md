---
title: 会话开始
description: 发出媒体会话开始的信号，并获取所有后续事件所需的会话ID。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---


# 会话开始

会话开始事件会打开一个媒体跟踪会话。 它必须是任何播放发送的第一个事件。 响应将返回一个会话ID，同一会话的所有后续事件必须包含该ID。

如果&#x200B;**在10分钟内未收到任何事件**，或者&#x200B;**在30分钟内未移动播放头**，则会话将自动过期。 如果会话过期，则必须调用会话重新开始以获取新的会话ID。

* **先决条件**：无；始终为第一个事件
* **关联的量度**： [[!UICONTROL 媒体开始]](/help/reporting/metrics/media-starts.md)

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

使用媒体对象和可选元数据调用`trackSessionStart`。

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

使用媒体对象和可选元数据调用`trackSessionStart`。

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

使用使用`ADBMobile.media.createMediaObject`创建的媒体对象调用`trackSessionStart`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "video-123",                        // name
  "video-id-123",                     // media ID
  128,                                // length (seconds)
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);

ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

使用`adb_media_init_mediainfo`生成媒体对象并调用`mediaTrackSessionStart`。 可选的第二个参数接受`a.media.*`元数据键或`invalid`的关联数组：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("video-123", "video-id-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

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

>[!ENDTABS]

## 恢复会话

在恢复之前关闭的会话时（例如，在跨设备切换后或应用程序恢复保存的播放状态后），在会话开始时设置恢复标志。 这会导致Analytics递增[[!UICONTROL 内容恢复]](/help/reporting/metrics/content-resumes.md)，而不是[[!UICONTROL 媒体开始]](/help/reporting/metrics/media-starts.md)。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

将`hasResume: true`添加到`sessionDetails`：

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
        streamType: "video",
        hasResume: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

在调用`trackSessionStart`之前，在媒体对象上设置`resumed`键：

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

mediaObject[MediaConstants.MediaObjectKey.resumed] = true
tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

在调用`trackSessionStart`之前，在媒体对象上设置`RESUMED`键：

```kotlin
val mediaObject = Media.createMediaObject("video-123", "video-id-123", 128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

mediaObject[Media.MediaObjectKey.RESUMED] = true
tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku Edge]

将`"hasResume": true`添加到`sessionDetails`：

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

将`"hasResume": true`添加到`sessionDetails`：

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
          "channel": "Sports",
          "hasResume": true
        },
        "playhead": 0
      }
    }
  }]
}'
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

在媒体对象上设置`MediaResumed`键：

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video
);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;
tracker.trackSessionStart(mediaObject, null);
```

>[!TAB Chromecast]

在媒体对象上设置`MediaResumed`键：

```javascript
var mediaObject = ADBMobile.media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video
);

mediaObject[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaObject, null);
```

>[!TAB Roku 2.x]

在调用`mediaTrackSessionStart`之前，在媒体对象上设置`resumed`键：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("video-123", "video-id-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)
mediaInfo.resumed = true

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

将`"media.resume": true`添加到`params`对象：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123",
    "media.resume": true
  }
}
```

>[!ENDTABS]
