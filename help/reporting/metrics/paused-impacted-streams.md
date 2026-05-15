---
title: 受暂停影响的流
description: 计算查看器至少暂停一次的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 11%

---


# 受暂停影响的流

**受暂停影响的流**&#x200B;量度计算查看器至少暂停一次的会话。 它是一个会话级别的布尔值。 同一会话中的多次暂停计为一个受影响的流。 使用它来测量经历任何暂停的会话的份额；对于总暂停量，使用[暂停事件](pause-events.md)。

## 如何计算此指标

在会话期间首次收到[暂停开始](/help/implementation/events/playback/pause-start.md)事件时，媒体后端设置`mediaReporting.sessionDetails.hasPauseImpactedStreams = true`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.pause`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | 不适用 |
