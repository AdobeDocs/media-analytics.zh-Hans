---
title: 丢帧（指标）
description: 报告跨会话总和平均值的累计丢帧。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# 丢帧（指标）

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**丢帧**&#x200B;指标。 Adobe Analytics从同一`a.media.qoe.droppedFrameCount`上下文数据变量自动填充配对的[丢帧（维度）](/help/reporting/dimensions/dropped-frames.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.droppedFrames`字段，您可以将其用作维度或指标。 有关如何收集此变量，请参阅[丢帧](/help/implementation/variables/quality/dropped-frames.md)。*

>[!ENDSHADEBOX]

**丢帧**&#x200B;量度报告跨会话的累计丢帧，适用于总和、平均和百分位数汇总。 使用量度可计算报告时段内的总放置量，并比较不同内容、网络或播放器之间的帧渲染质量。

## 如何计算此指标

播放器在丢弃累积时更新QoE对象的`droppedFrames`值。 后端报告关闭调用中的最新值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.droppedFrameCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

对于会话级别的布尔报表（是否有任何丢帧），请使用[受丢帧影响的流](dropped-frame-impacted-streams.md)。
