---
title: 内容开始
description: 计算主内容实际开始播放的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 10%

---


# 内容开始

**Content starts**&#x200B;量度计算主内容实际开始播放的会话数。 与[媒体开始](media-starts.md)不同，它排除在前置广告、缓冲或停止期间结束的会话。 这使得它成为完成率和参与率的正确分母。

## 如何计算此指标

媒体后端在首次接收主内容的[播放](/help/implementation/events/playback/play.md)事件时设置此标志。 该量度在该播放事件中触发，但在关闭调用时报告。 若要计算前段下拉率，请使用`(Media starts − Content starts) / Media starts`。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.play`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.play` |
