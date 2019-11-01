---
title: 在 Android 中跟踪章节和区段
description: 本主题介绍在Android上使用Media SDK实施章节和细分跟踪。
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Android 中跟踪章节和区段{#track-chapters-and-segments-on-android}

>[!IMPORTANT]
>
>以下说明提供了使用2.x SDK实施的指导。 If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 实现章节跟踪

1. 识别执行章节开始事件的时间，然后使用章节信息创建 `ChapterObject` 实例。

   `ChapterObject` 章节跟踪参考：

   >[!NOTE]
   >
   >仅当您计划跟踪章节时，才需要这些变量。

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 章节名称 | 是 |
   | `position` | 章节位置 | 是 |
   | `length` | 章节长度 | 是 |
   | `startTime` | 章节开始时间 | 是 |

   章节对象：

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. 如果为章节添加了自定义元数据，请为该元数据创建上下文数据变量：

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>(); 
   chapterMetadata.put("segmentType", "Sample Segment Type"); 
   chapterMetadata.put("segmentName", "Sample Segment Name"); 
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. 要开始跟踪章节播放，请在 `ChapterStart` 实例中调用 `MediaHeartbeat` 事件：

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata); 
   }
   ```

1. 当播放到达您通过自定义代码定义的章节结尾边界时，在 `ChapterComplete` 实例中调用 `MediaHeartbeat` 事件：

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
   }
   ```

1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请在 MediaHeartbeat 实例中调用 `ChapterSkip` 事件：

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
   }
   ```

1. 如果存在任何其他章节，请重复执行步骤 1 至 5。

