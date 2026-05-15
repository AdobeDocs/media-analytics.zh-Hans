---
title: 缓冲开始
description: 表示媒体播放器进入缓冲状态的信号。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 15%

---


# 缓冲开始

缓冲开始事件表示媒体播放器进入缓冲状态。

* **先决条件**： [会话开始](../session/session-start.md)
* **关联的量度**： [缓冲事件](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**基于XDM的API（Web SDK、Roku、Media Edge API、媒体收集API）：**&#x200B;没有缓冲恢复事件类型；在`bufferStart`之后发送[`play`](play.md)事件时推断为缓冲结束。
>
>**Mobile SDK：**&#x200B;在播放器退出缓冲时调用`trackEvent(BufferComplete)`，然后调用`trackPlay()`以继续播放。

## Web SDK

使用`eventType: "media.bufferStart"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

当播放器进入缓冲状态时，使用`BufferStart`调用`trackEvent`；当播放器退出时，使用`BufferComplete`调用。

**iOS (Swift)**

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

## Roku (BrightScript)

使用`eventType: "media.bufferStart"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge API

调用[bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用`BufferStart`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`bufferStart`帖子：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```
