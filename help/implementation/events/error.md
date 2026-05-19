---
title: 错误
description: 表示媒体播放器遇到错误。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 16%

---


# 错误

错误事件表示媒体播放器遇到错误。 跟踪错误不会关闭会话。 如果错误导致无法继续播放，请在错误事件后调用[会话结束](session/session-end.md)。

* **先决条件**： [会话开始](session/session-start.md)
* **关联的量度**：[受错误影响的流](/help/reporting/metrics/error-impacted-streams.md)

`errorDetails.source`属性仅接受两个值： `player` （源自媒体播放器的错误）和`external` （来自CDN或网络等外部源的错误）。

## Web SDK

使用`eventType: "media.error"`和所需的`errorDetails`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

使用错误ID字符串调用`trackError`。

**iOS (Swift)**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android (Kotlin)**

```kotlin
tracker.trackError("media-error-001")
```

## Roku (BrightScript)

使用`eventType: "media.error"`和所需的`errorDetails`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

## Media Edge API

使用所需的`errorDetails`调用[error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用错误ID字符串调用`trackError`：

```javascript
tracker.trackError("media-error-001");
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`error`帖子：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```
