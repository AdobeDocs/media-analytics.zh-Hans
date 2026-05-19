---
title: 广告时间结束
description: 表示广告时间中的所有广告都已结束。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 16%

---


# 广告时间结束

广告时间结束事件表示广告时间中的所有广告都已结束（已完成或跳过）。 它会关闭[广告时间开始](ad-break-start.md)打开的广告时间。

* **先决条件**： [会话开始](../session/session-start.md)，[广告时间开始](ad-break-start.md)
* **关联的量度**：无

>[!IMPORTANT]
>
>每个`adBreakStart`必须有匹配的`adBreakComplete`。 如果没有结束书挡，广告事件将被忽略，广告持续时间将归因于主内容。

## Web SDK

使用`eventType: "media.adBreakComplete"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

使用`AdBreakComplete`事件类型调用`trackEvent`。

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

## Roku (BrightScript)

使用`eventType: "media.adBreakComplete"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## Media Edge API

调用[adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
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

使用`AdBreakComplete`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`adBreakComplete`帖子：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```
