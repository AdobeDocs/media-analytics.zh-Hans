---
title: 章节结束
description: 表示章节区段已完成播放。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# 章节结束

章节结束事件表示章节结束播放。 当查看者到达章节结尾时发送该报告。 如果查看器跳过章节，请改为发送[章节跳过](chapter-skip.md)。

* **先决条件**： [会话开始](../session/session-start.md)，[章节开始](chapter-start.md)
* **关联的量度**： [章节完成](/help/reporting/metrics/chapter-completes.md)

## Web SDK

使用`eventType: "media.chapterComplete"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

使用`ChapterComplete`事件类型调用`trackEvent`。

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku (BrightScript)

使用`eventType: "media.chapterComplete"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

## Media Edge API

调用[chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用`ChapterComplete`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`chapterComplete`帖子：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
