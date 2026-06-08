---
title: 内容名称
description: 设置内容的友好名称（报告中显示的可读标题）。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 8%

---


# 内容名称

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**内容名称**变量的数据收集。 有关相应的报表维度，请参阅[内容名称](/help/reporting/dimensions/content-name.md)。*

>[!ENDSHADEBOX]

内容名称变量是易于用户识别的内容标题（例如，`"Blinding Light"`）。 它是可选的，但强烈推荐。 在XDM架构中，它将映射到`friendlyName` （不是`name`；`name`保存内容ID）。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.friendlyName` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.friendlyName` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`friendlyName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "Blinding Light",
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

将可读名称作为第一个(`name`)参数传递给`createMediaObject`。 第二个参数是内容ID。

```swift
let mediaObject = Media.createMediaObjectWith(name: "Blinding Light",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

将可读名称作为第一个(`name`)参数传递给`createMediaObject`。 第二个参数是内容ID。

```kotlin
var mediaInfo = Media.createMediaObject("Blinding Light",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

调用`createMediaSession`时，在`xdm.mediaCollection.sessionDetails`中设置`friendlyName`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "Blinding Light",
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

调用`xdm.mediaCollection.sessionDetails`中包含`friendlyName`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "friendlyName": "Blinding Light",
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

将人类可读的名称作为第一个参数传递给`ADB.Media.createMediaObject`：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "Blinding Light",    // name (friendly name)
  "video-123",              // media ID
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

将人类可读的名称作为第一个参数传递给`ADBMobile.media.createMediaObject`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "Blinding Light",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

将人类可读的名称作为第一个参数传递给`adb_media_init_mediainfo`：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Blinding Light", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.name`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.name": "Blinding Light"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
