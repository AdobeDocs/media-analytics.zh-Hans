---
title: 内容继续
description: 标记一个会话，该会话可恢复之前中断的播放，以便后端计算内容恢复事件。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 6%

---


# 内容继续

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**内容继续**&#x200B;变量的数据收集。 查看[[!UICONTROL 内容履历]](/help/reporting/metrics/content-resumes.md)以了解相应的报表量度。*

>[!ENDSHADEBOX]

内容恢复变量标记恢复之前中断的播放的会话。 将其设置为`media.sessionStart`，以便后端计算会话的[[!UICONTROL 内容恢复]](/help/reporting/metrics/content-resumes.md)事件并将其从新流计数中排除。 对于直接API和Edge API实施，客户端负责检测恢复的会话（例如，在缓冲、暂停或停止超过30分钟后）并相应地设置此标记。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.resume` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | 不适用 |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md) |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

为恢复的会话调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`内将`hasResume`设置为`true`：

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
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

将恢复标志作为媒体对象可选配置包的一部分传递到`trackSessionStart`。 使用`MediaConstants.MediaObjectKey.RESUMED`键。

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

将恢复标志作为媒体对象可选配置包的一部分传递到`trackSessionStart`。 使用`MediaConstants.MediaObjectKey.RESUMED`键。

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

为恢复的会话调用`createMediaSession`时，在`xdm.mediaCollection.sessionDetails`内将`hasResume`设置为`true`：

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
            "playhead": 60
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中`hasResume`设置为`true`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

在调用`trackSessionStart`之前，在媒体信息对象上设置`RESUMED`键：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，在媒体信息对象上设置`MediaResumed`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在调用`mediaTrackSessionStart`之前，在媒体对象上设置`resumed`键：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)
mediaInfo.resumed = true

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.resume`：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
