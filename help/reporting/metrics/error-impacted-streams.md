---
title: 受错误影响的流
description: 计算至少发生一个错误的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---


# 受错误影响的流

**错误影响的流**&#x200B;量度计算至少发生一个错误（`trackError`被调用或[错误](/help/implementation/events/error.md)事件已触发）的会话数。 量度是会话级别的布尔值 — 在一个受影响的流中，相同的会话计为多个错误。 对于总错误量，请使用[错误](/help/reporting/dimensions/errors.md)。

## 如何计算此指标

在会话期间首次收到[错误](/help/implementation/events/error.md)事件时，媒体后端设置`mediaReporting.qoeDataDetails.hasErrorImpactedStreams = true`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.error`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
