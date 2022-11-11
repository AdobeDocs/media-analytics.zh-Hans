---
title: 了解如何在Roku中跟踪章节和区段
description: 了解如何在Roku中使用Media SDK实施章节和区段跟踪。
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 88%

---

# 在 Roku 中跟踪章节和区段{#track-chapters-and-segments-on-roku}

以下说明为使用 2.x SDK 进行实施提供了指南。

>[!IMPORTANT]
>
> 如果您实施的是 1.x 版本的 SDK，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施标准广告元数据

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

   ```
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. 如果为章节添加了自定义元数据，请为该元数据创建上下文数据变量：

   ```
   chapterContextData = {}
   chapterContextData["seg_type"] = "seg_type"
   chapterContextData["seg_name"] = "seg_name"
   chapterContextData["seg_info"] = "seg_info"
   ```

1. 要开始跟踪章节播放，请在 `ChapterStart` 实例中调用 `MediaHeartbeat` 事件：

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. 当播放达到您通过自定义代码定义的章节结尾边界时，在 `MediaHeartbeat` 实例中调用 `ChapterComplete` 事件。

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. 如果由于用户选择跳过章节（例如，用户搜寻章节边界之外的内容）而使章节播放未能完成，请在 MediaHeartbeat 实例中调用 `ChapterSkip`。

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. 如果存在任何其他章节，请重复执行步骤 1 至 5。
