---
title: 章节跳过
description: 表示查看器跳过了一个章节。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 10%

---


# 章节跳过

章节跳过事件表示查看器在章节结束前跳过了该章节。 当查看者导航超过章节边界而不观看它完成时发送它。 如果章节播放到结尾，请发送[章节结束](chapter-complete.md)。

* **先决条件**： [会话开始](../session/session-start.md)，[章节开始](chapter-start.md)
* **关联的量度**：无

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.chapterSkip"`调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

使用`ChapterSkip`事件类型调用`trackEvent`。

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

使用`ChapterSkip`事件类型调用`trackEvent`。

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Roku Edge]

使用`eventType: "media.chapterSkip"`调用`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

>[!TAB Media Edge API]

调用[chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip)终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
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

使用`ChapterSkip`事件类型调用`trackEvent`：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB Chromecast]

使用`ChapterSkip`事件类型调用`trackEvent`：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB Roku 2.x]

使用`MEDIA_CHAPTER_SKIP`事件类型调用`mediaTrackEvent`：

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_SKIP)
```

>[!TAB 媒体收集API]

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`chapterSkip`帖子：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
