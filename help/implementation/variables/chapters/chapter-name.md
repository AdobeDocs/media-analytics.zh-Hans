---
title: 章节名称
description: 设置每个章节的友好名称，以便章节级别报表可以按章节标题划分。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 8%

---


# 章节名称

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**章节名称**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[章节名称](/help/reporting/dimensions/chapter-name.md)。*

>[!ENDSHADEBOX]

章节名称变量是易于用户识别的章节标题（例如，`"Pilot Episode - Opening"`）。 在内容分为章节的每个`media.chapterStart`事件上设置它。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.chapter.friendlyName` |
| **XDM集合字段** | [`xdm.mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.chapter.friendlyName` |
| **必需** | 否 |
| **发送条件** | [章节开始](/help/implementation/events/chapters/chapter-start.md)，章节关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.chapterDetails`中设置`friendlyName`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将章节名称作为第一个(`name`)参数传递给`createChapterObject`。

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

将章节名称作为第一个(`name`)参数传递给`createChapterObject`。

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

为`media.chapterStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.chapterDetails`中设置`friendlyName`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.chapterDetails`中包含`friendlyName`的[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

将章节名称作为第一个参数传递给`ADB.Media.createChapterObject`：

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

将章节名称作为第一个参数(`name`)传递给`ADBMobile.media.createChapterObject`：

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

将章节名称作为第一个参数(`name`)传递给`adb_media_init_chapterinfo`：

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB 媒体收集API]

在`chapterStart` POST请求的`params`对象中包括`media.chapter.friendlyName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
