---
title: 了解如何使用 JavaScript 3.x 跟踪章节和区段
description: 了解如何在浏览器应用程序 (JS) 中使用 Media SDK 实施章节和区段跟踪。
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 100%

---

# 使用 JavaScript 3.x 跟踪章节和区段{#track-chapters-and-segments-on-javascript}

以下说明为使用 3.x SDK 的实施提供了指南。

>[!IMPORTANT]
>
> 如果您实施的是 SDK 之前的版本，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

1. 识别执行章节开始事件的时间，然后使用章节信息创建 `ChapterObject` 实例。

   `ChapterObject` 章节跟踪引用：

   >[!NOTE]
   >
   >只有在您打算跟踪章节的情况下，才需要使用这些变量。

   | 变量名称 | 类型 | 描述 |
   | --- | --- | --- |
   | `name` | 字符串 | 表示章节名称的非空字符串。 |
   | `position` | 数字 | 内容中章节的位置，从 1 开始编号。 |
   | `length` | 数字 | 正数，表示章节长度。 |
   | `startTime` | 数字 | 章节开头的播放头值。 |

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
