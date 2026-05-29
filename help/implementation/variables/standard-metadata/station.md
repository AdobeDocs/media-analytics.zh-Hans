---
title: 电台/电视台
description: 为音频广播内容设置广播电台名称或ID。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# 电台/电视台

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**工作站**变量的数据收集。 查看[工作站](/help/reporting/dimensions/station.md)以了解相应的报表维度。*

>[!ENDSHADEBOX]

电台变量是广播音频内容的广播电台的名称或ID（例如，`"NPR"`或`"WXYZ-FM"`）。 使用它来比较联合网络中不同站点的参与情况。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.station` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.station` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`station`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        station: "NPR"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将工作站作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.AudioMetadataKeys.STATION`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将工作站作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.AudioMetadataKeys.STATION`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

使用`createMediaSession`在`sessionDetails`中设置`station`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "station": "NPR"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`station`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "station": "NPR"
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

在`contextData`对象中使用`ADB.Media.AudioMetadataKeys.Station`传递工作站：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Station] = "NPR";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，使用`ADBMobile.media.AudioMetadataKeys.STATION`在媒体对象的`StandardMediaMetadata`属性中设置工作站名称：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "NPR";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.station`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.station": "NPR"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
