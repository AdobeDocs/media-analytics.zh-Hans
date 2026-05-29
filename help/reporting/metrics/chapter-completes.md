---
title: 章节结束
description: 计入每个播放到结束的章节。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# 章节结束

**章节完成**&#x200B;指标计算每个播放到结束的章节。 将其与[章节开始](chapter-starts.md)配对，以计算章节完成率。

## 如何计算此指标

当收到[章节结束](/help/implementation/events/chapters/chapter-complete.md)事件时，媒体后端会设置此标志。 该量度在章节关闭调用中报告。 在播放过程中跳过或放弃的章节不计为已完成。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体章节]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.chapter.complete`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
