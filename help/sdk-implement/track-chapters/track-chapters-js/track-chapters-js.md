---
title: 了解如何使用JavaScript 2.x跟踪章节和区段
description: 了解如何在浏览器应用程序(JS)中使用Media SDK实施章节和区段跟踪。
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
exl-id: 9964ec0c-cce9-4ccc-bd26-a2b3fcdc3e28
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 84%

---

# 使用JavaScript 2.x跟踪章节和区段{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>以下说明为使用 2.x SDK 进行实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

1. 识别执行章节开始事件的时间，然后使用章节信息创建 `ChapterObject` 实例。

   `ChapterObject` 章节跟踪引用：

   >[!NOTE]
   >
   >只有在您打算跟踪章节的情况下，才需要使用这些变量。

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 章节名称 | 是 |
   | `position` | 章节位置 | 是 |
   | `length` | 章节长度 | 是 |
   | `startTime` | 章节开始时间 | 是 |

   章节对象：

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. 如果为章节添加了自定义元数据，请为该元数据创建上下文数据变量：

   ```js
   var chapterCustomMetadata = {
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info"
   };
   ```

1. 要开始跟踪章节播放，请在 `ChapterStart` 实例中调用 `MediaHeartbeat` 事件：

   ```js
   _onChapterStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata);
   };
   ```

1. 当播放到达您通过自定义代码定义的章节结尾边界时，在 `ChapterComplete` 实例中调用 `MediaHeartbeat` 事件：

   ```js
   _onChapterComplete = function() {
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
   };
   ```

1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请在 MediaHeartbeat 实例中调用 `ChapterSkip` 事件：

   ```js
   _onChapterSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
   };
   ```

1. 如果存在任何其他章节，请重复执行步骤 1 至 5。
