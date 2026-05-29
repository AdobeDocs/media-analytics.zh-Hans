---
title: 媒体逗留时间
description: 报告每个会话的活动播放总秒数，包括广告。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 8%

---


# 媒体逗留时间

**媒体逗留时间**&#x200B;量度报告每个会话的活动播放总秒数，包括主内容和广告，但不包括暂停、缓冲和停止。 使用此插件可测量查看者与播放器积极联系的总时间。 仅对于主内容，使用[内容逗留时间](content-time-spent.md)。

## 如何计算此指标

对于主要内容或广告，媒体后端计算播放器处于`play`状态时事件之间经过的时钟时间的总和。 暂停期间、缓冲事件和停滞被排除。 该量度在结束调用时报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在数据馈送、Data Warehouse和报表API中以秒为单位。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.totalTimePlayed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
