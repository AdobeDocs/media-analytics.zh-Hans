---
title: 节目
description: 为属于某个系列的视频内容设置节目名称，以便剧集可以汇总到报表中的单个项目中。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 8%

---


# 节目

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**节目**变量的数据收集。 查看对应的报表维度的[显示](/help/reporting/dimensions/show.md)。*

>[!ENDSHADEBOX]

节目变量是节目或系列的名称（例如，`"Blinding Light"`或`"Coastline Mysteries"`）。 在内容属于某个系列的每个会话上设置它，以便跨多季的集合并到节目维度中的单个行项目。 对于不属于某个系列的一次性内容，请保留此设置。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.show` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.show` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`show`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        show: "Blinding Light"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将显示名称作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.SHOW`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将显示名称作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.SHOW`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

使用`createMediaSession`在`sessionDetails`中设置`show`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "show": "Blinding Light"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`show`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "show": "Blinding Light"
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

使用`ADB.Media.VideoMetadataKeys.Show`在`contextData`对象中传递节目名称：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

调用`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.SHOW`在媒体对象的`StandardMediaMetadata`属性中设置显示名称：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "Blinding Light";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.show`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.show": "Blinding Light"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
