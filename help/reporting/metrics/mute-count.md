---
title: 静音计数
description: 报告查看器在会话期间静音的次数。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# 静音计数

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**静音计数**&#x200B;报告量度。 有关如何收集此变量，请参阅[静音](/help/implementation/variables/player-state/mute.md)。*

>[!ENDSHADEBOX]

**静音计数**&#x200B;量度报告查看器在会话期间静音的次数。 每个静音状态开始事件都会增加计数。 与受静音影响的[个流配对](mute-streams-impacted.md)进行会话级别的布尔汇总，与[静音总持续时间](mute-total-duration.md)进行状态总时间。

## 如何计算此指标

媒体后端会在每个静音状态开始事件时增加此计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.states.mute.count`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "mute"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
