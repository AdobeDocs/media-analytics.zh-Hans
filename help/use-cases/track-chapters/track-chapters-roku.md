---
title: 了解如何在 Roku 中跟踪章节和区段
description: 了解如何在 Roku 中使用 Media SDK 实施章节和区段跟踪。
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Z06I7x3nDZvYHoQHo9bcjs4UiS2YR6yN8rwJqG3vX1w
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
source-wordcount: 203
ht-degree: 93%

---

# 在 Roku 中跟踪章节和区段{#track-chapters-and-segments-on-roku}

以下说明为使用 2.x SDK 的实施提供了指南。

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
