---
title: 媒体开始
description: 计算开始的每个媒体会话，包括以前置广告或缓冲结束的会话。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%

---


# 媒体开始

**媒体开始**&#x200B;量度将计入每个开始的媒体会话。 一旦后端收到[会话开始](/help/implementation/events/session/session-start.md)事件，即使查看者在前置广告、缓冲或任何主内容播放之前退出，此时间也会递增。 将其用作funnel排名最前的媒体报表量度；将其与[Content starts](content-starts.md)配对，以测量广告和缓冲流失。

## 如何计算此指标

媒体后端在收到[会话开始](/help/implementation/events/session/session-start.md)事件时设置此标志。 报告的指标是每个会话`1`。 媒体开始次数是在开始调用时报告的，而不是在关闭调用时报告的；它是唯一不会等待会话关闭的量度。 所有其他媒体量度，包括[内容开始](/help/reporting/metrics/content-starts.md)、[内容逗留时间](/help/reporting/metrics/content-time-spent.md)和[进度标记](/help/reporting/metrics/progress-markers.md)，都会在结束调用时报告，并且在播放期间无法实时使用。 [广告开始](/help/reporting/metrics/ad-starts.md)是报告其触发事件而不是关闭时的附加量度。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.view`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.view` |
