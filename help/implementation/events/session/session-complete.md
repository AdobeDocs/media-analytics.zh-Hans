---
title: 会话结束
description: 表示查看器已到达主内容的结尾。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

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

>[!TAB Roku]

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

>[!TAB 媒体收集API]

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`sessionComplete`帖子：

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
