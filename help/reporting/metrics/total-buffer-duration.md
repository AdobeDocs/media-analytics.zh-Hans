---
title: 缓冲总持续时间（量度）
description: 报告跨会话总和平均值的累积缓冲时间。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 7%

---


# 缓冲总持续时间（量度）

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**总缓冲持续时间**&#x200B;指标。 Adobe Analytics从同一`a.media.qoe.bufferTime`上下文数据变量自动填充配对的[缓冲总持续时间（维度）](/help/reporting/dimensions/total-buffer-duration.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.bufferTime`字段，您可以将其用作维度或指标。*

>[!ENDSHADEBOX]

**总缓冲持续时间**&#x200B;量度报告跨会话的累积缓冲时间，适用于总计、平均值和百分位数汇总。 使用该量度可计算客户在报表时段内等待缓冲区所花费的总时间。

## 如何计算此指标

媒体后端计算每个缓冲时间间隔（从[缓冲开始](/help/implementation/events/playback/buffer-start.md)到下一个状态更改）的持续时间总和。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.bufferTime`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |
