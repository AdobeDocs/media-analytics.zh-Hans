---
title: 缓冲事件（量度）
description: 计算缓冲事件的总和以及各个会话的平均值。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# 缓冲事件（量度）

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**缓冲事件**&#x200B;度量。 Adobe Analytics从同一`a.media.qoe.bufferCount`上下文数据变量自动填充配对的[缓冲事件（维度）](/help/reporting/dimensions/buffer-events.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.bufferCount`字段，您可以将其用作维度或指标。*

>[!ENDSHADEBOX]

**缓冲事件**&#x200B;量度计算跨会话的缓冲事件，适用于总和、平均和百分位数汇总。 使用该量度计算报告时段内的缓冲总量，并比较内容、网络或播放器间的缓冲稳定性。

## 如何计算此指标

每次播放器进入[缓冲开始](/help/implementation/events/playback/buffer-start.md)状态时，媒体后端都会递增计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.bufferCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

对于会话级别的布尔报表（会话是否遇到任何缓冲），请使用[受缓冲影响的流](buffer-impacted-streams.md)。
