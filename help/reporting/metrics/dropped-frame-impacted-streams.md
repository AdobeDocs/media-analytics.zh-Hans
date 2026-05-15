---
title: 受丢帧影响的流
description: 计算至少丢弃了一个帧的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 11%

---


# 受丢帧影响的流

**丢帧影响的流**&#x200B;度量计算至少丢帧了一次的会话数。 量度是会话级别的布尔值 — 在一个受影响的流中，同一会话计数的多个丢帧。 对于总丢帧量，请使用[丢帧](dropped-frames.md)。

## 如何计算此指标

如果会话关闭时QoE对象的`droppedFrames`值大于零，则媒体后端设置`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams = true`。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.droppedFrames`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
