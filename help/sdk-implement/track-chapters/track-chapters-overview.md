---
seo-title: 概述
title: 概述
uuid: 3fe32425-5e2a-4886-8fea-d91 d15671 bb0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 概述{#overview}

>[!IMPORTANT]
>
>以下说明为使用2.x SDK提供了实施指南。If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

章节和细分跟踪可用于自定义定义的媒体章节或区段。章节跟踪的一些常用用法是根据媒体内容定义自定义细分，或在广告片段之间定义内容细分。Chapter tracking is **not** required for core media tracking implementations.

章节跟踪包括章节开始、章节结束和章节跳过。您可以将媒体播放器API与自定义细分逻辑结合使用，以标识章节事件并填充所需和可选的章节变量。

## Player活动

### 在章节开始时

* 为章节创建章节对象实例 `chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* 调用 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 在章节上完成

* 调用 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 第章跳过章节

* 调用 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. 识别执行章节开始事件的时间，然后使用章节信息创建 `ChapterObject` 实例。

   以下是 `ChapterObject` 章节跟踪引用：

   >[!NOTE]
   >
   >仅当您计划跟踪章节时，才需要这些变量。

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 章节名称 | 是 |
   | `position` | 章节位置 | 是 |
   | `length` | 章节长度 | 是 |
   | `startTime` | 章节开始时间 | 是 |

1. 如果为章节添加了自定义元数据，请为元数据创建上下文数据变量。
1. 要开始跟踪章节播放，请在 `ChapterStart` 实例中调用 `MediaHeartbeat` 事件。
1. 当播放达到您通过自定义代码定义的章节结尾边界时，在 实例中调用 `ChapterComplete` 事件。`MediaHeartbeat`
1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请在 MediaHeartbeat 实例中调用 `ChapterSkip`。
1. 如果存在任何其他章节，请重复执行步骤 1 至 5。

以下示例代码将JavaScript2.x SDK用于HTML媒体播放器。您应将此代码与核心媒体播放代码结合使用。

```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 
```

## 验证 {#section_07EC2811BE3249249494596BFE9BF869}

### 章节开始

在单个章节播放开始时，将发送一个键调用：

* 心率章节开始(此调用包含其他章节元数据变量。)

### 章节结束

在章节边界结束时，会发送心率章节结束调用。

### 章节跳过

在跳过章节时，会发送心率章节跳过调用。
