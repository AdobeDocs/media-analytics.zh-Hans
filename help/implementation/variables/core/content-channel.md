---
title: 内容渠道
description: 设置通道以标识播放内容的分发站点、网络或属性。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 6%

---


# 内容渠道

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**内容渠道**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[内容渠道](/help/reporting/dimensions/content-channel.md)。*

>[!ENDSHADEBOX]

内容频道变量可标识播放内容的分发站点、网络或属性。 所有流媒体实施都需要此参数。 可接受任何字符串。 典型值包括网络名称、站点路径的一部分或内部属性标识符。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.channel` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.channel` |
| **必需** | 是 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`channel`：

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

创建跟踪器时，使用`MediaConstants.TrackerConfig.CHANNEL`通过跟踪器配置设置频道。 频道不是媒体对象的一部分。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

创建跟踪器时，使用`MediaConstants.TrackerConfig.CHANNEL`通过跟踪器配置设置频道。 频道不是媒体对象的一部分。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

调用`createMediaSession`时，在`xdm.mediaCollection.sessionDetails`中设置`channel`：

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

调用`xdm.mediaCollection.sessionDetails`中包含`channel`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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

在创建跟踪器之前，在`ADB.MediaConfig`上设置频道：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

调用`trackSessionStart`时传递`channel`作为标准元数据键：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.channel": "Sports" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

在`ADBMobileConfig.json`的`mediaHeartbeat`部分中设置`channel`。 渠道是配置值，而不是每个会话的值：

```json
"mediaHeartbeat": {
  "channel": "Sports"
}
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.channel`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
