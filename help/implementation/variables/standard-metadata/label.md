---
title: 标签
description: 设置发布音频内容的录制标签。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 9%

---


# 标签

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**标签**变量的数据收集。 查看相应报表维度的[标签](/help/reporting/dimensions/label.md)。*

>[!ENDSHADEBOX]

label变量是发布音频内容的录制标签的名称（例如，`"Capitol Records"`）。 使用它来比较音乐或播客目录中不同标签之间的参与度。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.label` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.label` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`label`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        label: "Capitol Records"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将标签作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.AudioMetadataKeys.LABEL`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将标签作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.AudioMetadataKeys.LABEL`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`在`sessionDetails`中设置`label`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "label": "Capitol Records"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`label`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "label": "Capitol Records"
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

使用`ADB.Media.AudioMetadataKeys.Label`在`contextData`对象中传递标签：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Label] = "Capitol Records";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，使用`ADBMobile.media.AudioMetadataKeys.LABEL`在媒体对象的`StandardMediaMetadata`属性中设置记录标签：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "Capitol Records";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在调用`mediaTrackSessionStart`之前，使用`MEDIA_AudioMetadataKeyLABEL`在媒体对象的标准元数据中设置记录标签：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyLABEL] = "Capitol Records"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.label`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.label": "Capitol Records"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
