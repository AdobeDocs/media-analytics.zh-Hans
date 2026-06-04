---
title: 受缓冲影响的流
description: 计算播放器至少一次进入缓冲状态的会话数。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---


# 受缓冲影响的流

**Buffer影响的流**&#x200B;度量对播放器至少一次进入缓冲状态的会话进行计数。 量度是会话级别的布尔值 — 在一个受影响的流中，同一会话中有多个缓冲事件计数。 对于总缓冲卷，请使用[缓冲事件](buffer-events.md)。

## 如何计算此指标

媒体后端在会话期间首次收到[缓冲开始](/help/implementation/events/playback/buffer-start.md)事件时设置此标志。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.buffer`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
