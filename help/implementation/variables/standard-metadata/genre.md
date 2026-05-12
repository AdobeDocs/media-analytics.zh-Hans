---
title: 流派
description: 将内容流派设置为以逗号分隔的字符串。 多流派内容在报告中的行项目之间拆分。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 13%

---


# 流派

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**流派**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[流派](/help/reporting/dimensions/genre.md)。*

>[!ENDSHADEBOX]

类型变量是制作者定义的内容类型（例如，`"Drama"`、`"Comedy"`或`"Drama,Action"`）。 当内容适合多种类型时，请使用逗号分隔多个值。 在报表中，列表变量将每个值拆分为单独的行项目，每个行项目具有相同的量度权重。

>[!NOTE]
>
>在报告管道中，流派值显示为`mediaReporting.sessionDetails.genreList`（列表字段）。 较旧的`mediaReporting.sessionDetails.genre`路径仍然有效，但建议使用`genreList`。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.genre` |
| **XDM集合字段** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必需** | 否 |
| **发送条件** | 会话开始，会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.sessionDetails`中设置`genre`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

将类型字符串作为哈希映射参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.GENRE`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`在`sessionDetails`中设置`genre`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用`mediaCollection.sessionDetails`中包含`genre`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.Genre`在`contextData`对象中传递流派：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## 媒体收集 API

在`params`对象中包括`media.genre`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
