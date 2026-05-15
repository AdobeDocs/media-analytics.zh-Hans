---
title: 内容逗留时间
description: 报告每个会话的活动主内容播放的总秒数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 8%

---


# 内容逗留时间

**内容逗留时间**&#x200B;量度报告每个会话的活动主内容播放总秒数，不包括广告、暂停、缓冲和停顿。 将其用作内容查看的参与量度；有关包括广告在内的逗留时间，请参阅[媒体逗留时间](media-time-spent.md)。

## 如何计算此指标

媒体后端计算播放器在主内容上处于`play`状态时事件之间经过的时钟时间的总和。 在广告、暂停、缓冲事件和停滞期间排除时间。 该量度在结束调用时报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在数据馈送、Data Warehouse和报表API中以秒为单位。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.timePlayed`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
