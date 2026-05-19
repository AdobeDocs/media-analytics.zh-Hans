---
title: 聚焦总时长
description: 报告播放器在会话期间聚焦的累积秒数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# 聚焦总时长

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**聚焦总持续时间**&#x200B;报告量度。 请参阅[焦点](/help/implementation/variables/player-state/in-focus.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**聚焦总持续时间**&#x200B;量度报告播放器在会话期间聚焦的累计时间（以秒为单位）。 后端将计算焦点状态 — 开始事件和匹配状态 — 结束事件之间的每个间隔的总和。

## 如何计算此指标

媒体后端计算会话期间所有聚焦间隔内经过的时间总和。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.infocus.time`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "inFocus"`，字段`time` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.infocus.time` |
