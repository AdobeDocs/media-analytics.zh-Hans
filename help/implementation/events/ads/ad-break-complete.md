---
title: 广告时间结束
description: 表示广告时间中的所有广告都已结束。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%
---

# 广告时间结束

广告时间结束事件表示广告时间中的所有广告都已结束（已完成或跳过）。 它会关闭[广告时间开始](ad-break-start.md)打开的广告时间。

* **先决条件**： [会话开始](../session/session-start.md)，[广告时间开始](ad-break-start.md)
* **关联的量度**：无

>[!IMPORTANT]
>
>每个`adBreakStart`必须有匹配的`adBreakComplete`。 如果没有结束书挡，广告事件将被忽略，广告持续时间将归因于主内容。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

使用`AdBreakComplete`事件类型调用`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

使用`AdBreakComplete`事件类型调用`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`AdBreakComplete`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

使用`AdBreakComplete`事件类型调用`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Roku 2.x]

使用`MEDIA_AD_BREAK_COMPLETE`事件类型调用`mediaTrackEvent`：

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_COMPLETE)
```

>[!TAB 媒体收集API]

向[事件终结点](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)发送`adBreakComplete`帖子：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
