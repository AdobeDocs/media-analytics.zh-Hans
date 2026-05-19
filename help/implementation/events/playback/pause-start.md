---
title: 暂停开始
description: 表示用户暂停了媒体播放。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 19%

---


# 暂停开始

暂停开始事件表示用户暂停了播放。 没有单独的恢复事件；恢复播放时发送[播放](play.md)事件。

* **先决条件**： [会话开始](../session/session-start.md)
* **关联的量度**： [暂停事件](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>没有恢复事件类型。 在`pauseStart`之后发送[`play`](play.md)事件时推断为恢复。

## Web SDK

使用`eventType: "media.pauseStart"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

## Mobile SDK

当用户暂停播放时，调用`trackPause`。

**iOS (Swift)**

```swift
tracker.trackPause()
```

**Android (Kotlin)**

```kotlin
tracker.trackPause()
```

## Roku (BrightScript)

使用`eventType: "media.pauseStart"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

## Media Edge API

调用[pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

当用户暂停播放时调用`trackPause`：

```javascript
tracker.trackPause();
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`pauseStart`帖子：

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```
