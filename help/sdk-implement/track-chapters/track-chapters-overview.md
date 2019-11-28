---
title: 概述
description: 如何使用 Media SDK 实施章节和区段跟踪。
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 概述{#overview}

>[!IMPORTANT]
>
>以下说明为使用 2.x SDK 进行实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

章节和区段跟踪适用于自定义的媒体章节或区段。章节跟踪的一些常见用例包括根据媒体内容定义自定义区段（例如，棒球赛的回合），或者定义不同广告时间之间的内容区段。对于核心媒体跟踪实施，章节跟踪&#x200B;**并非**&#x200B;必需项。

章节跟踪包括章节开始、章节结束和章节跳过。您可以结合自定义分段逻辑使用媒体播放器 API 来识别章节事件，并填充必需章节变量和可选章节变量。

## 播放器事件

### 在章节开始时

* 为章节创建章节对象实例 `chapterObject`
* 填充章节元数据 `chapterCustomMetadata`
* 调用 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 在章节结束时

* 调用 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 在章节跳过时

* 调用 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## 实施章节跟踪 {#implement-chapter-tracking}

1. 识别执行章节开始事件的时间，然后使用章节信息创建 `ChapterObject` 实例。

   以下是 `ChapterObject` 章节跟踪引用：

   >[!NOTE]
   >
   >只有在您打算跟踪章节的情况下，才需要使用这些变量。

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 章节名称 | 是 |
   | `position` | 章节位置 | 是 |
   | `length` | 章节长度 | 是 |
   | `startTime` | 章节开始时间 | 是 |

1. 如果为章节添加了自定义元数据，请为元数据创建上下文数据变量。
1. 要开始跟踪章节播放，请在 `ChapterStart` 实例中调用 `MediaHeartbeat` 事件。
1. 当播放达到您通过自定义代码定义的章节结尾边界时，在 `MediaHeartbeat` 实例中调用 `ChapterComplete` 事件。
1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请在 MediaHeartbeat 实例中调用 `ChapterSkip`。
1. 如果存在任何其他章节，请重复执行步骤 1 至 5。

以下代码示例为 HTML5 媒体播放器使用 JavaScript 2.x SDK。您应该结合使用此代码与核心媒体播放代码。

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

