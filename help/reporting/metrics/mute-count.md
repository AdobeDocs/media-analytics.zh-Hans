---
title: 静音计数
description: 报告查看器在会话期间静音的次数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---


# 静音计数

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**静音计数**&#x200B;报告量度。 有关如何收集此变量，请参阅[静音](/help/implementation/variables/player-state/mute.md)。*

>[!ENDSHADEBOX]

**静音计数**&#x200B;量度报告查看器在会话期间静音的次数。 每个静音状态开始事件都会增加计数。 与受静音影响的[个流配对](mute-streams-impacted.md)进行会话级别的布尔汇总，与[静音总持续时间](mute-total-duration.md)进行状态总时间。

## 如何计算此指标

媒体后端在每个mute state-start事件中递增`mediaReporting.states[]`的`mute`条目中的`count`字段。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.mute.count`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "mute"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
