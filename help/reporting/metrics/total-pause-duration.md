---
title: 暂停总持续时间
description: 报告查看者在会话期间暂停的累积秒数。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---


# 暂停总持续时间

**总暂停持续时间**&#x200B;量度报告查看器在会话期间暂停的累积秒数。 该量度是每个[暂停开始](/help/implementation/events/playback/pause-start.md)事件与后续[播放](/help/implementation/events/playback/play.md)事件之间的所有间隔的总和。 多个暂停相加。 与[暂停事件](pause-events.md)配对，以获得平均暂停长度。

## 如何计算此指标

媒体后端计算每[暂停开始](/help/implementation/events/playback/pause-start.md)事件与匹配的[播放](/help/implementation/events/playback/play.md)事件之间经过的时钟时间的总和。 该量度在结束调用时报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在其他位置显示为（以秒为单位）。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.pauseTime`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | 不适用 |
