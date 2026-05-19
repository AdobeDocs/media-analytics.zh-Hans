---
title: 会话结束
description: 在查看器放弃内容时立即关闭媒体会话。
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 11%

---


# 会话结束

会话结束事件会立即不可逆地关闭媒体跟踪会话。 会话结束是硬关闭 — 一旦发送，会话即被终止，并且其下无法跟踪任何进一步的事件。 只有在您确定之后不会再发生其他事件时（例如，当播放器被销毁或页面卸载时），才使用会话结束。 在大多数情况下，更安全的做法是让会议自然过期，而不是冒险中断可能仍会到达的事件。 如果查看器完成内容，请改为调用[会话完成](session-complete.md)。

如果没有明确的会话结束，则会话会在没有事件发生10分钟或播放头没有移动30分钟后自动关闭。

* **先决条件**： [会话开始](session-start.md)
* **关联的量度**：无

## Web SDK

使用`eventType: "media.sessionEnd"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

当查看器关闭播放器或导航离开时，调用`trackSessionEnd`。

**iOS (Swift)**

```swift
tracker.trackSessionEnd()
```

**Android (Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

使用`eventType: "media.sessionEnd"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge API

调用[sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
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

当查看器关闭播放器或导航离开时调用`trackSessionEnd`：

```javascript
tracker.trackSessionEnd();
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`sessionEnd`帖子：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
