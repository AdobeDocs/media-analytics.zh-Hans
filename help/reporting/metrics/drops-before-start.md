---
title: 开始前丢帧
description: 计算查看器在呈现任何主内容之前退出的会话数。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%
---

# 开始前丢帧

**开始前丢弃**&#x200B;度量计算查看器在呈现任何主内容之前退出的会话。 量度会标记预先内容的放弃情况，而不考虑广告行为，因此它是衡量纯粹预先内容流失的最佳量度。 将其与[媒体开始](/help/reporting/metrics/media-starts.md)和[内容开始](/help/reporting/metrics/content-starts.md)配对，以计算从未生成内容帧的会话的共享。

## 如何计算此指标

媒体后端为关闭会话且从未在主内容上生成[播放](/help/implementation/events/playback/play.md)事件设置此标志。 该量度在结束调用时报告。 常见情况包括：查看器在前置广告期间退出，播放器在初始缓冲阶段无限期停止，或者在第一个主内容播放事件之前触发错误。 在所有这些情况下，会话记录了[媒体开始](/help/reporting/metrics/media-starts.md)，但没有记录[内容开始](/help/reporting/metrics/content-starts.md)，并且没有记录[进度标记](/help/reporting/metrics/progress-markers.md)。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.dropBeforeStart`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
