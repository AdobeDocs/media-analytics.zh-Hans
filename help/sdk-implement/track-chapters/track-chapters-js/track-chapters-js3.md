---
title: 了解如何使用JavaScript 3.x跟踪章节和区段
description: 了解如何在浏览器应用程序(JS)中使用Media SDK实施章节和区段跟踪。
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 64%

---

# 使用JavaScript 3.x跟踪章节和区段{#track-chapters-and-segments-on-javascript}

以下说明为使用 3.x SDK 进行实施提供了指南。

>[!IMPORTANT]
>
> 如果您实施的是SDK的先前版本，可以在此处下载开发人员指南：[下载SDK。](/help/sdk-implement/download-sdks.md)

1. 识别执行章节开始事件的时间，然后使用章节信息创建 `ChapterObject` 实例。

   `ChapterObject` 章节跟踪引用：

   >[!NOTE]
   >
   >只有在您打算跟踪章节的情况下，才需要使用这些变量。

   | 变量名称 | 类型 | 描述 |
   | --- | --- | --- |
   | `name` | 字符串 | 表示章节名称的非空字符串。 |
   | `position` | 数字 | 章节在内容中的位置，从1开始。 |
   | `length` | 数字 | 正数，表示章节的长度。 |
   | `startTime` | 数字 | 章节开始时的播放头值。 |

   章节对象：

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. 如果为章节添加了自定义元数据，请为该元数据创建上下文数据变量：

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. 要开始跟踪章节播放，请在 `ChapterStart` 实例中调用 `MediaHeartbeat` 事件：

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. 当播放到达您通过自定义代码定义的章节结尾边界时，在 `ChapterComplete` 实例中调用 `MediaHeartbeat` 事件：

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请在 MediaHeartbeat 实例中调用 `ChapterSkip` 事件：

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. 如果存在任何其他章节，请重复执行步骤 1 至 5。
