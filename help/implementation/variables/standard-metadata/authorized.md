---
title: 已授权
description: 将会话标记为通过Adobe Pass进行身份验证，以便将其计入授权事件。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 15%

---


# 已授权

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Authorized**&#x200B;变量的数据收集。 查看[Authorized](/help/reporting/metrics/authorized.md)以获取相应的报表量度。*

>[!ENDSHADEBOX]

授权变量会标记其用户已通过Adobe Pass/TV-Everywhere获得授权的会话。 在确认授权时将其设置为`"TRUE"`；否则，请将其保留为未设置。 与[MVPD](/help/implementation/variables/standard-metadata/mvpd.md)配对，以中断提供商的身份验证。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.pass.auth` |
| **XDM集合字段** | [`mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.pass.auth` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.sessionDetails`中设置`authorized`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

将授权标志作为哈希映射参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.AUTHORIZED`。

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

使用`createMediaSession`在`sessionDetails`中设置`authorized`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用`mediaCollection.sessionDetails`中包含`authorized`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

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
          "authorized": "TRUE"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

使用`ADB.Media.VideoMetadataKeys.Authorized`在`contextData`对象中传递授权标志：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

## 媒体收集 API

在`params`对象中包括`media.pass.auth`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。
