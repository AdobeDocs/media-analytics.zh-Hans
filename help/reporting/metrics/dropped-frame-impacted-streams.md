---
title: 受丢帧影响的流
description: 计算至少丢弃了一个帧的会话数。
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%

---


# 受丢帧影响的流

**丢帧影响的流**&#x200B;度量计算至少丢帧了一次的会话数。 量度是会话级别的布尔值；同一会话内多次删除的会话计数相当于一个受影响的流。 对于总丢帧量，请使用[丢帧](dropped-frames.md)。

## 如何计算此指标

如果会话关闭时QoE对象的`droppedFrames`值大于零，媒体后端将设置此标志。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.droppedFrames`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
