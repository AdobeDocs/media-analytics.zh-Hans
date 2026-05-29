---
title: 媒体下载标志
description: 将会话标记为已下载的离线播放，以便与流式传输会话分开报告。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 6%

---


# 媒体下载标志

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Media downloaded flag**&#x200B;变量的数据收集。 查看相应报表维度的[下载的媒体](/help/reporting/dimensions/media-downloaded-flag.md)。*

>[!ENDSHADEBOX]

媒体已下载标记指示会话是先前下载的离线内容的播放，而不是来自Internet的实时流的播放。 在初始化跟踪器(Mobile SDK)时设置它，或将其包含在`sessionStart`有效负载（Edge/媒体收集API）中。 使用此标记可在报告中将离线播放与流式处理会话分开。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.downloaded` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.downloaded` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`内将`isDownloaded`设置为`true`：

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
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

使用`MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`创建跟踪器时，在跟踪器配置中设置下载内容标志。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

使用`MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`创建跟踪器时，在跟踪器配置中设置下载内容标志。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

>[!TAB Roku]

调用`createMediaSession`时，在`xdm.mediaCollection.sessionDetails`内将`isDownloaded`设置为`true`：

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
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

在设备返回联机状态后调用[已下载](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded)终结点，在`mediaDownloadedEvents`内批量处理完整的脱机会话。 Adobe自动将`isDownloaded`设置为`true`并分配会话ID；请勿在有效负载中包含任一会话ID。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

在创建跟踪器之前在`ADB.MediaConfig`上设置`downloadedContent`：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，在媒体信息对象上设置`MediaDownloaded`：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaDownloaded] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.downloaded`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
