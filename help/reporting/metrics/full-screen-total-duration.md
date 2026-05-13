---
title: 全屏总时长
description: 报告查看器在会话期间全屏停留的累积秒数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 全屏总时长

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**全屏总持续时间**&#x200B;报告量度。 有关如何收集此变量，请参阅[全屏](/help/implementation/variables/player-state/full-screen.md)。*

>[!ENDSHADEBOX]

**全屏总持续时间**&#x200B;量度报告查看器在会话期间全屏使用的累积时间（以秒为单位）。 后端计算全屏状态 — 开始事件与匹配状态 — 结束事件之间的每个间隔的总和。

## 如何计算此指标

媒体后端计算会话期间所有全屏间隔的占用时间总和。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.fullscreen.time`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "fullscreen"`，字段`time` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
