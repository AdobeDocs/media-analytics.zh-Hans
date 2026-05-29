---
title: 广告结束
description: 表示单个广告已完成播放。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---


# 广告结束

广告结束事件表示单个广告已完成播放。 在广告播放到结束之后发送。 如果查看器跳过广告，请改为发送[广告跳过](ad-skip.md)。

* **先决条件**： [会话开始](../session/session-start.md)，[广告时间开始](ad-break-start.md)，[广告开始](ad-start.md)
* **关联的量度**：[[!UICONTROL 广告完成]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>此事件必须由`adBreakStart`和`adBreakComplete`书档包围，即使播放了单个广告也是如此。 如果没有这些书挡，广告事件将被忽略，广告持续时间将被计为主内容持续时间。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.adComplete"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

>[!TAB iOS]

使用`AdComplete`事件类型调用`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

使用`AdComplete`事件类型调用`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku]

使用`eventType: "media.adComplete"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

>[!TAB Media Edge API]

调用[adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
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

使用`AdComplete`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

使用`AdComplete`事件类型调用`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB 媒体收集API]

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`adComplete`帖子：

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
