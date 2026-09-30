---
title: 会话结束
description: 在查看器放弃内容时立即关闭媒体会话。
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
source-wordcount: '323'
ht-degree: 5%
---

# 会话结束

会话结束事件会立即不可逆地关闭媒体跟踪会话。 会话结束是一个硬关闭；发送会话后，会话将被终止，并且其后无法跟踪任何进一步事件。 只有在您确定之后不会再发生其他事件时（例如，当播放器被销毁或页面卸载时），才使用会话结束。 在大多数情况下，更安全的做法是让会议自然过期，而不是冒险中断可能仍会到达的事件。 如果查看器完成内容，请改为调用[会话完成](session-complete.md)。

如果没有明确的会话结束，则会话会在没有事件发生10分钟或播放头没有移动30分钟后自动关闭。

>[!NOTE]
>
>您可以安全地为同一会话多次调用会话结束。 后端在第一个事件上关闭会话，并静默丢弃该会话ID的所有后续事件，包括第二个会话结束。 您无需防止在竞争条件下出现重复调用，例如30分钟超时在查看器关闭播放器的同时过期。

* **先决条件**： [会话开始](session-start.md)
* **关联的量度**：无

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

当查看器关闭播放器或导航离开时，调用`trackSessionEnd`。

```swift
tracker.trackSessionEnd()
```

>[!TAB Android]

当查看器关闭播放器或导航离开时，调用`trackSessionEnd`。

```kotlin
tracker.trackSessionEnd()
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

当查看器关闭播放器或导航离开时调用`trackSessionEnd`：

```javascript
tracker.trackSessionEnd();
```

>[!TAB Chromecast]

当查看器关闭播放器或导航离开时调用`trackSessionEnd`：

```javascript
ADBMobile.media.trackSessionEnd();
```

>[!TAB Roku 2.x]

当查看器关闭播放器或导航离开时调用`mediaTrackSessionEnd`：

```brightscript
ADBMobile().mediaTrackSessionEnd()
```

>[!TAB 媒体收集API]

向[事件终结点](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)发送`sessionEnd`帖子：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```

>[!ENDTABS]
