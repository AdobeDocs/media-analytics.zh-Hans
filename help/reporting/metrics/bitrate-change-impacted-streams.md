---
title: 受比特率更改影响的流
description: 计算至少发生一次比特率更改的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# 受比特率更改影响的流

**比特率更改影响的流**&#x200B;度量计算至少发生一次比特率更改的会话。 量度是会话级别的布尔值 — 在同一会话中，多个比特率更改计为一个受影响的流。 对于总比特率更改卷，请使用[比特率更改](/help/reporting/dimensions/bitrate-changes.md)。

## 如何计算此指标

在会话期间首次收到[比特率更改](/help/implementation/events/playback/bitrate-change.md)事件时，媒体后端设置`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.bitrateChange`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
