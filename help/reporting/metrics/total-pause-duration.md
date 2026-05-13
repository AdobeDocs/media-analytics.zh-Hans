---
title: 暂停总持续时间
description: 报告查看者在会话期间暂停的累积秒数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 8%

---


# 暂停总持续时间

**总暂停持续时间**&#x200B;量度报告查看器在会话期间暂停的累积秒数。 该量度是每个`media.pauseStart`与后续`media.play`之间的所有间隔的总和。 多个暂停相加。 与[暂停事件](pause-events.md)配对，以获得平均暂停长度。

## 如何计算此指标

媒体后端计算每`media.pauseStart`与匹配的`media.play`事件之间经过的时钟时间的总和。 该量度在结束调用时报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在其他位置显示为（以秒为单位）。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.pauseTime`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
