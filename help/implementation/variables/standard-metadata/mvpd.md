---
title: MVPD
description: 当用户通过Adobe Pass进行身份验证时，设置多频道视频节目分发商。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 8%

---


# MVPD

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**MVPD**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[MVPD](/help/reporting/dimensions/mvpd.md)。*

>[!ENDSHADEBOX]

MVPD （多频道视频节目分发商）变量是用户通过身份验证的有线电视、卫星电视或虚拟MVPD提供商（例如，`"Comcast"`、`"DirecTV"`或`"YouTubeTV"`）。 当内容通过Adobe Pass或TV-Everywhere身份验证进行封闭时，设置此项。 与[Authorized](/help/implementation/variables/standard-metadata/authorized.md)配对，以跟踪哪些会话已完成身份验证。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.pass.mvpd` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.pass.mvpd` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`mvpd`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将MVPD作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.MVPD`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将MVPD作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.MVPD`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`在`sessionDetails`中设置`mvpd`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`mvpd`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "mvpd": "Comcast"
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

使用`ADB.Media.VideoMetadataKeys.MVPD`在`contextData`对象中传递MVPD：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.MVPD`在MVPD对象的`StandardMediaMetadata`属性中设置媒体对象：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "Comcast";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在调用`mediaTrackSessionStart`之前，使用`MEDIA_VideoMetadataKeyMVPD`在媒体对象的标准元数据中设置MVPD：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyMVPD] = "Comcast"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.pass.mvpd`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
