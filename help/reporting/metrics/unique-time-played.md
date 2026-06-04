---
title: 独特播放时间
description: 报告在会话期间查看的不同内容的秒数，为搜寻回放删除重复项。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# 独特播放时间

**唯一播放时间**&#x200B;量度报告会话期间查看的不同内容的秒数，为通过向后搜寻重新播放的区段去重。 与[内容逗留时间](content-time-spent.md)相比，当查看者在同一会话中重新观看同一内容的一部分时，唯一播放时间会更短。

## 如何计算此指标

媒体后端会跟踪在会话期间查看了哪些播放头间隔，并对它们的合并进行求和。 播放同一段时长为5秒的片段两次，仍会计为5秒。 该量度在结束调用时报告。 该值在Analysis Workspace中显示为`HH:MM:SS`，在数据馈送、Data Warehouse和报表API中以秒为单位。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.uniqueTimePlayed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
