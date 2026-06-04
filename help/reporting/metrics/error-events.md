---
title: 错误事件
description: 计算错误事件的总和以及跨会话的平均值。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# 错误事件

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**错误事件**量度。 Adobe Analytics从同一`a.media.qoe.errorCount`上下文数据变量自动填充配对的[错误维度](/help/reporting/dimensions/errors.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.errorCount`字段，您可以将其用作维度或指标。*

>[!ENDSHADEBOX]

**错误事件**&#x200B;量度计算跨会话的错误事件，适用于总和、平均值和百分位数汇总。 使用该量度计算报告时段内的总错误量，并比较内容、网络或播放器之间的错误率。

## 如何计算此指标

媒体后端会递增播放器报告的每个错误的计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.errorCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

对于会话级别的布尔报表（无论是否发生任何错误），请使用[受错误影响的流](error-impacted-streams.md)。
