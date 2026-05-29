---
title: 季
description: 设置情景内容的季编号，以便按季划分参与情况。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 9%

---


# 季

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**季**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[季](/help/reporting/dimensions/season.md)。*

>[!ENDSHADEBOX]

season变量是节目的季编号（通常是诸如`"2"`之类的字符串整数）。 为属于某个系列的内容设置此变量，以便按季节划分参与度。 与[节目](/help/implementation/variables/standard-metadata/show.md)和[剧集](/help/implementation/variables/standard-metadata/episode.md)配对，以获取完整的节集上下文。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.season` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.season`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.season` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`season`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        season: "2"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将季作为哈希映射参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.SEASON`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将季作为哈希映射参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.SEASON`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

使用`createMediaSession`在`sessionDetails`中设置`season`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "season": "2"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`season`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "season": "2"
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

使用`ADB.Media.VideoMetadataKeys.Season`在`contextData`对象中传递季：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Season] = "2";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.SEASON`在媒体对象的`StandardMediaMetadata`属性中设置季编号：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "2";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.season`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.season": "2"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
