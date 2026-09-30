---
title: 静音总时长
description: 报告会话期间音频静音的累积秒数。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%
---

# 静音总时长

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**静音总持续时间**&#x200B;报告量度。 有关如何收集此变量，请参阅[静音](/help/implementation/variables/player-state/mute.md)。*

>[!ENDSHADEBOX]

**静音总持续时间**&#x200B;量度报告会话期间音频静音的累计时间（以秒为单位）。 后端对静音状态开始事件和匹配状态结束事件之间的每个间隔求和。

## 如何计算此指标

媒体后端计算会话期间所有静音间隔内经过的时间总和。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.states.mute.time`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "mute"`，字段`time` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.mute.time` |
