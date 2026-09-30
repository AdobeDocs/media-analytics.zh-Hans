---
title: 暂停开始
description: 表示用户暂停了媒体播放。
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
source-wordcount: '159'
ht-degree: 9%
---

# 暂停开始

暂停开始事件表示用户暂停了播放。 没有单独的恢复事件；恢复播放时发送[播放](play.md)事件。

* **先决条件**： [会话开始](../session/session-start.md)
* **关联的量度**： [[!UICONTROL 暂停事件]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>没有恢复事件类型。 在`pauseStart`之后发送[`play`](play.md)事件时推断为恢复。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

当用户暂停播放时，调用`trackPause`。

```swift
tracker.trackPause()
```

>[!TAB Android]

当用户暂停播放时，调用`trackPause`。

```kotlin
tracker.trackPause()
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

当用户暂停播放时调用`trackPause`：

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

当用户暂停播放时调用`trackPause`：

```javascript
ADBMobile.media.trackPause();
```

>[!TAB Roku 2.x]

当用户暂停播放时调用`mediaTrackPause`：

```brightscript
ADBMobile().mediaTrackPause()
```

>[!TAB 媒体收集API]

向[事件终结点](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)发送`pauseStart`帖子：

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
