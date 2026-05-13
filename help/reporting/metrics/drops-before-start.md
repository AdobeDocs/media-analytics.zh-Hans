---
title: 开始前丢帧
description: 计算查看器在呈现任何主内容之前退出的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 8%

---


# 开始前丢帧

**开始前丢弃**&#x200B;度量计算查看器在呈现任何主内容之前退出的会话。 量度会标记预先内容的放弃情况，而不考虑广告行为，因此它是衡量纯粹预先内容流失的最佳量度。 将其与[媒体开始](/help/reporting/metrics/media-starts.md)和[内容开始](/help/reporting/metrics/content-starts.md)配对，以计算从未生成内容帧的会话的共享。

## 如何计算此指标

媒体后端为关闭的会话设置`mediaReporting.qoeDataDetails.isDroppedBeforeStart = true`，而不会在主内容上生成`media.play`事件。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.dropBeforeStart`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
