---
title: 平均比特率（量度）
description: 报告每个会话的原始加权平均比特率（以kbps为单位）。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 8%

---


# 平均比特率（量度）

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**平均比特率**&#x200B;事件度量，该度量报告每个会话的原始加权平均比特率。 请参阅分段维度的平均比特率（维度）[&#128279;](/help/reporting/dimensions/average-bitrate.md)。 有关如何收集此变量，请参阅[比特率](/help/implementation/variables/quality/bitrate.md)。*

>[!ENDSHADEBOX]

**平均比特率**&#x200B;量度报告每个会话的原始加权平均播放比特率（以kbps为单位）。 与[分段维度](/help/reporting/dimensions/average-bitrate.md)不同，该量度是一个连续的数值，适用于跨会话的总和、平均值和百分位数汇总。

## 如何计算此指标

媒体后端计算会话期间报告的所有比特率值的加权平均值，该加权平均值按每个比特率处于活动状态的持续时间进行加权。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.bitrateAverage`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverage` |
