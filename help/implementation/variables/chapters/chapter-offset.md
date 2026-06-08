---
title: 章节偏移
description: 设置章节在内容中的偏移，以秒为单位，从开始时间算起。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 6%

---


# 章节偏移

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**章节偏移**&#x200B;变量的数据收集。 查看相应报表维度的[章节偏移](/help/reporting/dimensions/chapter-offset.md)。*

>[!ENDSHADEBOX]

章节偏移变量是章节在内容中的偏移，以秒为单位，从开始起算。 第一个章节通常具有偏移`0`；后续章节具有与其播放头开始时间匹配的偏移。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.chapter.offset` |
| **XDM集合字段** | [`xdm.mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.chapter.offset` |
| **必需** | 否(Mobile SDK)；是(Edge、Media Collection API) |
| **发送条件** | [章节开始](/help/implementation/events/chapters/chapter-start.md)，章节关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.chapterDetails`中设置`offset`：

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

>[!TAB iOS]

将偏移量（以秒为单位）作为第四个参数(`startTime`)传递给`createChapterObject`。

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

将偏移量（以秒为单位）作为第四个参数(`startTime`)传递给`createChapterObject`。

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

为`media.chapterStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.chapterDetails`中设置`offset`：

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

>[!TAB Media Edge API]

调用`xdm.mediaCollection.chapterDetails`中包含`offset`的[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)终结点：

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

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

将章节偏移量（以秒为单位）作为第四个参数(`startTime`)传递给`ADBMobile.media.createChapterObject`：

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime (seconds from content start)
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

将章节偏移量（以秒为单位）作为第四个参数(`startTime`)传递给`adb_media_init_chapterinfo`：

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB 媒体收集API]

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

>[!ENDTABS]
