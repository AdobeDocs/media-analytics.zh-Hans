---
title: 隐藏式字幕总时长
description: 报告在会话期间启用的累积秒数字幕。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 7%

---


# 隐藏式字幕总时长

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**隐藏式字幕总持续时长**&#x200B;报表量度。 有关如何收集此变量，请参阅[隐藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)。*

>[!ENDSHADEBOX]

**隐藏式字幕总时长**&#x200B;量度报告在会话期间启用字幕的累计时间（以秒为单位）。 后端对支持字幕的状态开始事件和匹配的状态结束事件之间的每个间隔求和。

## 如何计算此指标

媒体后端计算会话期间所有启用字幕的时间总和。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.closedcaptioning.time`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "closedCaptioning"`，字段`time` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
