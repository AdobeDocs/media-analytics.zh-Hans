---
title: 章节逗留时间
description: 报告每个章节的活动播放总秒数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# 章节逗留时间

**章节逗留时间**&#x200B;量度报告每个章节的活动播放总秒数。 将其与[章节长度](/help/reporting/dimensions/chapter-length.md)配对，以计算每个使用章节的份额。

## 如何计算此指标

当播放器在章节中处于`play`状态时，媒体后端计算两个事件之间经过的时钟时间的总和。 暂停期间、缓冲期间和停止期间的时间被排除。 该量度在章节关闭调用中报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在数据馈送、Data Warehouse和报表API中以秒为单位。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体章节]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.chapter.timePlayed`收集。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
