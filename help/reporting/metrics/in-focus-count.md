---
title: 聚焦计数
description: 报告播放器在会话期间获得焦点的次数。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# 聚焦计数

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**聚焦计数**&#x200B;报告量度。 请参阅[焦点](/help/implementation/variables/player-state/in-focus.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**聚焦计数**&#x200B;量度报告播放器在会话期间获得聚焦的次数。 每个焦点状态开始事件都会增加计数。 与受会话级布尔值汇总影响的流数量[进行配对](in-focus-streams-impacted.md)，与处于状态的总时间处于焦点状态的总持续时间为[进行配对](in-focus-total-duration.md)。

## 如何计算此指标

媒体后端会递增每个焦点状态开始事件的此计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.states.infocus.count`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "inFocus"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
