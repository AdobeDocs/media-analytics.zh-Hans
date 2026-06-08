---
title: 内容类型
description: 设置内容类型以标识流的格式（VOD、Live、Linear、Podcast、song等）。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 5%

---


# 内容类型

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**内容类型**&#x200B;变量的数据收集。 查看相应报表维度的[内容类型](/help/reporting/dimensions/content-type.md)。*

>[!ENDSHADEBOX]

内容类型变量标识流的格式（例如，VOD、Live或Linear表示视频，播客或有声读物表示音频）。 所有流媒体实施都需要它，并且必须在会话开始时设置。 Adobe定义的值会填充内置的内容类型区段和报表；自定义字符串也将被接受，但不会与内置区段匹配。 如果未设置，则值默认为`missing_content_type`。

建议值：

* **视频：** `vod`，`live`，`linear`，`ugc`，`dvod`
* **音频：** `song`，`podcast`，`audiobook`，`radio`

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.contentType` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.contentType` |
| **必需** | 是 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`contentType`：

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

将内容类型常量作为`streamType`参数传递给`createMediaObject`。 使用`MediaConstants.StreamType.*`值，如`VOD`、`LIVE`、`LINEAR`、`AOD`、`PODCAST`。 注意：在Mobile SDK中，`streamType`参数控制内容类型。 流类型变量（音频与视频）是单独的`mediaType`参数。

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

将内容类型常量作为`streamType`参数传递给`createMediaObject`。 使用`MediaConstants.StreamType.*`值，如`VOD`、`LIVE`、`LINEAR`、`AOD`、`PODCAST`。 注意：在Mobile SDK中，`streamType`参数控制内容类型。 流类型变量（音频与视频）是单独的`mediaType`参数。

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

调用`createMediaSession`时，在`xdm.mediaCollection.sessionDetails`中设置`contentType`：

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

调用`xdm.mediaCollection.sessionDetails`中包含`contentType`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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

将`ADB.Media.StreamType.*`常量作为第四个参数传递给`ADB.Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

将`ADBMobile.media.StreamType.*`常量作为第四个参数传递给`ADBMobile.media.createMediaObject`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

将`MEDIA_STREAM_TYPE_*`常量作为第四个(`streamType`)参数传递给`adb_media_init_mediainfo`。 在Roku 2.x SDK中，此参数带有内容类型(`vod`、`live`、`linear`)：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.contentType`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
