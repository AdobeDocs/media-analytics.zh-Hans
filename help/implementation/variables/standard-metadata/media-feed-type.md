---
title: 媒体馈送类型
description: 根据区域或质量的不同，确定内容的广播馈送类型（例如，East-HD或West-SD）。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 7%

---


# 媒体馈送类型

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**媒体馈送类型**变量的数据收集。 有关相应的报表维度，请参阅[媒体馈送类型](/help/reporting/dimensions/media-feed-type.md)。*

>[!ENDSHADEBOX]

媒体馈送类型变量标识广播馈送（例如，`"East-HD"`、`"West-SD"`或`"4K"`）。 当通过多个区域或质量馈送交付相同内容，并且需要按馈送划分参与时，可使用它。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.feed` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.feed` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`feed`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        feed: "East-HD"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将馈送类型作为哈希映射参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.MEDIA_FEED`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将馈送类型作为哈希映射参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.MEDIA_FEED`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`在`sessionDetails`中设置`feed`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "feed": "East-HD"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`feed`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "feed": "East-HD"
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

使用`ADB.Media.VideoMetadataKeys.Feed`在`contextData`对象中传递馈送：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Feed] = "East-HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.FEED`在媒体对象的`StandardMediaMetadata`属性中设置媒体馈送类型：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "East-HD";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在调用`mediaTrackSessionStart`之前，使用`MEDIA_VideoMetadataKeyFEED`在媒体对象的标准元数据中设置媒体馈送类型：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyFEED] = "East-HD"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.feed`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.feed": "East-HD"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
