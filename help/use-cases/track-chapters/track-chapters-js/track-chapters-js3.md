---
title: 了解如何使用 JavaScript 3.x 跟踪章节和区段
description: 了解如何在浏览器应用程序 (JS) 中使用 Media SDK 实施章节和区段跟踪。
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/YZAcZVcqS15hCae-LYwjpSYztXijauQNIzElCcWcPT0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 224
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
