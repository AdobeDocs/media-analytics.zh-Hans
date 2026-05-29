---
title: 内容播放器名称
description: 设置播放器名称以标识呈现内容的播放器。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---


# 内容播放器名称

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**内容播放器名称**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[内容播放器名称](/help/reporting/dimensions/content-player-name.md)。*

>[!ENDSHADEBOX]

内容播放器名称变量标识呈现内容的播放器（例如，`HTML5 Player`、`Brightcove`或`Roku Player`）。 所有流媒体实施都需要它，并且必须在会话开始时设置。 该值用在内容播放器名称维度中，以比较同一资产中不同播放器之间的参与度和质量。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.playerName` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.playerName` |
| **必需** | 是 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`playerName`：

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

创建跟踪器时，使用`MediaConstants.TrackerConfig.PLAYER_NAME`通过跟踪器配置设置播放器名称。 播放器名称不是媒体对象的一部分。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

创建跟踪器时，使用`MediaConstants.TrackerConfig.PLAYER_NAME`通过跟踪器配置设置播放器名称。 播放器名称不是媒体对象的一部分。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku]

调用`createMediaSession`时，在`xdm.mediaCollection.sessionDetails`中设置`playerName`：

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

调用`xdm.mediaCollection.sessionDetails`中包含`playerName`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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

在创建跟踪器之前，在`ADB.MediaConfig`上设置播放器名称：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

调用`trackSessionStart`时传递播放器名称作为标准元数据键：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.playerName": "Chromecast Player" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.playerName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
