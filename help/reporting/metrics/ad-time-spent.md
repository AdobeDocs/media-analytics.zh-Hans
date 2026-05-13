---
title: 广告逗留时间
description: 报告每个会话的活动广告播放总秒数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---


# 广告逗留时间

**广告逗留时间**&#x200B;量度报告每个会话的活动广告播放总秒数，不包括暂停、缓冲和停止。 请将其与[内容逗留时间](/help/reporting/metrics/content-time-spent.md)配对，以将广告加载与内容参与进行比较。

## 如何计算此指标

媒体后端计算播放器在广告上处于`play`状态时两个事件之间经过的时钟时间的总和。 暂停和缓冲期间的时间被排除。 该量度将在广告关闭调用中报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在数据馈送、Data Warehouse和报表API中以秒为单位。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.timePlayed`自动收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
