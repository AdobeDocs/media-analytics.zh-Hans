---
title: 章节结束
description: 表示章节区段已完成播放。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---


# 章节结束

章节结束事件表示章节结束播放。 当查看者到达章节结尾时发送该报告。 如果查看器跳过章节，请改为发送[章节跳过](chapter-skip.md)。

* **先决条件**： [会话开始](../session/session-start.md)，[章节开始](chapter-start.md)
* **关联的量度**： [[!UICONTROL 章节完成]](/help/reporting/metrics/chapter-completes.md)

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

使用`ChapterComplete`事件类型调用`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

>[!TAB Android]

使用`ChapterComplete`事件类型调用`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`ChapterComplete`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

>[!TAB Chromecast]

使用`ChapterComplete`事件类型调用`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
```

>[!TAB Roku 2.x]

使用`MEDIA_CHAPTER_COMPLETE`事件类型调用`mediaTrackEvent`：

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_COMPLETE)
```

>[!TAB 媒体收集API]

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`chapterComplete`帖子：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```

>[!ENDTABS]
