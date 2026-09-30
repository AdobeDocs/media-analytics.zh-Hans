---
title: 受比特率更改影响的流
description: 计算至少发生一次比特率更改的会话数。
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
source-wordcount: '145'
ht-degree: 10%
---

# 受比特率更改影响的流

**比特率更改影响的流**&#x200B;度量计算至少发生一次比特率更改的会话。 量度是会话级别的布尔值；同一会话中的多个比特率更改计为一个受影响的流。 对于总比特率更改卷，请使用[比特率更改](/help/reporting/dimensions/bitrate-changes.md)。

## 如何计算此指标

媒体后端在会话期间首次收到[比特率更改](/help/implementation/events/playback/bitrate-change.md)事件时设置此标志。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.bitrateChange`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
