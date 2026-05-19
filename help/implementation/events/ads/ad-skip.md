---
title: 广告跳过
description: 表示查看器跳过了广告。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# 广告跳过

广告跳过事件表示查看器在广告完成之前跳过了该广告。 当查看者选择跳过按钮时发送它。 如果广告播放到结束，请改为发送[广告结束](ad-complete.md)。

* **先决条件**： [会话开始](../session/session-start.md)，[广告时间开始](ad-break-start.md)，[广告开始](ad-start.md)
* **关联的量度**：无

>[!IMPORTANT]
>
>此事件必须由`adBreakStart`和`adBreakComplete`书档包围，即使播放了单个广告也是如此。 如果没有这些书挡，广告事件将被忽略，广告持续时间将被计为主内容持续时间。

## Web SDK

使用`eventType: "media.adSkip"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## Mobile SDK

使用`AdSkip`事件类型调用`trackEvent`。

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku (BrightScript)

使用`eventType: "media.adSkip"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## Media Edge API

调用[adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

使用`AdSkip`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## 媒体收集 API

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`adSkip`帖子：

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
