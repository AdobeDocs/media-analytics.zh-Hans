---
seo-title: 概述
title: 概述
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 概述{#overview}

>[!IMPORTANT]
>
>以下说明提供了使用2.x SDK实施的指导。 If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

章节和细分跟踪适用于自定义媒体章节或细分。 章节跟踪的一些常见用途是根据媒体内容（如棒球引擎）定义自定义区段，或定义广告分段之间的内容区段。 Chapter tracking is **not** required for core media tracking implementations.

章节跟踪包括章节开始、章节结束和章节跳过。您可以将媒体播放器API与自定义细分逻辑结合使用，以识别章节事件并填充所需的和可选的章节变量。

## 播放器事件

### 章节开始

* 为章节创建章节对象实例 `chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* 调用 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 论章节的完成

* 调用 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 章节跳过

* 调用 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## 实现章节跟踪 {#implement-chapter-tracking}

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

以下示例代码将JavaScript 2.x SDK用于HTML5媒体播放器。 应将此代码与核心媒体播放代码一起使用。

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

