---
title: 比特率更改（量度）
description: 计算各个会话的总和平均值的比特率更改事件。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%

---


# 比特率更改（量度）

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**比特率更改**&#x200B;量度。 Adobe Analytics从同一`a.media.qoe.bitrateChangeCount`上下文数据变量自动填充配对的[比特率更改（维度）](/help/reporting/dimensions/bitrate-changes.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`字段，您可以将其用作维度或指标。 有关如何触发比特率更改事件，请参阅[比特率更改](/help/implementation/variables/quality/bitrate-change.md)。*

>[!ENDSHADEBOX]

**比特率更改**&#x200B;量度计算跨会话的比特率更改事件，适用于总和、平均值和百分位数汇总。 使用量度可计算报告时段内比特率更改的总量，并比较内容、网络或播放器之间的比特率稳定性。

## 如何计算此指标

媒体后端在会话期间每收到[比特率更改](/help/implementation/events/playback/bitrate-change.md)事件就递增计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.bitrateChangeCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

对于会话级别的布尔报表（会话是否遇到任何比特率更改），请使用[受比特率更改影响的流](bitrate-change-impacted-streams.md)。
