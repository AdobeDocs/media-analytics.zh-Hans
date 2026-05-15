---
title: 播放
description: 表示媒体播放器已进入播放状态。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 17%

---


# 播放

播放事件表示媒体播放器状态已更改为播放。 在内容开始时、自动播放时以及播放器在暂停或缓冲后恢复时发送此包。 没有单独的恢复事件；[暂停开始](pause-start.md)或[缓冲开始](buffer-start.md)之后的播放事件用作恢复。

* **先决条件**： [会话开始](../session/session-start.md)
* **关联的量度**： [内容开始](/help/reporting/metrics/content-starts.md)

## Web SDK

使用`eventType: "media.play"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

在媒体播放器开始或继续播放时调用`trackPlay`。

**iOS (Swift)**

```swift
tracker.trackPlay()
```

**Android (Kotlin)**

```kotlin
tracker.trackPlay()
```

## Roku (BrightScript)

使用`eventType: "media.play"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用[播放](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

在媒体播放器开始或继续播放时调用`trackPlay`：

```javascript
tracker.trackPlay();
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`play`帖子：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
