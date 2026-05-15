---
title: 标签
description: 设置发布音频内容的录制标签。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 16%

---


# 标签

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**标签**&#x200B;变量的数据收集。 查看相应报表维度的[标签](/help/reporting/dimensions/label.md)。*

>[!ENDSHADEBOX]

label变量是发布音频内容的录制标签的名称（例如，`"Capitol Records"`）。 使用它来比较音乐或播客目录中不同标签之间的参与度。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.label` |
| **XDM集合字段** | [`mediaCollection.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.label` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.sessionDetails`中设置`label`：

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

## Mobile SDK

将标签作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.AudioMetadataKeys.LABEL`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## Media Edge API

调用`mediaCollection.sessionDetails`中包含`label`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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

## Media SDK

使用`ADB.Media.AudioMetadataKeys.Label`在`contextData`对象中传递标签：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Label] = "Capitol Records";

tracker.trackSessionStart(mediaInfo, contextData);
```

## 媒体收集 API

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
