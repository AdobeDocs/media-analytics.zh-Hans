---
title: 章节开始
description: 计入会话期间开始播放的每个章节。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---


# 章节开始

**章节开始**&#x200B;指标计算会话期间开始播放的每一个章节。 将其与[章节完成](chapter-completes.md)配对，以计算章节完成率。

## 如何计算此指标

在收到`media.chapterStart`事件时，媒体后端设置`mediaReporting.chapterDetails.isStarted = true`。 该量度在章节关闭调用中报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体章节]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.chapter.view`收集。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
