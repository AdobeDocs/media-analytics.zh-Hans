---
title: 在 Chromecast 中跟踪章节和区段
description: 本主题介绍如何在 Chromecast 中使用 Media SDK 实施章节和区段跟踪。
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Chromecast 中跟踪章节和区段{#track-chapters-and-segments-on-chromecast}

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

   章节对象：[createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. 如果为章节添加了自定义元数据，请为该元数据创建上下文数据变量：

   ```js
   var chapterContextData = { 
       segmentType: "Sample segment type" 
   };
   ```

1. 要开始跟踪章节播放，请跟踪 `ChapterStart` 事件：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData); 
   ```

1. 当播放到达您通过自定义代码定义的章节结尾边界时，在 `ChapterComplete` 实例中调用 `MediaHeartbeat` 事件：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请跟踪 `ChapterSkip` 事件：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip); 
   ```

1. 如果存在任何其他章节，请重复执行步骤 1 至 5。

