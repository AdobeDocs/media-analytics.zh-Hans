---
title: 会话结束
description: 表示查看器已到达主内容的结尾。
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
source-wordcount: '188'
ht-degree: 7%
---

# 会话结束

会话结束事件表示查看器已到达主内容的结尾。 它不会立即关闭会话；会话将保持打开状态，直到它自然过期。 如果要立即关闭会话，请改为调用[会话结束](session-end.md)。

* **先决条件**： [会话开始](session-start.md)
* **关联的量度**： [[!UICONTROL 内容完成]](/help/reporting/metrics/content-completes.md)

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.sessionComplete"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

>[!TAB iOS]

当媒体播放器到达内容结尾时，调用`trackComplete`。

```swift
tracker.trackComplete()
```

>[!TAB Android]

当媒体播放器到达内容结尾时，调用`trackComplete`。

```kotlin
tracker.trackComplete()
```

>[!TAB Roku Edge]

使用`eventType: "media.sessionComplete"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

>[!TAB Media Edge API]

调用[sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
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

当媒体播放器到达内容结尾时，调用`trackComplete`：

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

当媒体播放器到达内容结尾时，调用`trackComplete`：

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

当媒体播放器到达内容结尾时，调用`mediaTrackComplete`：

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB 媒体收集API]

向[事件终结点](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)发送`sessionComplete`帖子：

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
