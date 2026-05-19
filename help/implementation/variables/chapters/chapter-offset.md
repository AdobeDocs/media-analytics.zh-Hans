---
title: 章节偏移
description: 设置章节在内容中的偏移，以秒为单位，从开始时间算起。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 12%

---


# 章节偏移

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**章节偏移**&#x200B;变量的数据收集。 查看相应报表维度的[章节偏移](/help/reporting/dimensions/chapter-offset.md)。*

>[!ENDSHADEBOX]

章节偏移变量是章节在内容中的偏移，以秒为单位，从开始起算。 第一个章节通常具有偏移`0`；后续章节具有与其播放头开始时间匹配的偏移。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.chapter.offset` |
| **XDM集合字段** | [`mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.chapter.offset` |
| **必需** | 否(Mobile SDK)；是(Edge、Media Collection API) |
| **发送条件** | [章节开始](/help/implementation/events/chapters/chapter-start.md)，章节关闭 |

## Web SDK

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`mediaCollection.chapterDetails`中设置`offset`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

将偏移量（以秒为单位）作为第四个参数(`startTime`)传递给`createChapterObject`。

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

为`media.chapterStart`调用`sendMediaEvent`时，在`mediaCollection.chapterDetails`中设置`offset`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

## Media Edge API

调用`mediaCollection.chapterDetails`中包含`offset`的[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

## Media SDK

将偏移作为第四个参数传递给`ADB.Media.createChapterObject`：

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## 媒体收集 API

在`chapterStart` POST请求的`params`对象中包括`media.chapter.offset`：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。
